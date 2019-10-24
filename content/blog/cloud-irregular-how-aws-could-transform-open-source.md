+++
title = "Hey AWS - it's time to pay OSS developers"
date = 2019-10-23T09:27:38-05:00
description = "The Serverless Application Repository is *so close* to being a game-changer."
+++

<img class="alignnone size-full wp-image-2812" src="/images/cloud-irregular.png" alt="cloud-irregular" />

*In each issue of the "Cloud Irregular" newsletter, I'll try to provide a useful piece of commentary on some tech-related topic. After that I'll let you know about any new stuff I've published, or upcoming talks. Then I'll give you something extremely silly, just to cleanse your palate, and we'll be done.* 

*Sound good? If so, throw in your email at the bottom of this post.*

## AWS could transform open source with a single feature. Why won't they do it?

Dearly beloved, we have gathered here today to pay our respects to the [AWS Serverless Application Repository](https://aws.amazon.com/serverless/serverlessrepo/) -- the [much-ballyhooed](https://www.forbes.com/sites/janakirammsv/2018/02/26/aws-serverless-application-repository-to-boost-adoption-of-function-as-a-service/#401df42b6d5c) service that lets you share snippets of CloudFormation config, or even whole back-end applications, with the world. Ashes to ashes, dust to dust, please form an orderly line to inspect the casket.

Technically, the SAR isn't dead -- in AWS-land, [nothing ever is](https://aws.amazon.com/simpledb/). But it's not exactly showing much life, either. Close to two years after general release, I count [fewer than 600 "apps"](https://serverlessrepo.aws.amazon.com/applications) in the public repository, plus a few more that are hidden by default because they use suspect IAM permissions. Take out hello-world filler and apps contributed by AWS themselves, and the number drops by another 20-30%. Even the most popular apps have been deployed only a couple thousand times (compare with npm's [billion downloads a day](https://www.businesswire.com/news/home/20180912005283/en/npm-Registry-Crosses-Billion-Average-Daily-Downloads)). This is not a thriving ecosystem.

Now, these numbers don't include SAR apps published privately for use within an organization. From what I've seen, a fair number of folks are using SAR as an internal service registry of sorts for shared components. This is valid, cool, etc. But I know the SAR team dreams bigger. As they should. Who wouldn't want to build the npm of the cloud?

Not the AWS community, evidently. And it's not hard to see why when you look at what's really going on. 

Here's the current SAR model: you and I write code for free and publish it on AWS's closed platform. AWS makes money off every deployment of that solution -- which may exist to cover an AWS feature gap in the first place. This is way more asymmetrical than a platform designed for community sharing like Github or npm. It feels to me almost like doing unpaid feature development for AWS. No wonder OSS developers aren’t flocking to the platform.

How do we spin the flywheel to get this service moving? You don't really need me to spell out how to fix the Serverless App Repo: **pay developers**. This is obvious enough that AWS addresses it [in their own FAQ](https://aws.amazon.com/serverless/serverlessrepo/faqs/). They tell you to use the AWS Marketplace if you want to make money off your app. 

But the Marketplace is a closed-source system with a way higher barrier to entry. I shouldn't have to create my own SaaS company to put the AWS-config equivalent of left-pad out in the world. I should just be able to push to GitHub, trigger "sar publish" and call it a day. That's the innovative part of SAR, and something worth keeping. 

So how can we monetize it for creators?

AWS doesn't currently charge for the SAR service itself, just for the resources it deploys. Imagine if they added a fraction of a cent onto that charge that finds its way back to the developer, maybe as a credit on their own AWS bill. While these commissions would be small, it's easy to see them adding up just because AWS is so famously hard to configure. Check out Aleksandar Simovic's ["Deploy to S3" app](https://serverlessrepo.aws.amazon.com/applications/arn:aws:serverlessrepo:us-east-1:375983427419:applications~deploy-to-s3), which does a super boring thing that everyone has lost half a sprint to automating. Half the internet runs on S3. A few million deployments of useful config scraps like that add up fast. Talk about [FinDev](https://aws.amazon.com/blogs/enterprise-strategy/findev-and-serverless-microeconomics-part-1/)...

I do see a couple of potential challenges here. The lesser one is around developer identity: AWS doesn't currently have a canonical user ID that follows developers between accounts. This would be needed to correctly route payments (and to make sure devs can't collect self-payouts by deploying their own applications, of course). The grapevine says AWS is working on a solution for the developer identity problem, though -- I don't expect this to be a major hurdle in the long term.

Now, a trickier problem: since SAR code and config is open-source, one could easily envision consumers saying, "Rather than pay a surcharge, I'll just copy this application, deploy it outside of SAR, and save the fraction of a cent per deployment." That this would probably be a stupid optimization is entirely orthogonal to the number of smarty-pants engineers who would do it, and I speak as an SPE. So you wouldn't want to create a contrary incentive that depresses use of SAR.

I see three solutions to this. Number one, don't create a SAR surcharge (a SARcharge?), just carve a little bit out of AWS's [giant data transfer margin](https://www.lastweekinaws.com/blog/aws-cross-az-data-transfer-costs-more-than-aws-says/) and pay creators .001 cents per deployment or whatever. The second solution is probably a bit more realistic and certainly more interesting: incentivize creators the way sales reps and consulting partners are incentivized, on the impact they create for AWS's top line. If deployments of my app rack up $1 million in AWS spend, I should get half a percent of that credited back to my AWS bill.

And then there's the most likely path of all, because it's one Amazon is already taking. Remember when I said there were no SAR apps with more than a couple thousand deployments? That's almost true. There's a single SAR app, one solitary outlier, that's been deployed nearly fifty thousand times. It's [an app that aids in creating Alexa skills](https://serverlessrepo.aws.amazon.com/applications/arn:aws:serverlessrepo:us-east-1:173334852312:applications~alexa-skills-kit-nodejs-factskill). Now *there's* a platform with healthy adoption - [more than a hundred thousand Alexa skills have been published](https://developer.amazon.com/blogs/alexa/post/c2d062ff-17b3-47f6-b256-f12c7e20f594/congratulations-alexa-skill-builders-100-000-skills-and-counting), and some developers earn [as much as ten grand a month](https://www.cnbc.com/2018/04/12/student-makes-10000-a-month-inventing-skills-for-amazon-alexa.html) through the [Alexa Developer Rewards program](https://developer.amazon.com/en-US/alexa/alexa-skills-kit/learn/build-a-business/rewards). The rewards program is more opaque than the bald forms of revenue sharing I suggested above -- it sounds like Amazon just picks high-performing skills and sends their creators a check -- but it's obviously working as an incentive. 

I mean, you want to talk adoption? Let people create apps for AWS on commission, and all of a sudden you have an EXPLOSION of activity on the platform. Developers flock to write apps, which means developers become hyper-aware of what the SAR can do and use it in their own corporate applications, creating a virtuous cycle. You also keep the OSS good vibes flowing by letting the config be open-source. You'd need a higher-quality, Alexa-style rating system so the good stuff bubbles to the top, and probably a bit of editorial oversight, but this seems all kinds of doable once you get past that whole icky idea of, ya know, paying people for their work. 

This leaves only one question: why isn't AWS doing this, given that they've clearly thought about the problem a lot more than I have? I don't know. I wonder if it might just be too radical. As far as I know, this would be something pretty new in the open-source community. It doesn't align with any of the standard ways of making OSS work pay, like adding enterprise features or taking on a sponsor. 

But hey, Alexa didn't start out by paying skill builders either. It only added the rewards program after a frustrated creator [emailed Jeff Bezos](https://www.cnbc.com/2018/04/12/student-makes-10000-a-month-inventing-skills-for-amazon-alexa.html). And if AWS wants the Serverless App Repo to be a world-beater, they might have to start giving back a little bit too.

Or I might be missing something obvious! So feel free to yell at me in the comments.


## Links and events

- I started thinking more about the Serverless App Repo after I did [this writeup](https://www.trek10.com/blog/examining-aws-serverless-apps/) on a recent [open-source release](https://github.com/awslabs/realworld-serverless-application) from the SAR team that outlines their internal standards for code and config. My TL;DR: no magic, just thorough execution.

- Thanks to all who helped make this month's ServerlessConf [a huge success](https://read.acloud.guru/the-state-of-serverless-circa-10-2019-2bfd0e605700)! If you couldn't make it, I [previewed GIA's talk](https://www.trek10.com/blog/think-faas-serverless-in-the-cloud-with-diamonds/) on the Think FaaS podcast.  

- I'm in the process of moving to the Charlotte area. If you hail from there, give me a shout -- I'd love to grab coffee with you.

My story ["Empathy Bee"](https://www.diabolicalplots.com/dp-fiction-55a-empathy-bee-by-forrest-brazeal/), about what happens when grade-school academic competitions evolve into the Turing Test, is out and has a couple of [nice](https://quicksipreviews.blogspot.com/2019/09/quick-sips-diabolical-plots-55.html) [reviews](https://www.tangentonline.com/e-market-monthly-reviewsmenu-265/279-diabolical-plots/4284-diabolical-plots-55-september-2019).

## Just for fun

It's been a busy few weeks, but I did make up some ["Tom Swifties"](https://en.wikipedia.org/wiki/Tom_Swifty) for you:

- "Someone has stolen the glass out of these windows," said Tom painstakingly.
- "We're lost!" cried Tom unfoundedly.
- "Die, evil clone!" said Tom, beside himself with rage.
- "We used to have such a 'can-do' spirit around here," Tom said candidly.
- "I guess we'll just wait four hours for a table, then," said Tom, without any reservations at all.