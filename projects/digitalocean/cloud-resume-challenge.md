+++
description = "Follow these steps to complete the Cloud Resume Challenge using DigitalOcean as your cloud provider."
title = "The Cloud Resume Challenge - DigitalOcean"

+++

| Challenge name             | Cloud(s)     | Challenge goal                                                         | Contributor                             |
| :------------------------- | :----------- | :--------------------------------------------------------------------- | :-------------------------------------- |
| The Cloud Resume Challenge | DigitalOcean | "Create a portfolio site that shows off your cloud and DevOps skills." | [amycodes](https://github.com/amycodes) |

## 1. Source Control

You do not want to be updating either your back-end API or your front-end website by making calls from your laptop. You want them to update automatically whenever you make a change to the code. (This is called [continuous integration and deployment, or CI/CD](https://help.github.com/en/actions/building-and-testing-code-with-continuous-integration/about-continuous-integration).) Create a [GitHub repository](https://help.github.com/en/github/creating-cloning-and-archiving-repositories/creating-a-new-repository) for your backend code.

## 2. HTML

Your resume needs to be written in [HTML](https://developer.mozilla.org/en-US/docs/Web/HTML). Not a Word doc, not a PDF. [Here is an example of what I mean](https://codepen.io/emzarts/pen/OXzmym).

## 3. CSS

Your resume needs to be styled with [CSS](https://www.w3schools.com/css/). No worries if you're not a designer -- neither am I. It doesn't have to be fancy. But we need to see something other than raw HTML when we open the webpage.

## 4. Static Website

Your HTML resume should be deployed online using [DigitalOcean AppPlatform](https://www.digitalocean.com/products/app-platform).

## 5. DNS

Point a custom DNS domain name to the AppPlatform Application, so your resume can be accessed at something like my-c00l-resume-website.com. You can use [Custom Domains on DigitalOcean](https://docs.digitalocean.com/products/networking/dns/) or any other DNS provider for this. A domain name usually costs about ten bucks to register.

## 6. Javascript

Your resume webpage should let people submit their e-mail address into a form for further communication. You will need to write a bit of HTML & [Javascript](https://developer.mozilla.org/en-US/docs/Web/JavaScript) to make this happen. Here is a helpful tutorial to get you started in the right direction.

## 7. Database

The contact form should be able to store the addresses in a database. We suggest you use MongoDB, a Managed NoSQL Database option on DigitalOcean. Here is a great [tutorial](https://realpython.com/introduction-to-mongodb-and-python/) on how to connect to MongoDB with Python.

## 8. API

Do not communicate directly with Redis from your Javascript code. Instead, you will need to create an [API](https://medium.com/@perrysetgo/what-exactly-is-an-api-69f36968a41f) that accepts requests from your web app and communicates with the database. I suggest using AppPlatform and DigitalOcean Functions services for this. They will be free or close to free for what we are doing.

## 9. Python

You will need to write a bit of code in the DigitalOcean Function; you could use more Javascript, but it would be better for our purposes to explore Python -- a common language used in back-end programs and scripts. Here is a good, free [Python tutorial](https://www.learnpython.org/).

## 10. Tests

You should also include some tests for your Python code. [Here are some resources](https://realpython.com/python-testing/) on writing good Python tests.

## 11. Infrastructure as Code

You should not be configuring your API resources -- the Redis table, the AppPlatform Static Site, the Function -- manually, by clicking around in the DigitalOcean console. Instead, define them in an [AppPlatform App Specification](https://docs.digitalocean.com/products/app-platform/reference/app-spec/) template and deploy them using the [DigitalOcean Command Line Tool](https://docs.digitalocean.com/reference/doctl/). This is called "[infrastructure as code](https://www.hashicorp.com/resources/what-is-infrastructure-as-code/)" or IaC. It saves you time in the long run.

## 12. CI/CD

Set up [GitHub Actions](https://help.github.com/en/actions/getting-started-with-github-actions/about-github-actions) such that when you push an update to your App Specification template or Python code, your Python tests get run. If the tests pass, the AppPlatform application should get packaged and deployed to DigitalOcean.

## 13. Blog post

Finally, in the text of your resume, you should link a short blog post describing some things you learned while working on this project. [Dev.to](https://dev.to/) or [Hashnode](https://hashnode.com/) are great places to publish if you don't have your own blog.

Congratulations! Through the challenge, you have managed to touch many different cloud services. There are still places where your resume project could be improved, including adding analytics, automation, and external integrations. Also consider building the function with different languages such as NodeJS, PHP, or Go or using different database types. The more services you touch, the better you understand the pros and cons of each one. Happy programming!
