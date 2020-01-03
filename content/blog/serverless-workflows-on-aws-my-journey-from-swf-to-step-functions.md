+++
title = "Serverless workflows on AWS: my journey from SWF to Step Functions"
date = 2016-12-29T18:07:39-05:00
description = ""
og_image = "forrest.png"
+++

<em>AWS Lambda functions can only run for a maximum of five minutes. This must be distinctly understood, or nothing wonderful can come of the story you are about to hear.</em>
<h2>The Problem</h2>
This past summer, my team and I set out to build an internal software system used for deployment testing on AWS. The application would run a large number of workflow executions in parallel each night and might perform a few one-off executions during the day - maybe six hours total use out of every twenty-four, with only a small fraction of that time spent doing actual compute tasks. Trying to scale, manage and spend money on EC2 instances for that workload didn't interest us. We wanted to run our whole workflow process end-to-end on <a href="https://aws.amazon.com/lambda/">AWS Lambda</a>.

And we did. Heaven help us, we did. This is our story.

<h2>Helpful Background: Workflows on AWS</h2>
<em>(You can skip this section if you know SWF already) </em>

If your cloud application has lots of moving parts and does asynchronous processing, you probably need some kind of distributed workflow service: an orchestration system that will help you hand out tasks to worker processes and manage central state.

If your cloud is AWS, you may already be familiar with their well-established workflow service, <a href="https://aws.amazon.com/swf/">SWF</a>. The "S" stands for "Simple", which is a bit of a misnomer, but using SWF is at least easier than building a fully managed, highly available workflow engine on your own. SWF's fundamental abstractions are the "decider" - a piece of compute logic that figures out what task to perform next - and "workers", ancillary processes that do the decider's bidding. Implementing these functions is up to you. SWF makes sure each task gets assigned exactly once, maintains a record of task state throughout the workflow, and generally acts like a helpful parent getting children out the door on time for school.

The SWF <a href="https://aws.amazon.com/swf/faqs/">FAQ</a> says that workers and the decider "can run on cloud infrastructure, such as Amazon EC2, or on machines behind firewalls." SWF also provides a mechanism for invoking AWS Lambda functions as worker tasks. But the implicit assumption is that you will use a long-running, persistent server for your decider.

That last point did not sit well with my team. For the reasons mentioned above, we much preferred to put that decider on Lambda too.
<h2>Serverless Workflows on SWF</h2>
AWS Lambda functions, as I said, can only run for a maximum of five minutes. But SWF architecture requires the decider regularly to poll SWF for what are called "decision tasks" - notifications that an activity worker has completed its duties and handed control back to the workflow. Our decider logic, when coordinating a more complicated deployment test, might have to do this polling for a couple of hours. How to perform this long-running task on a very short-running Lambda function?

Our initial answer: CloudWatch Events. Each time we started a workflow, we set up a CloudWatch rule that invoked the decider Lambda function every couple of minutes. The decider would wake up, check SWF, and go back to sleep if nothing interesting was happening.

The design looked something like this:

[caption id="attachment_2573" align="alignnone" width="760"]<img class="alignnone size-full wp-image-2573" src="/images/swf-serverless.png" alt="blank-diagram-page-1" width="760" height="528" /> Figure 1. Our serverless SWF design, at PowerPoint levels of naivety[/caption]

 

While our implementation of this design worked well enough for the first few months of the project's life, its limitations quickly became clear:
<ul>
 	<li><strong>Latency.</strong> CloudWatch rules cannot run more frequently than once a minute, and SWF scheduling delays made it advisable to invoke the decider even less frequently than that. This situation created significant latency between workflow actions, leading to inflated workflow times that were especially noticeable for workflows involving lots of short tasks.</li>
 	<li><strong>Cost.</strong> Having to run the decider on a two-minute loop throughout the life of the workflow somewhat negated the cost advantages we hoped to get from using Lambda instead of EC2 in the first place, especially as our number of workflows scaled up.</li>
 	<li><strong>Runtime State. </strong>Every time the Lambda decider function ran, it had to figure out where it was in the workflow process. SWF is supposed to make stateless execution easy, and it provides the complete deployment workflow history as a JSON blob when handing tasks to the decider, but the blob quickly becomes unmanageably large and filled with superfluous data. To keep track of what was going on in the workflows, we resorted to maintaining ephemeral state in a DynamoDB table, adding more latency and cost.</li>
 	<li><strong>Retries/Error Handling. </strong>SWF, I regret to say, has bugs<strong>. </strong>Sometimes SWF completely fails to schedule a task, or does it so late that the workflow's task timeout expires. Finding and catching these errors required even more state maintained outside of SWF.</li>
 	<li><strong>Debugging. </strong>The<strong> </strong>SWF console's workflow event views are difficult to read, oddly paginated and don't provide much information, leading to a rabbit trail of log searches anytime something went wrong.</li>
 	<li><strong>Code Maintainability. </strong>The combination of multiple state sources and ramifying failure scenarios, not to mention the central "hack" of running the SWF decider in a loop, led to a mess of one-off fixes and hacky workarounds in our codebase.</li>
</ul>
All in all, this first design was a good (or rather, very bad) example of what I'll call "serverless for serverless's sake". In retrospect, if I'm being completely honest with myself, we would have done just as well to forego the whole Lambda idea and run the decider on a set of EC2 instances.

But once that sweet serverless stuff hits your bloodstream, it's pretty hard to quit. As use of our application scaled up and our back end got more and more unwieldy, we clutched to a rumor we'd heard from our AWS liaison that some sort of "serverless-first" update to SWF was in the works. What we needed was a true serverless workflow system: one that didn't require constant polling, could pass minimal state between Lambda functions without requiring additional database infrastructure and had no long-running components whatsoever. Though we didn't quite realize it, what we needed was a state machine.
<h2 id="WindsorandStepFunctions-StepFunctions(SFN)">Enter Step Functions</h2>
Lo and behold, AWS announced a new service called <a class="external-link" href="https://aws.amazon.com/step-functions/" rel="nofollow">Step Functions</a> (SFN) during re:Invent in November 2016. Yep, it's state machines - and a whole lot more. A Step Functions state machine processes JSON the way a sea cucumber processes sand. It hooks together the input and output of Lambda functions in one giant tube of state, all wrapped up in a JSON template definition that is grandiosely called the "Amazon States Language". Here are a few of the best features of SFN:
<ul>
 	<li>Visual workflows</li>
</ul>
Step Functions ingests your JSON template and turns it into a real-time graphical view, helping you make sense of your state machine's current, well, state.

[caption id="attachment_2623" align="alignnone" width="1122"]<img class="alignnone size-full wp-image-2623" src="/images/sfn-diagram.png" alt="SFN visual" width="1122" height="1042" /> Figure 2. The visual representation for one of our early workflow tests. Green means the step succeeded.[/caption]

 
<ul>
 	<li>No need to talk to the orchestrator</li>
</ul>
SWF requires deciders to ask the system for tasks and workers to let the system know when they're done. The beauty of SFN is that your business code doesn't need to know anything about SFN. Each Lambda function is completely self-contained. It accepts input and returns output. The state machine just passes the baton.
<ul>
 	<li>Easy implementation of dynamic backoff for async tasks</li>
</ul>
If your workflow has I/O-bound periods where it's waiting on some external task, you don't want to burn any more compute time than necessary. Not only does SFN let you include "wait states" that sit there counting sheep before calling your next Lambda function, but you can parameterize the duration of the wait period to build your own dynamic exponential backoff.

Needless to say, we took one look at Step Functions and knew that our poor, hardworking SWF solution was history. A little over a month later, we've rewritten our entire application to use SFN, and we're loving the results.

 
<h2 id="WindsorandStepFunctions-SFNvsSWF">SFN vs SWF</h2>
SFN state machines have already demonstrated improvement over our old SWF solution in the following areas:
<ul>
 	<li><strong>Latency.</strong> One of our workflows with several short deployment steps took thirty minutes to run under the old system. It takes -- no kidding -- thirty seconds to run to completion on SFN.</li>
 	<li><strong>Cost.</strong> No SWF decider means no Lambda functions treated like persistent compute, which radically lowers cost. Moreover, the state machine structure of SFN means no calls to a DynamoDB state table.</li>
 	<li><strong>Runtime State. </strong>The state machine seamlessly transfers the minimal amount of data needed between lambda functions, eliminating the need for other logs or database tables to hold runtime state.</li>
 	<li><strong>Retries/Error Handling. </strong>SFN retries failed executions and easily reroutes errors.</li>
 	<li><strong>Debugging. </strong>Visual workflows help quickly pinpoint solutions to state machine problems.</li>
 	<li><strong>Code Maintainability. Our </strong>codebase has now been completely refactored to take advantage of SFN's better abstractions and streamlined requirements. I think there's about half as much code as there was before.</li>
</ul>
Of course, SFN is still a new service with plenty of quirks and feature gaps. A couple of current things to keep in mind:
<ul>
 	<li>As of this writing, CloudFormation does not yet support Step Functions, so all SFN automation must happen in code.</li>
 	<li>SFN has had <a class="external-link" href="https://forums.aws.amazon.com/thread.jspa?threadID=244399" rel="nofollow">some issues</a> with properly deleting state machines. The AWS folks appear to be actively working on the issue.</li>
 	<li>SFN is only available in a few regions so far, so make sure to check <a href="http://docs.aws.amazon.com/general/latest/gr/rande.html#step-functions_region">this list</a> before getting started. However, AWS has already hinted that Step Functions will displace SWF as their go-to workflow solution in the future, so I wouldn't worry about widespread availability for long.</li>
</ul>
<h2 id="WindsorandStepFunctions-SFNvsSWF">Lessons from the journey</h2>
The world of serverless changes fast. Keep in mind that AWS Lambda itself is barely two years old, and most of the ecosystem around it is quite a bit more recent. Just because a service you need isn't around today, doesn't mean it won't exist tomorrow. In the meantime, living a bit past the bleeding edge certainly has drawbacks, but there are advantages too. Without the knowledge we gained from several months of trying to fit the round peg of serverless workflows into the square hole of SWF, we wouldn't have been able to make such a fast cutover to Step Functions.

And I'm more than happy to share that knowledge. So please hit me up if you have questions about any of the technologies discussed in this post. I'd love to chat with you about serverless workflows on AWS!

 
