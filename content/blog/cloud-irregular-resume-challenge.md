+++
title = "The cloud resume challenge"
date = 2020-04-23T09:27:38-05:00
description = "Send me your resume, and I will do my best to help you get a job in the cloud. (Some conditions apply.)"
og_image = "cloud-irregular.png"
+++

<img class="alignnone size-full wp-image-2812" src="/images/cloud-irregular.png" alt="cloud-irregular" />

*Big news: you can [preorder](https://www.amazon.com/Read-Aloud-Cloud-Innocents-Inside/dp/1119677629/ref=sr_1_1?keywords=read+aloud+cloud+innocents+forrest&qid=1585258373&sr=8-1) my first book, The Read Aloud Cloud!*

# The cloud resume challenge

Updated June 2020: Visit the [official Cloud Resume Challenge homepage](https://cloudresumechallenge.dev/) or [join the Discord](https://discord.gg/mr63ws) for rules, FAQ, and further updates.

We're now at that point in quarantine where even [the jobs people thought were safe](https://www.usatoday.com/story/money/2020/04/23/coronavirus-could-cost-state-government-worker-their-jobs/2998645001/) are starting to dry up. Friends and family are telling me: "I've been thinking about changing careers and going into IT. Maybe doing something in the cloud, like you. Where should I start?"

So I'm making an offer right now, before God and the internet and everybody: send me your resume, and I will do my best to help you get a job in the cloud.

Yes, there are some conditions. The first two are easy.

The first condition is that I am not personally hiring anybody at the moment, and cannot force anyone else to hire you. But I have a relatively large network of connections, at least forty percent of whom seem to be tech recruiters, and I will make as much noise as possible to get their attention on you and your resume.

Second condition: the less prior experience you have, the bigger deal I will make out of you. For example, somebody who completes the Cloud Resume Challenge with no prior IT experience or related degree is going to get personal shoutouts on my Twitter and LinkedIn, personalized code reviews, direct intros to hiring managers, etc.

**If you are fortunate enough to have a job in the cloud already, please share this post with #CloudResumeChallenge -- let's get it in the hands of the people who need it.**

OK, now the important conditions.

1. Your resume needs to have the [AWS Cloud Practitioner certification](https://aws.amazon.com/certification/certified-cloud-practitioner/) on it. This is an introductory certification that orients you on the industry-leading AWS cloud -- if you have a more advanced AWS cert, that's fine but not expected. No cheating: include the validation code on the resume. You can sit this exam online for $100 USD. If that cost is a dealbreaker for you, let me know and I'll see if I can help. [Here are some exam prep resources](https://www.selikoff.net/2019/01/20/how-i-recommend-studying-for-the-aws-certified-cloud-practitioner-exam/). 
1. Your resume needs to be written in [HTML](https://developer.mozilla.org/en-US/docs/Web/HTML). Not a Word doc, not a PDF. [Here is an example of what I mean](https://codepen.io/emzarts/pen/OXzmym).
1. Your resume needs to be styled with [CSS](https://www.w3schools.com/css/). No worries if you're not a designer -- neither am I. It doesn't have to be fancy. But we need to see something other than raw HTML when we open the webpage.
1. Your HTML resume should be deployed online as an [Amazon S3 static website](https://docs.aws.amazon.com/AmazonS3/latest/dev/WebsiteHosting.html). Services like Netlify and GitHub Pages are great and I would normally recommend them for personal static site deployments, but they make things a little too abstract for our purposes here. Use S3. 
1. The S3 website URL should use [HTTPS](https://www.cloudflare.com/learning/ssl/what-is-https/) for security. You will need to use [Amazon CloudFront](https://aws.amazon.com/blogs/networking-and-content-delivery/amazon-s3-amazon-cloudfront-a-match-made-in-the-cloud/) to help with this.
1. Point a custom DNS domain name to the CloudFront distribution, so your resume can be accessed at something like `my-c00l-resume-website.com`. You can use [Amazon Route 53](https://aws.amazon.com/route53/) or any other DNS provider for this. A domain name usually costs about ten bucks to register.
1. Your resume webpage should include a visitor counter that displays how many people have accessed the site. You will need to write a bit of [Javascript](https://developer.mozilla.org/en-US/docs/Web/JavaScript) to make this happen. Here is a [helpful tutorial](https://www.codecademy.com/learn/introduction-to-javascript) to get you started in the right direction.
1. The visitor counter will need to retrieve and update its count in a database somewhere. I suggest you use Amazon's [DynamoDB](https://aws.amazon.com/dynamodb/) for this. (Use on-demand pricing for the database and you'll pay essentially nothing, unless you store or retrieve much more data than this project requires.) Here is a [great free course](https://linuxacademy.com/course/dynamo-db-deep-dive/) on DynamoDB.
1. Do not communicate directly with DynamoDB from your Javascript code. Instead, you will need to create an [API](https://medium.com/@perrysetgo/what-exactly-is-an-api-69f36968a41f) that accepts requests from your web app and communicates with the database. I suggest using AWS's API Gateway and Lambda services for this. They will be free or close to free for what we are doing. You will need to write a bit of code in the Lambda function; you could use more Javascript, but it would be better for our purposes to explore Python -- a common language used in back-end programs and scripts -- and its [boto3 library for AWS](https://boto3.amazonaws.com/v1/documentation/api/latest/index.html). Here is a good, free [Python tutorial](https://www.learnpython.org/).
1. You should also include some tests for your Python code. [Here are some resources](https://realpython.com/python-testing/) on writing good Python tests.
1. You should not be configuring your API resources -- the DynamoDB table, the API Gateway, the Lambda function -- manually, by clicking around in the AWS console. Instead, define them in an [AWS Serverless Application Model (SAM) template](https://aws.amazon.com/serverless/sam/) and deploy them using the AWS SAM CLI. This is called "[infrastructure as code](https://www.hashicorp.com/resources/what-is-infrastructure-as-code/)" or IaC. It saves you time in the long run.
1. You do not want to be updating either your back-end API or your front-end website by making calls from your laptop, though. You want them to update automatically whenever you make a change to the code. (This is called [continuous integration and deployment, or CI/CD](https://help.github.com/en/actions/building-and-testing-code-with-continuous-integration/about-continuous-integration).) Create a private [GitHub repository](https://help.github.com/en/github/creating-cloning-and-archiving-repositories/creating-a-new-repository) for your backend code. Set up [GitHub Actions](https://help.github.com/en/actions/getting-started-with-github-actions/about-github-actions) such that when you push an update to your Serverless Application Model template or Python code, your Python tests get run. If the tests pass, the SAM application should get packaged and deployed to AWS.
1. Create a second private GitHub repository for your website code. Create GitHub Actions such that when you push new website code, the S3 bucket automatically gets updated. (You may need to [invalidate your CloudFront cache](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Invalidation.html) in the code as well.) *Important note: DO NOT commit AWS credentials to source control! Bad hats will find them and use them against you!*
1. Finally, in the text of your resume, you should link a short blog post describing some things you learned while working on this project. [Dev.to](https://dev.to) is a great place to publish if you don't have your own blog.

And that's it. When you have done all this, add my GitHub username (`@forrestbrazeal`) as a collaborator on your repositories. If you have indeed met the conditions listed above, I will give you a personalized code review, then make as much noise about you as I can to anybody who will listen (including sharing your awesome blog post!).

Now, before you say it ... obviously, I have no right to tell you to do any of this stuff. You will have to open a large number of browser tabs to figure out the steps. It will take you quite a few long evenings at the kitchen table. You might reasonably conclude that none of what I just suggested is worth the dubious reward of having a random industry professional share your resume with a few thousand people.

But if you give this project a try and realize that you hate it, or you're just not interested, you'll have learned a valuable lesson about whether or not you really want a career in the cloud -- because these are the types of problems that real cloud engineers and developers really work on.

And I believe that if you can, in good faith, complete the Cloud Resume Challenge, you will already have more useful skills than a lot of people who graduate from university computer science programs. Specifically: you will understand something about full-stack software development, version control, infrastructure as code, automation, continuous integration and delivery, cloud services and "serverless", application security, and networking. And you'll have learned by doing, because I didn't give you enough instructions to figure any of this out without going down some late-night rabbit holes. Most importantly, you will have demonstrated the number-one skill in a cloud engineer's toolbox: the ability to learn fast and google well.

Those are skills you can take to a job interview. And I'll do my best to help you get one.

Good luck!

# Links and events

OK the big big news already mentioned up top is that you can pre-order THE READ ALOUD CLOUD from Wiley -- [Amazon now](https://www.amazon.com/Read-Aloud-Cloud-Innocents-Inside/dp/1119677629), other retailers soon. The launch date says September but we are actually hoping to release quite a bit sooner. I'll let you know in this space.

I know the prevailing wisdom in tech right now is that physical books and traditional publishers are a sucker's game. But darn it, I don't know how else a book like this could exist. It has more than a hundred full-page color illustrations! It has maps and schematics and an extended quotation from Percy Bysshe Shelley's "THE CLOUD!" It's all a little much, even to hold in your hand. I can't imagine trying to deal with it on an e-reader.

Also, there's a tiny, stupid, selfish part of me that loves physical books and was really excited about walking into a real bookstore and seeing my real book on the real shelf. So I am sad that quarantine uncertainites make this dream less likely to happen. And yes, I know that this is the dictionary definition of a first-world problem. Randall Munroe was right: our brains have one scale, we just size our problems to fit it.

In other news ...

Yay virtual events!

I'm [speaking](https://virtual.serverlessdays.io/speakers/202004/forrest/) at ServerlessDays Virtual this week, so you have no excuse for not being there.

I'm also hosting a series of webinars at A Cloud Guru. The [first of them](https://register.gotowebinar.com/register/8898498642660017166) is happening on May 6 and I will pretend to know enough about containers to keep up with Chad Schmutzer, who eats them for breakfast.

A few recent writings:

[With VPNs besieged, cloud desktops get their closeup](https://info.acloud.guru/resources/vpn-cloud-desktop-amazon-workspaces) -- Quarantine is literally and figuratively killing the corporate network, will this finally be the end of the VPN and the beginning of sensible zero-trust architectures?

[In praise of S3, the greatest cloud service of all time](https://info.acloud.guru/resources/brazeal-in-praise-of-s3-the-greatest-cloud-service-of-all-time) -- An unabashed fawning over the Eighth Wonder of the World. We're not worthy.

[Why central cloud teams fail](https://info.acloud.guru/resources/why-central-cloud-teams-fail-and-how-to-save-yours) -- This has been gradually dawning on me for about five years, but gelled quickly once I started talking to a bunch of customers at A Cloud Guru. The people who think they need formal cloud training the *least* (that central team of CloudFormation cowboys, you know who you are) are actually the people who need it the *most* -- not for yourselves, but for the rest of the org. Otherwise, you're all going to drown in support requests because the legacy product teams can't keep up with you. Been there, done that, still have the Jira tickets assigned to me.

# Just for fun

I have something INCREDIBLY fun and interactive just about ready to share with you, but its launch has been pushed back a couple of months -- so stay tuned on that. In the meantime, here is a poster-sized image from THE READ ALOUD CLOUD for you to use as you will. It's not exactly a Wardley Map, but it makes a pretty great Twitter background [if I do say so myself](https://twitter.com/forrestbrazeal).

<img class="alignnone size-full wp-image-2812" src="/images/traveling-by-cloud.png" alt="traveling-by-cloud" />

Again, [that pre-order link](https://www.amazon.com/Read-Aloud-Cloud-Innocents-Inside/dp/1119677629). Thanks for taking this journey with me -- lots more traveling by cloud to come.
 
 
 
