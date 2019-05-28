+++
title = "Cloud Irregular: Does Anyone Know How Your System Works?"
date = 2019-05-28T09:27:38-05:00
description = "How do you get into a position where not a single person at your company, even the architects, can adequately describe your own software?"
draft = false
+++

<img class="alignnone size-full wp-image-2812" src="/images/cloud-irregular.png" alt="cloud-irregular" />

*In each issue of the "Cloud Irregular" newsletter, I'll try to provide a useful piece of commentary on some tech-related topic. After that I'll let you know about any new stuff I've published, or upcoming talks. Then I'll give you something extremely silly, just to cleanse your palate, and we'll be done.* 

*Sound good? If so, throw in your email at the bottom of this post.*

### Does Anyone Know How Your System Works?

Let's suppose you, like me, are a tech consultant, and you have just walked into a large enterprise to help them refactor a big ol' legacy software application. (A BOLSA? Can we make that a thing?)

Naturally your first question is something like "Can I see a diagram of the existing system?" Hard to refactor if you don't know what you're dealing with.

But instead of sending you a wiki link to the specs of the BOLSA, the CTO or software development director or or whoever brought you in gets a weird look on their face and says: "We'll need to talk to Chris."

Chris has been around for fifteen years and is a human repository of architectural knowledge. Or so the director believes. But when you get Chris in the room it turns out that he only knows about the parts of the app that are fifteen years old, not the dozens of new pieces that have been bolted on since then. He suggests talking to Martha. But Martha has moved into a new role and isn't as close to the code as she used to be.

So the conference room gradually fills up with people, and the whiteboard gradually fills up with scribbles, and eventually you get some sort of illegible spaghetti diagram that the committee agrees might, maybe, at some level, describe the system as far as they can remember. Possibly. Who's to say? Not anyone who works here, apparently. Let's take a few low-res phone pictures of this whiteboard and start refactoring!

I run into this sort of situation all the time, and it hasn't quite stopped blowing my mind. Like, how do you get into a position where not a single person at your company, even the "architects", can adequately describe your own software? Is it a misguided focus on segregation of responsibilities? A culture of knowledge-hoarding that deliberately avoids documentation? Not enough functional tests? A lack of product ownership? Or, most likely, is it all those factors snowballing together over years into a gigantic blob of fear and inertia that nobody dares to touch anymore?

Anyhow, I appreciated Joe Emison's [recent Twitter thread](https://twitter.com/JoeEmison/status/1130084973074165763) on this subject. His thesis boils down to this:

> Organizations are in one of two phases of software development leadership: either at least one person understands how everything works at the lowest architectural/data-flow level, or no one does.

Which on one level is a truism -- unless you are building Schrodinger's Cloud, obviously the system is either understood or it is not, no in-between superpositions. 

Joe's point, though, is that the organizations that *can't* explain their BOLSAs (yep, this acronym is definitely a thing now) are in deep danger -- in large part because, the less confident you are in what your app does, the more likely you are to avoid changing anything. And though maintaining the status quo may work superficially well for awhile, eventually your old dependencies will stop being supported, or you'll be spending too much money on legacy vendors. Even worse, you won't be able to deliver features as quickly, or with the same capabilities, as your more nimble competitors. Oh yeah, and stuff will break all the time. In production. Really badly. And it will get harder and harder to fix without breaking something else you don't understand.

So, when the impetus for change gets too great to ignore, what must our guardians of the black-box BOLSA do? They call in consultants to do the innovative work of redesigning their application. 

This used to puzzle me -- and again, I work in consulting -- because wouldn't you rather have your own team do that kind of work? After all, they understand your business domain better than anyone else. Sure, get advice from a consultant, but own the new product yourself. It's more fun, it's better for morale, and eventually you'll need to develop that expertise in-house anyway. Meanwhile, have the consultants or contractors or whatever take over the maintenance tasks on your legacy system. That should be basically undifferentiated work by now.

BUT -- and here's the really treacherous part -- if you can't explain how your system works, you can't hand it over to anyone else. You're locked into sort of a reverse [reality distortion field](https://en.wikipedia.org/wiki/Reality_distortion_field) where you don't believe you can accomplish *anything* worthwhile, and over time you the things you do get further and further divorced from useful work. This is how you get whole teams of IT professionals who can only describe what they do by saying ["We keep the lights on"](https://faasandfurious.com/92). Once you define yourself that way, you have lost the capacity to innovate as an organization, and you'll struggle to attract new talent as well. No matter how many consultants you bring in, I don't know of anything short of major upheaval that can turn things around.

If you are stuck on a team that is stuck in this situation, please accept my empathy. I know it sucks, and there is no easy solution. The good news, though, is that the nobody-understands-how-things-work problem, perhaps uniquely among the dysfunctions of large organizations, can be powerfully attacked at the lowest level of the team. *You* can become the one who knows how things work. All it takes is an awful lot of awkward questions.

If you sense that nobody has a full picture of what your system does, then, the best advice I have is to become a sort of evolutionary biologist. Dig around  for the mutations and genetic characteristics that cause your app to be expressed in its current form. Start asking empirical questions, and keep looking until you find answers. For example, given some asynchronous workflow process with zero documentation:

- Why does this workflow exist?
- Who can initiate this workflow, and when?
- What are the different states an item can pass through during this workflow?
- How do we know those are the only possible states?
- Where do failure states go?

And then, of course, write the answers down and keep them up to date. Don't wait for a promised "documentation sprint" -- when has that ever actually happened? I guarantee that, on a team where nobody understands the system, there is enough dead time that you could start to assemble this knowledge between your other tasks. Don't assume the business logic is unknowable. It's code, after all. Let's hope it's mostly deterministic. You, as a professional who cares what happens, can figure it out. 

And when you know what is happening, then you have the power to effect positive change. I hope you will. 

### Links and Events

- My previous Cloud Irregular piece on [IT jobs in danger](https://forrestbrazeal.com/2019/01/16/cloud-irregular-the-creeping-it-apocalypse/) continues to make people uncomfortable, most recently [in the digital pages of CIO magazine](https://www.cio.com/article/3397111/it-job-apocalypse-rise-of-the-machines.html).

- ServerlessConf is [coming up again](https://nyc2019.serverlessconf.io/) in October! I'm co-chairing this year, and would love to see your [talk submission](https://serverlessconf2019.typeform.com/to/eopTfq) before the end-of-May deadline. We are still accepting 5-minute lightning talks from folks who are newer to speaking and/or serverless.

- I'll be at the AWS Chicago Summit this week speaking about CI/CD design for large enterprises. There will be Avengers memes. [Register for free](https://www.cvent.com/events/aws-summit-chicago/registration-21a28f888de849188ab183411ec289d4.aspx?fqp=true)! If you can't make it, no worries -- I also put up a [companion blog post](https://www.trek10.com/blog/pragmatic-enterprise-cicd/).

- I'll be [speaking](https://www.dashcon.io/talks/when-bad-architectures-happen-to-good-people/) at DashCon July 17 on serverless migrations -- let me know if you'll be in NYC and would like to meet up that week.

- I recently wrote a [love letter](https://aws.amazon.com/blogs/aws/building-serverless-pipelines-with-amazon-cloudwatch-events/) to CloudWatch Events, the best-kept secret in serverless event processing, for the AWS blog.

- In non-tech writing, I have two science fiction stories out this month, both concerned with the uneasy influence of AI on the near future. You can read "Under The Hat" at [Constellary Tales](http://constellary.com/blog-post/fiction-under-the-hat/) and listen to "The Girl of The Golden City" on the Hugo Award-winning podcast [StarShipSofa](http://www.starshipsofa.com/blog/2019/05/08/starshipsofa-no-587-forrest-brazeal/).

### Just For Fun

Occasionally I'll put up a random question on Twitter to get reactions from the cloud community. Here are a couple of fun recent ones -- the replies are always good for a chuckle.

- [What is a fact about AWS that you are sad that you know?](https://twitter.com/forrestbrazeal/status/1126161569988206594)
- [How do you explain your job to non-technical friends and family?](https://twitter.com/forrestbrazeal/status/1131256785451540480)