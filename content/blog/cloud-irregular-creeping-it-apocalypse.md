+++
title = "Cloud Irregular: The Creeping IT Apocalypse"
date = 2019-01-16T09:27:38-05:00
description = "I've been saying for awhile now that we're getting close to a crisis point in the IT world. The mid-tier IT worker is in imminent danger of being automated out of existence, and just like with the vanished factory jobs of the last 30 years, nobody wants to admit it's happening until it's too late."
+++

<img class="alignnone size-full wp-image-2812" src="/images/cloud-irregular.png" alt="cloud-irregular" />

*So, I'm trying a thing. A newsletter thing. I'm not sure if this will work, or how often I will do it. Probably not more frequently than once a month.*

*In each issue of "Cloud Irregular", I'll try to provide a useful piece of commentary on some tech-related topic. After that I'll let you know about any new stuff I've published, or upcoming talks. Then I'll give you something extremely silly, just to cleanse your palate, and we'll be done.* 

*Sound good? If so, throw in your email at the bottom of this post.*

[HackerNews comments](https://news.ycombinator.com/item?id=18930781)

### The creeping IT apocalypse

So apparently [AWS is working on a clandestine low-code/no-code product codenamed "AWS for Everyone"](https://www.geekwire.com/2019/aws-everyone-new-clues-emerge-amazons-secretive-low-code-no-code-project/). It's useless to speculate on this without concrete info (though that didn't stop Geekwire), but hopefully this isn't just another half-baked attempt to simplify the process of application development past all recognition. An awful lot of smart people have been trying to make graphical interfaces to help non-programmers code since - what, pre-Visual Basic? - and those projects always seem to get bogged down by a) fundamental limitations of usefulness or b) horrifying snarls of technical debt, or c) both of the above.

No, the real trend to watch here is not that the cloud providers are making it easier for non-technical people to code (although they are), but that they are *straight-up reducing the number of people required to deliver technical solutions.*

I've been saying for awhile now that we're getting close to a crisis point in the IT world. The mid-tier IT worker is in imminent danger of being automated out of existence, and just like with the vanished factory jobs of the last 30 years, nobody wants to admit it's happening until it's too late.

The IT automation apocalypse will move slowly (by tech standards), so it is flying under the radar. Unlike with the collapse of American manufacturing, we won't get breathless feature articles and political posturing. A shuttered factory and 700 unemployed workers are concrete, easily visible; a decaying Rust Belt town makes an arresting photo spread. But how do you build a narrative around midlevel IT engineers let go in twos and threes from jobs that even they probably can't quite describe? 

Moreover, the first people to feel the pain will not be the highly-paid, conference-trotting Very Important Programmers in job-rich tech hubs. They will be anonymous Windows administrators and point-and-click DBAs and "senior application developers" who munge JSON in C#. Normal people making comfortable money, fifty to eighty thousand dollars a year in ordinary places like Omaha and Memphis and Santa Fe.

Whether they and their bosses realize it yet or not, all these people are doing work that is not unique or proprietary to their business. 

Cloud scale has enabled AWS and Azure and Google to identify patterns that are common across customers and industries. Look at Google's suite of natural language processing services, or AWS's steady creep up the stack with development automation services like AppSync and Amplify. Once the providers build it, nobody else has to. I mean, you could, but the opportunity cost gets harder and harder to justify. 

Again, it's not that these tools have democratized IT or software development, exactly. Rather, they've enabled technical work to be done by a vastly smaller absolute number of people. (This is also the primary selling point of "serverless" computing, by the way, though it's not quite polite to say so.)

Sure, the cloud services are expensive. So are the robots used in warehouses and on factory floors. But they're less expensive than a bunch of humans with health benefits. And the average mid-sized financial services company or industrial shop is not doing cutting edge work that requires a lot of groundbreaking programmers anyway. IT is overhead, for them. Way better to pay Azure for a DevOps service than to hire a dedicated DevOps engineer.

Companies still need tech-savvy people, of course, just like factories need people on the floor. But instead of five backend developers and three ops people and a DBA to keep the lights on for your line-of-business app, now you maybe need two people total. Those two people make great money, they're plenty busy, and they have lots of technical challenges to solve. But they're not managing a database cluster or babysitting a build server or writing giant stored procedures to do some non-differentiated task, like OCR on insurance forms. The cloud provider can do that (and is adding more capabilities all the time).

This is not a zero-sum game of outsourcing, like people feared 15 years ago. These jobs have been distributed via the economy of scale to a small number of domain specialists working for service providers. They're disappearing into the cloud, and they're never coming back, and too many of my fellow tech workers aren't prepared for what's about to happen.

I've spent my career in tech, almost a decade at this point, running about a step-and-a-half ahead of the automation reaper. I was an IT field engineer maintaining server blades until they turned into EC2 instances. I was a DevOps DBA building SQL Server clusters on top of AWS EC2; then RDS got better and that wasn't a good use of manpower anymore. I was a CI/CD tool builder for internal development teams - cloud providers and service companies now make better versions of those tools available at cloud scale. Just about every role I've had in tech has become an inefficiency, sometimes due in part to my own efforts. The work has been automated out of existence, and I have moved on. 

So how do you know if your job is going to disappear into the cloud? You don't really need me to tell you. You already feel it in your bones. Repetition is a sure warning sign. If you're building the same integrations, patching the same servers over and over again every day, congratulations -- you've already become a robot. It's only a matter of time before a small shell script makes it official.

The solution is simple, but not easy: you simply must keep moving. If you don't know how to code, learn - like planting a tree, the best time to start was ten years ago, but the second best time is now. If your technical competence is ten years out of date, don't cling to your hard-won kingdom of decaying knowledge and sabotage any attempts at change: get out and pick up a certification, attend a meetup, something. Anything. At the end of the day, we're all self-taught engineers.

Otherwise, I'll tell you what will happen. The economy will take a small dip, or your department will get re-orged, and you will lose that job as an operations engineer on a legacy SaaS product. You'll look around for a similar job in your area and discover that nobody is hiring people anymore whose skill set is delivering a worse version of what AWS's engineers can do for a fraction of the cost. And by then you won't have the luxury of time to level up your skills.

Please don't be that person. If you need some advice on where to take your career, feel free to reach out -- I'll offer any help I can. Because you can definitely stay ahead of the IT automation apocalypse. It just requires serious personal effort. 

That's how I know this is gonna get real bad.

### Links and Events

If you're in the Raleigh, NC area on January 24th, I hope you'll join me at the [Triangle Serverless Meetup](https://www.meetup.com/TriangleServerless/events/257885233/), where I'll be speaking on serverless data patterns and telling you about the most embarrassing moment of my IT career. If you're not in Raleigh, I believe the atrocities will be streamed on Triangle's YouTube and Twitch.

I'll also be making a trip to the Bay Area March 18-20th for a couple of speaking engagements. I'll have some free time, so please give me a shout if you're from around there and want to meet up and talk.

I [interviewed](https://read.acloud.guru/how-serverless-is-breaking-down-barriers-in-tech-9b32d7fbf9e7) Stackery's Farrah Campbell for A Cloud Guru. She has a provocative perspective on how the serverless community is eliminating gatekeepers and democratizing tech. Worth a read...

I spent a ton of time over the year-end holiday digging deep on [relational modeling in DynamoDB](https://www.trek10.com/blog/dynamodb-single-table-relational-modeling/). Code is included.

In non-tech writing news, I had a couple of fictional stories published this month: [World War 2.8.41 Release Notes](https://dailysciencefiction.com/science-fiction/future-societies/forrest-brazeal/world-war-2841-release-notes) at Daily Science Fiction, and [Death's Head in B Dorm](https://menacinghedge.com/winter2019/entry-brazeal.php) at Menacing Hedge.

### Just For Fun
*In each newsletter, I'll try to put something completely silly and useless, just in case you're afraid of getting too much value out of this.*

Today: Disney Foxes, Ranked By Wokeness

5. Bre'r Fox from *Song of the South*. A racist fox. Not woke.
4. The fox from the fox hunt in *Mary Poppins*. An Irish revolutionary fox. Awake, but unwoke.
3. Tod from *The Fox and the Hound*. A very boring fox, not a political fox at all. Well, I guess he is a bit of a gun control or animal rights fox. Slightly woke.
2. Robin Hood from *Robin Hood*. A democratic socialist fox. Likely favors a 100% marginal tax rate on the rich. Woke.
1. Nick Wilde from *Zootopia*. Sort of the opposite of Bre'r Fox. An extremely woke fox. Perhaps - dare I say - overly woke, for a fox. What am I saying, a fox can't be too woke. Our winner!

(If the words "fox" and "woke" look meaningless to you now, my work here is done!)