+++
date = "2017-04-05T10:49:34-05:00"
title = "Building a Serverless Blog"
draft = false
image = "Image-05.png"
categories = ["Building a Serverless Blog"]
tags = ["aws", "lambda", "cloudfront", "api gateway", "route53", "s3", "cloudformation", "github"]
+++

We're really excited to share with you what we've been working on. Our desire is to give you an opportunity to learn how to implement some serverless technologies. After going through a starter course such as `Serverless Concepts` or `Lambda Deep Dive` on [Serverless Academy](http://www.serverlessacademy.com/), implementing a blog is a great way to apply some of your new skills. Watch as we introduce this series on "Building a Serverless Blog."

<iframe width="560" height="315" src="https://www.youtube.com/embed/uK5E7TFIAA4" frameborder="0" allowfullscreen></iframe>

## What are we trying to accomplish?

> We want you to be able to create and deploy your own serverless blogs just as easily as we did, hopefully even easier. We've created a ready-to-go stack that you can deploy to AWS.

Currently, this will allow people to store their content in GitHub and our stack will generate the resulting website in S3 and CloudFront so you can take advantage of extremely fast speeds and extremely low costs.

## How are we going to go about accomplishing this?

> AWS CloudFormation allows us to specify what AWS services we will use and how they are connected. The CloudFormation template will deploy an AWS Lambda handler that will generate a new post when it is triggered by an API Gateway endpoint. GitHub triggers the API Gateway endpoint when new content is added. We have an S3 bucket that stores the generated website. We use CloudFront to pick up changes in S3 and caches the website artifacts in a Content Delivery Network which makes access to the content extremely fast. Finally, we have Route53 set up to connect a domain name to your CloudFront distribution.

## What challenges are we running into?

> A little background, we're basing this on the JAMstack: JavaScript, APIs, and Markup. We're trying to ship atomic deploys, which allows us to deploy updates in an all-or-nothing fashion. We wanted to change CloudFront paths to point to a new atomic version of the blog, but CloudFront usually expects the "Origin Path" to stay the same. If you change the "Origin", even if it's in the same S3 bucket, CloudFront takes a long time to update the distribution.

## What are we going to do to mitigate the challenges?

> S3 has versioning capabilities. If you turn on versioning in an S3 bucket, changes get stored under a unique key where it can be accessed later on. We can reference those version keys to handle a roll-back scenario. This will let us take advantage of the less-than-a-minute content updates in CloudFront.

## Wrapping up

I hope you'll join us as we continue this series, jumping into the details of implementing our serverless blog solution. We would love your feedback! Don't hesitate to let us know what kind of projects you're working on and what kind of content you'd love to see here! Here are the repos we're publishing in this effort:

* [Serverless Academy Blog Content](https://github.com/linuxacademy/serverless-blog)
* [Serverless Academy Blog Stack](https://github.com/linuxacademy/serverless-blog-ops)
* Coming Soon: Serverless Academy Blog Theme