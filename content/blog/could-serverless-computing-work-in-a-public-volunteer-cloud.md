+++
title = "Could Serverless Computing Work in a Public Volunteer Cloud?"
date = 2018-05-26T18:23:17-05:00
description = ""
draft = false
+++

<h4>Serverless computing</h4>
What's that old schoolyard rhyme? "AWS and Azure, sitting in a tree, I - A -A - S,  P - A -Y - G. First come VMs, then containers, then come stateless microservices running on public cloud infrastructure at fractions of a cent per second." Or something like that.

Anyway, application deployments are getting lighter, backend microservices are getting smaller, and now many development shops are moving toward "serverless architectures" in which dynamic computational tasks are handled using a few cycles on somebody else's managed server. As of 2016, the public cloud giants (<a href="https://aws.amazon.com/lambda/">AWS</a>, <a href="https://cloud.google.com/functions/docs/">Google Cloud</a> and <a href="https://azure.microsoft.com/en-us/services/functions/">Microsoft Azure</a>) all have their own "serverless services" that allow you to buy processing time for cheap. And I do mean cheap - a million AWS Lambda requests per month, each lasting five seconds, <a href="https://s3.amazonaws.com/lambda-tools/pricing-calculator.html">will set you back about $10.62</a>.

Developers gravitate toward this approach because it's scalable, cost-effective and requires little to no infrastructure maintenance. In AWS, you might deploy an application with data stores in RDS or DynamoDB, static web content hosted in S3, an API Gateway directing traffic and Lambda functions running the business rules - look Mom, no servers!

But wait a minute. Is a pay-as-you-go public cloud really the only place to run serverless compute functions? After all, a handful of computer scientists have been running little pieces of code on distributed computers for years, at a price even Lambda will never beat: free.

<!--more-->
<h4>Enter the "volunteer cloud"</h4>
<a href="https://en.wikipedia.org/wiki/Volunteer_computing">Volunteer computing</a> is a decades-old distributed computing model, typically used by a university or other research facility to crowdsource computationally-intensive tasks. Ordinary computer users connect their home PCs to a centralized service, using their CPU's idle cycles to process small jobs as part of the research project's larger goal.

The largest and best-organized volunteer computing effort is UC Berkeley's open source <a href="https://boinc.berkeley.edu">BOINC framework</a>, currently facilitating about 60 research projects around the world. <a href="http://boinc.berkeley.edu/boinc_papers/crossroads.pdf">This UC Berkeley paper</a>, uploaded in 2013, has a good overview of volunteer computing's history and its ongoing challenges. If you read the paper carefully, you might catch the money quote near the end:
<blockquote>"There have been attempts to commercialize volunteer computing by paying participants, directly or via a lottery, and reselling the computing power. These efforts have failed because the potential buyers, such as pharmaceutical companies, are unwilling to have their data on computers outside of their control."</blockquote>
To understand this quote, you have to think about volunteer computing the way the author does: as a method for processing huge computations in bite-size pieces. And he's right that highly-regulated companies with piles of data to crunch may not be able to farm out their calculations to strangers on the Internet.

But all of a sudden, there's another widespread commercial use case for itty bitty pieces of distributed compute time: serverless architectures. Couldn't somebody leverage volunteer computing to provide a free, highly available public compute infrastructure for some of these new-school apps?
<h4>Advantages</h4>
Free compute on an open source platform is a volunteer cloud's biggest selling point for commercial enterprises. You could also argue that a cloud comprising millions of personal devices would be much more highly available than AWS or Azure, which rely on a relatively small number of datacenters, but as we'll see below, this argument is a bit illusory.

In fact, a public volunteer cloud would face even bigger versions of some of volunteer computing's traditional challenges. Let's consider a few potential issues in roughly increasing order of difficulty.
<h4>Issue #1: Incentive</h4>
How do you convince people to run someone else's code on their computers? <a href="http://boinc.berkeley.edu/projects.php">BOINC projects</a> woo users with lofty humanist or humanitarian goals, but there's no altruistic incentive to enable commercial projects. Paying cloud participants a flat rate, or allowing them to bid on jobs, may never be feasible; the existing cloud services mentioned above are simply too cheap an alternative.

But here's where the new paradigm comes in. With so many people running serverless architectures now, a free, public distributed compute service has the ability to <em>directly benefit</em> more people than ever before. So maybe peer-to-peer ethics are the answer. Maybe the rule is, if you submit X requests to the service, you have to accept Y jobs in return. The more compute cycles you pay into the grid, the more you get out.
<h4>Issue #2: Churn</h4>
How do you ensure the availability of a volunteer cloud? Volunteer computing resources, by definition, are voluntary: they can appear or disappear at any time, even in the middle of a calculation. For anybody other than hobbyists to use a service like this, you need at least a few 9's of average uptime.

One solution may be to assign a rank to individual computer nodes based on their availability (how often they are online and accepting jobs) and reliability (what percentage of assigned jobs they complete), with a steep penalty for reliability lapses. In a sufficiently large network, untrustworthy nodes would rarely or never receive requests. In fact, a node might be required to bank a certain amount of "goodwill", demonstrated by time spent online and graceful offline exits, before becoming a full-fledged participant in the grid.
<h4>Issue #3: Security</h4>
Here's where things get really tricky, because both the computer owners and the application developers running code have to worry. The computer owner wants to be sure that code harmful to him doesn't run on his system; the application developer wants to be sure nobody tampers with her code while it's running. BOINC gets around this problem by signing executables at the source and cross-checking results. An application developer using our hypothetical cloud could request a cross-check as well, but only allowing signed executables to run would be a huge barrier to entry, so properly sandboxing the code on the client system would be imperative.
<h4>Issue #4: Centralized Control</h4>
A volunteer cloud is not a peer-to-peer network. Some central authority has to queue job requests, assign them to client computers based on availability and geographic location and deliver responses.  I rate this as the trickiest issue for a couple reasons. First, if the volunteer cloud is going to be free to users, somebody else will have to foot a bill to maintain (or pay for some managed) central infrastructure, and it's not obvious who would have the incentive to do that. Second, if the central control goes down, the grid is down, which eliminates much of the advantage of having widely distributed compute nodes. (If I'm missing an obvious solution to this problem, please yell at me in the comments.)
<h4>Anyway</h4>
The barriers to a publicly available volunteer cloud may seem insurmountable in the current marketplace, just as they have for the last couple of decades. But here's the difference: until the last couple years, the idea would have seemed much more far-fetched, because commercial app backends weren't designed to run as stateless microservices accessed through APIs. The architecture has changed the conversation. Even with the challenges, maybe it's time to give volunteer cloud computing another look.