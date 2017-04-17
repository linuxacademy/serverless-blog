+++
date = "2017-04-17T10:51:41-05:00"
title = "Choose the Right Tools for the Job"
draft = true
categories = ["Building a Serverless Blog"]
tags = ["hugo", "jamstack", "lambda"]
+++

_This post is a follow-up to the [Building a Serverless Blog](../building-a-blog/), start there if you'd like some context._

Are you familiar with the [JAMstack](https://jamstack.org/)? It's defined as a:

> Modern web development architecture based on client-side JavaScript, reusable APIs, and prebuilt Markup.

The JAMstack represents some new modern [best practices](https://jamstack.org/best-practices/):

* Entire Project on a CDN
* Everything Lives in Git
* Modern Build Tools
* Automated Builds
* Atomic Deploys
* Instant Cache Invalidation

Traditionally, you would use tools like Wordpress to deliver a blog to the public. Wordpress works for a lot of organizations, but not everyone needs all of the complexity that comes with Wordpress.

For the Serverless Academy blog, we want to optimize for reads. The content is mostly static: blog posts that we write and you read. Traffic should show that reading far outweighs writing in our system. Therefore, we don't really need:

* A Relational Database Management System
* A comprehensive user management system
* A marketplace of plugins
* etc.

Instead, what we need is:

* A way to write blog posts
* A place to store the content
* A place to store the theme
* A way to publish content

## Writing Blog Posts

Following JAMstack principles, I am able to write blog posts (like the one you're reading) with any text editor. I'm using a Markup called Markdown, which is very readable and can render into a number of formats, including HTML. This means I can focus on writing with the tools I am most comfortable with. Right now, I'm writing this in [Visual Studio Code](https://code.visualstudio.com/).

## Storing Content and Theme

I need a place to store the content. Instead of reaching for a SQL database like I would with Wordpress, I can store the content using just git. Since the content doesn't change too frequently and the filesize is relatively small, I can use standard source control management for this. I've opted to use GitHub as the repository for the content [here](https://github.com/linuxacademy/serverless-blog). I've also created a `git subtree` which allows me to edit the theme and embed it in the same repository as my content, but also [push it to its own repository](https://github.com/linuxacademy/serverless-blog-theme) where others can apply the theme to their blogs as well.

## Publishing Content

To me, this is where things get interesting: we need to take the content and smash it together with the theme and then make the content accessible somewhere on the web. This is where a static site generator comes in. There are tools out there, such as Jekyll, that are pretty ubiquitous. For example, if you create a GitHub repo following Jekyll conventions, GitHub Pages will automatically generate the output for you and serve the content.

Jekyll is slow. Depending on the amount of content and complexity of the navigation on the site, I've seen rendering take upwards of 20 minutes. Instead, I've chosen a Static Site Generator called [Hugo](https://gohugo.io/). Hugo is written in Go, which allows it to be portable and fast. So fast, that we've decided to provide a similar GitHub-Jekyll experience, yet with Hugo by using webhooks and AWS Lambda.

Feel free to [explore the pieces that make this work](https://github.com/linuxacademy/serverless-blog-ops). We'll follow this up with a run-down on deploying your own GitHub-Hugo stack on AWS!