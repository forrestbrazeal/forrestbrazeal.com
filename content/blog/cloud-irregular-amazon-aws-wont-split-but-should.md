+++
title = "Cloud Irregular: Amazon won't spin off AWS, and that's too bad for AWS"
date = 2019-07-24T09:27:38-05:00
description = "Many customers are not using AWS the way it's designed to be used, as a holistic, deeply integrated platform, and the looming shadow of Amazon is the reason why."
og_image = "cloud-irregular.png"
+++

<img class="alignnone size-full wp-image-2812" src="/images/cloud-irregular.png" alt="cloud-irregular" />

*In each issue of the "Cloud Irregular" newsletter, I'll try to provide a useful piece of commentary on some tech-related topic. After that I'll let you know about any new stuff I've published, or upcoming talks. Then I'll give you something extremely silly, just to cleanse your palate, and we'll be done.* 

*Sound good? If so, throw in your email at the bottom of this post.*

### Amazon won't spin off AWS, and that's too bad for AWS

First let's make one thing perfectly clear: Amazon and AWS are not splitting up. AWS CEO Andy Jassy has [repeatedly avowed](https://www.cnbc.com/2019/06/11/aws-ceo-we-would-follow-the-law-if-regulators-demand-amazon-spin-out.html) that the only way AWS will ever leave the mothership is if federal regulators feed him feet first into a wood chipper.

On one level, this makes sense. AWS still generates something like [half of Amazon's operating income](https://www.cnbc.com/2019/04/25/aws-earnings-q1-2019.html). Amazon can wrap its tentacles around every facet of the consumer experience because of the big dollars rolling in from its cloud business. AWS's dominance fuels big AMZN share prices and funds new innovation, etc, etc. We get it: Amazon will let go of AWS when you pry it from [Jeff Bezos' weirdly fearsome biceps](https://www.telegraph.co.uk/technology/2017/07/28/biceps-billionaire-doesnt-matter-jeff-bezos-not-worlds-richest/).

That's what AWS does for Amazon. But what does Amazon do for AWS? Increasingly, as far as I can tell, bad things.

Let's lay aside for a moment the whole regulatory question, whether AWS and Amazon will someday be trust-busted and broken up by force. The 2020 presidential candidates can [hash that out](https://www.nytimes.com/2019/03/08/us/politics/elizabeth-warren-amazon.html). Amazon is causing other political problems for AWS already.

Look, Amazon is huge; it's owned by the richest man in the world, who increasingly owns [other things](https://www.marketwatch.com/story/its-not-just-amazon-and-whole-foods-heres-jeff-bezos-enormous-empire-in-one-chart-2017-06-21) as well. That means bad vibes from some other venture can poison AWS deals.

Remember [JEDI](https://defensesystems.com/articles/2018/07/26/jedi-hits-the-street.aspx), that $10 billion single-vendor Department of Defense contract AWS has been craving for what seems like years? Apparently the whole bid process [is now on hold](https://www.theregister.co.uk/2019/07/18/jedi_cloud_donald_trump/), not because of anything AWS did wrong, but because, well, Jeff Bezos also owns the Washington Post, which Donald Trump does not appreciate, and so it's all a mess. (Also, I love that Oracle has been apparently fomenting all this strife via Machiavellian backstage dealings, which I guess is Oracle's whole brand now.)

There's also the issue of AWS selling technology, directly or indirectly, to government agencies and police forces who use it for dubious purposes like [facial recognition](https://www.theverge.com/2018/6/22/17492106/amazon-ice-facial-recognition-internal-letter-protest). Werner Vogels' recent AWS Summit keynote address suffered [no fewer than five interruptions](https://www.wsj.com/articles/protesters-disrupt-amazon-event-over-its-ties-with-ice-11562882825) from protesters angry that AWS services support the operations of US Immigrations and Customs Enforcement (ICE). 

While this might seem to be AWS's problem, I guarantee that the name recognition of Amazon among everyday consumers drives a lot of the public outrage. (That's why you often see Amazon-dot-com protests misdirected at AWS events. I've seen protesters interrupt an AWS summit with signs and shouts about Amazon warehouse conditions. The lines are blurry and it's no wonder people get confused.) 

Take Amazon out of the equation, and for better or worse the scrutiny of AWS goes down. To put it another way, there's like a 50% chance that anyone running a big Oracle cluster at this point is a supervillain, but you don't see Oracle getting protested.

Leaving aside the public sector issues, we have Gartner's new magic quadrant report (I know, stay with me) [reminding us](https://www.crn.com.au/news/aws-azure-and-google-top-gartners-iaas-magic-quadrant-528501) that many companies, particularly retailers, are now eschewing AWS out of an existential fear that they are funneling dollars indirectly to their biggest competitor. [Walmart, Target, and Kroger](https://www.geekwire.com/2018/least-one-retailer-online-outlet-zulily-still-willing-sign-amazon-web-services/) are all notorious for their no-AWS tech policies, with Amazon's 2017 acquisition of Whole Foods apparently the last straw.

This is bad enough, but survivable: AWS can and does thrive without Walmart's business. But Walmart actually takes their policy a lot further: they now [require their tech partners to stay off AWS as well](https://www.techrepublic.com/article/walmart-forces-tech-partners-to-leave-aws-following-whole-foods-acquisition/). These retailers (and [healthcare providers](https://www.digitalcommerce360.com/2019/06/09/nearly-50-of-health-systems-see-amazon-as-a-threat/), and [car companies](https://www.cnbc.com/2019/03/16/why-volkswagen-chose-microsoft-azure-over-aws.html), and whatever industry Amazon disrupts next) are fighting for their lives, and they'll play every card they hold to swing their sizable partner ecosystems toward Microsoft or Google. The competing cloud platforms, for their part, are perfectly willing to push this narrative, [swearing up and down](https://www.cnbc.com/2019/02/12/microsoft-google-cloud-pitch-vs-aws-we-wont-compete-with-you.html) that they won't "compete with partners".

So here's the reality on the ground. I just got back from [speaking at Dash](https://www.dashcon.io/talks/when-bad-architectures-happen-to-good-people/), Datadog's New York conference focused on next-generation ops and infrastructure (though mostly, let's be real, focused on Datadog). I took an informal survey of tech leads there, people building SaaS platforms for everything from real estate to nonprofits to IoT. Not things Amazon competes with directly. But nearly all of these vendors have, or want to believe that they will land, the kind of big customer that may have a "no AWS" policy. 

So with few exceptions, they are hedging their bets. They build on containers in a misplaced belief that will make quick migrations easier, they architect dubious "multi-cloud" workloads ... the point is, they're not using AWS the way it's designed to be used, as a holistic, deeply integrated platform, and the looming shadow of Amazon is the reason why. 

Of course, the whole "I can't go all-in on AWS because some of my own customers might distrust AWS, because they in turn fear Amazon" thing is such a delightfully screwy reason for making suboptimal tech choices. It reminds me of the old fundamentalist idea of [secondary separation](https://www.patheos.com/blogs/religionnow/2017/10/secondary-separation-islam/), where you shun an innocent person because they've insufficiently disassociated themselves from heretics. 

The problem with secondary separation, as the fundamentalists discovered, is that it has no logical stopping point. What degree of separation is enough? How many layers of vendors must you purge before you can be sure you're not bankrolling heresy, or Amazon? The whole conversation is faintly dumb, but it's *happening*, and that's a problem for AWS as much as for the engineering teams who have to work around them.

So let's recap the reasons Amazon may be harming AWS:

- Amazon's name recognition creates a target on AWS's back when they want to work in politically-charged areas

- Jeff Bezos's other business ventures and feud with the president jeopardize AWS's government contracts

- Companies that compete with Amazon don't want to use AWS services

- Companies that want to attract business from Amazon competitors avoid AWS, or use it less fully

None of these things are that bad on their own, at least not yet. But they all keep AWS from being the best, most juggernaut-y version of itself. They keep AWS's services from competing on equal footing in the marketplace. And that's a shame, because the tech itself is often pretty great.

It's worth noting that [some smart people](https://www.businessinsider.com/scott-galloway-amazon-will-spin-off-amazon-web-services-ignition-2018-12) think Amazon will eventually have to spin off AWS just because AWS would be so valuable and do so well in the market as a "pure cloud" player. But AWS is a victim of its own success. It's not going anywhere because Amazon depends on it. And as Amazon expands to threaten more industries, AWS may paradoxically become less successful. It's a weird bind.

At any rate, unless something big changes in the regulatory landscape, Amazon and AWS will probably remain joined at the hip. And I'll keep having frustrating conversations with more and more clients about why they can't use the best cloud services on the market.

*Disclaimer: I work for an AWS consulting partner, but I own no $AMZN stock and have no direct interest in what Amazon does with AWS.*

### Links and events

- ServerlessConf is [coming up again](https://nyc2019.serverlessconf.io/) in October! Check out the [agenda](https://nyc2019.serverlessconf.io/agenda.html) and make plans to join me in NYC for the hottest conference in the cloud. There's a great balance of speakers, both serverless "old-timers" and new faces, and a heavy concentration of hands-on use case stories. Should be a lot of fun.

- Check out this [recording](https://www.youtube.com/watch?v=M215idpHA6E) of a recent webinar I did with AWS and Epsagon on modern application development. If the word "webinar" makes your eyes go glassy, call it a "parley" or a "confabulation". There's a lot of good material in there.

- I wrote up [a few tips](https://dev.to/trek10inc/ci-cd-aws-and-serverless-5-tips-i-learned-the-hard-way-223p) learned the hard way about serverless CI/CD on AWS.

- Jared Short and I are trying an experiment with [serverless.help](https://serverless.help) -- submit your serverless question, we'll answer it and add it to a public repository so others can benefit. It's a conscious effort to get more shared knowledge out of Slack groups and back onto the public web. You can also add your own questions and answers directly to the [repo](https://github.com/trek10inc/serverless.help).

My brain-augmentation story ["The Mark"](https://www.mysteriononline.com/2019/06/the-mark.html) is free to read this month at Mysterion.

### Just for fun

Five completely useless books that I greatly enjoy:

[How I Became A Famous Novelist](https://www.powells.com/book/-9780802170606) by Steve Hely

[The Decline and Fall of Practically Everybody](https://www.powells.com/book/-9780879235147) by Will Cuppy

[Versus](https://www.powells.com/book/-2221141745616) by Ogden Nash

[The Prehistory of the Far Side](https://www.powells.com/book/-9780836218510) by Gary Larson

[The Prisoner of Zenda](https://www.powells.com/book/-9781853261138) by Anthony Hope
