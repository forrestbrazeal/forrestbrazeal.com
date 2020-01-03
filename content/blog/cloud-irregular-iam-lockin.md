+++
title = "Cloud Irregular: IAM Is The Real Cloud Lock-In"
date = 2019-02-18T09:27:38-05:00
description = "Forget Lambda and serverless: if you are doing anything at all in AWS besides using it as a fantastically overpriced datacenter, I pretty much guarantee you are deeply locked into IAM."
og_image = "cloud-irregular.png"
+++

<img class="alignnone size-full wp-image-2812" src="/images/cloud-irregular.png" alt="cloud-irregular" />

*In each issue of the "Cloud Irregular" newsletter, I'll try to provide a useful piece of commentary on some tech-related topic. After that I'll let you know about any new stuff I've published, or upcoming talks. Then I'll give you something extremely silly, just to cleanse your palate, and we'll be done.* 

*Sound good? If so, throw in your email at the bottom of this post.*

### IAM is the real cloud lock-in

Here we go again -- that ["Lambda and serverless is the worst form of proprietary lock-in in the history of humanity"](https://www.theregister.co.uk/2017/11/06/coreos_kubernetes_v_world/) article has [resurfaced](https://news.ycombinator.com/item?id=19080875), like a salmon returning to its birthplace, to spawn another generation of fishy, slippery [FUD](https://en.wikipedia.org/wiki/Fear,_uncertainty_and_doubt).

I'm obviously an [advocate](https://aws.amazon.com/developer/community/heroes/forrest-brazeal/) for serverless technologies, and I do not agree with the points attempted by the CoreOS CTO in that article. I've even [taken a stab](https://www.trek10.com/blog/think-faas-podcast-talkin-lock-in/) at refuting them before. Briefly, portability is overrated, and the business advantages of building on serverless functions often dwarf the hypothetical risks associated with doing so. Unless, that is, you are the CTO of an infrastructure business that would be existentially challenged by the rise of serverless, which [checks notes] appears to be not *not* the case with CoreOS.

The thing that I've eventually realized about this "Lambda bad, vendor choice good" argument, though, is that it's [not even wrong](https://en.wikipedia.org/wiki/Not_even_wrong). Debating the potential lock-in, or lack thereof, of Lambda functions is beside the point. By the time you even start that conversation, you're already so far down the rabbit hole of dependence on a very particular managed service that worrying about the portability of a few Javascript functions seems like little more than [bikeshedding](https://en.wikipedia.org/wiki/Law_of_triviality). 

I'm referring, of course, to AWS IAM, which absolutely is the worst form of cloud lock-in that currently exists, at least relative to the zero people who seem to be talking about it. (I except Oracle and their house of contractual horrors from this discussion because to perpetrate cloud lock-in, they'd have to have, you know, [a functioning cloud](https://www.forbes.com/sites/danwoods/2018/10/29/four-common-mistakes-in-understanding-oracles-cloud-troubles/#482e195e1df8).)

To illustrate this point, we have to look no farther than the nine-hundred-pound gorilla of the IAM jungle, which continues to be Microsoft's ActiveDirectory. I'm not sure I even know what ActiveDirectory is anymore, to be honest. Is it a [cloud service](https://azure.microsoft.com/en-us/services/active-directory/)? A ["hybrid identity" provider](https://docs.microsoft.com/en-us/azure/active-directory/hybrid/plan-hybrid-identity-design-considerations-overview)? A flippin' [Linux domain controller](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/login-using-aad)? The answer to all of those questions appears to be "yes, if that is what you want", which is why AD implementations will surely keep an army of Microsoft "IT Pros" busy for a couple more decades.

Here's what ActiveDirectory is not: easy to migrate off of. I've sat in a few meetings where large enterprises attempted to calculate the cost and effort required to move their internal IT infrastructure away from AD. Sweat pops on brows. Entire fiefdoms of IT people dig their trenches and prepare for siege. When AD is handling all your authentication and your domains and your roles and policies and has been doing so for 15 years, dislodging it feels like doing quadruple bypass surgery on your entire organization. No wonder most of those meetings end with sort of a defeated shuffle back to the cubicles. You might say that "just figure out a way to keep things integrated with AD" was the real Group Policy all along.

AWS IAM sees all of that lock-in and says "Hold my [beer](https://github.com/awslabs/simplebeerservice)." At least ActiveDirectory, at its core, is LDAP-compatible. IAM is a completely closed system that undergirds every aspect of the integration between the dozens of services in a typical AWS footprint. Sure, some more traditional network security options exist in the VPC space, but running a bunch of VMs in AWS just so you can control the ingress and egress yourself gets expensive fast. 

The "correct" (and maybe cheaper, and significantly faster) way to use AWS is to glue together services outside the VPC, to use Cognito and Global Accelerator and API Gateway and take advantage of the AWS control plane all the way down to their custom hardware. Forget Lambda and serverless: if you are doing anything at all in AWS besides using it as a fantastically overpriced datacenter, I pretty much guarantee you are deeply locked into IAM.

When I type it all out like that, it looks like a Very Bad Thing, and I do find it bizarre that IAM is not brought up more frequently in people's "proprietary lock-in" screeds. But here's the actual question: *is it* a bad thing to depend so heavily on AWS? 

Maybe! It depends on how much you trust them to a) stay in business; b) not jack up your prices; c) not deprecate services out from under you; and d) provide more value to you in business acceleration than they take away in flexibility. So far, AWS has had a pretty good track record on all those fronts. (There's also the possibility they could [eat your entire company](https://www.inc.com/sonya-mann/aws-startups-conflict.html) with a feature release, but you'll have to work through that risk on your own.)

I mean, I don't hear a lot of companies mourning the decision to go all-in on ActiveDirectory 15-20 years ago. Sure, they're hideously locked into it now. But that software, or suite of server roles, or ramifying cloud behemoth, or whatever we've decided AD is now, enabled a lot of business growth over the years. It was an industry-standard solution that was widely understood and reasonably easy to support. Also, it pretty much worked. Nobody's cursing their past selves for making that choice, even if the outward migration path leads through a blood-soaked minefield.

Like, what was the alternative? Do you really think that if your average enterprise had implemented their own squirrelly domain setup on top of LDAP from scratch back in 2002 or whatever, that things would have gone *better* for them? No, that would have been a terrible idea and it would have ended with everybody getting fired and the new CIO implementing ActiveDirectory anyway. (If this happened to you I want to hear about it, please write me.)

And all of that may turn out to be just as true for AWS IAM. If you've run the risk calculations on the four considerations I mentioned above, and you feel comfortable with the answers, then you should be no more concerned about IAM lock-in than you were 15 years ago about AD lock-in, simple as that. You can get busy building.

If the risks don't work out for you, then throw in your lot with the CoreOS guy and start building bespoke auth layers to support your in-house container orchestration platform. Just be aware that while you are doing that, your competitors will be moving faster and breaking things ... but perhaps a smaller number of things than you and your horrifying custom infrastructure will be breaking.

Meanwhile, to those who maintain that serverless is "the worst form of proprietary lock-in in the history of humanity", I say two things: 1) you don't know the half of it, and 2) ... what's your point?

### Links and events

The [previous edition](https://forrestbrazeal.com/2019/01/16/cloud-irregular-the-creeping-it-apocalypse/) of Cloud Irregular, which addressed the creeping collapse of midlevel IT jobs, went a little bit viral and created a [ton](https://news.ycombinator.com/item?id=18930781) of [interesting](https://www.reddit.com/r/devops/comments/agyo82/the_creeping_it_apocalypse_what_are_your_thoughts/) [discussions](https://soylentnews.org/article.pl?sid=19/01/22/2022257). More importantly, I got dozens of messages from folks at a legitimate career crossroads, trying to figure out their next step. I do not have all the answers (or maybe any), but my offer still stands: if you want to talk through the next phase of your IT career, please [reach out](https://forrestbrazeal.com/#contact). I'll help however I can.

I recently wrote the [official GitLab CI + AWS SAM reference implementation](https://gitlab.com/gitlab-examples/aws-sam), and published [this blog post](https://about.gitlab.com/2019/02/04/multi-account-aws-sam-deployments-with-gitlab-ci/) about it. There's even a sample SAM app -- just run `sam init --location git+https://gitlab.com/gitlab-examples/aws-sam` to get started.

I [chatted](https://www.youtube.com/watch?v=SP1az1FXyyo) with fellow AWS Serverless Hero Marcia Villalba about serverless trends coming out of re:Invent 2018. Check out the video, and subscribe to Marcia's channel while you're at it!

[The Think FaaS podcast is back](https://www.trek10.com/blog/think-faas-serverless-in-production/) with a series featuring another AWS Serverless Hero, Yan Cui. He also has a related [video course](https://www.manning.com/livevideo/production-ready-serverless) out from Manning.

Finally, I had the chance to provide technical review on [this provocative paper on serverless computing](https://rise.cs.berkeley.edu/blog/a-berkeley-view-on-serverless-computing/) from Berkeley's RiseLab. They think serverless will become the "default computing paradigm of the Cloud era", and I don't disagree...

### Just for fun

I'm happy to share that the "FaaS and Furious" tech webcomic, which began four years ago on my blog and has been published for the last year and change by A Cloud Guru, now has an [official webcomic site](https://acloud.guru/comics)! It contains the full archives and will be updated weekly. You are hereby invited to use the comics in your PowerPoint slides, paper your office with them, or deface them in acts of naked cloud-related rage. I'm told they are also great for communicating with IT executives who prefer their "big picture" discussions to consist entirely of, well, big pictures.