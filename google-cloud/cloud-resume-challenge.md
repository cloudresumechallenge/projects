+++
description = "Follow these steps to complete the Cloud Resume Challenge using Google Cloud (GCP) as your cloud provider."
title = "The Cloud Resume Challenge - GCP"

+++

| Challenge name | Cloud(s) | Challenge goal | Contributor |
| :--- | :--- | :--- | :--- |
| The Cloud Resume Challenge | Google Cloud | "Create a portfolio site that shows off your cloud and DevOps skills." | [@forrestbrazeal](https://twitter.com/forrestbrazeal) |

## 1. Certification

Your resume needs to have the [Google Cloud Digital Leader](https://cloud.google.com/certification/cloud-digital-leader) certification on it. This is an introductory certification that orients you on Google Cloud -- if you have a more advanced Google Cloud cert, that's fine but not expected. You can sit this exam online for $100 USD. [Google offers exam prep resources](https://cloud.google.com/training/business#cloud-digital-leader-path). 

## 2. HTML

 Your resume needs to be written in [HTML](https://developer.mozilla.org/en-US/docs/Web/HTML). Not a Word doc, not a PDF. [Here is an example of what I mean](https://codepen.io/emzarts/pen/OXzmym).

## 3. CSS
Your resume needs to be styled with [CSS](https://www.w3schools.com/css/). No worries if you're not a designer -- neither am I. It doesn't have to be fancy. But we need to see something other than raw HTML when we open the webpage.

## 4. Static Website
Your HTML resume should be deployed online as a static website using [Google Cloud Storage](https://cloud.google.com/storage/docs/hosting-static-website). Services like Netlify and GitHub Pages are great and I would normally recommend them for personal static site deployments, but they make things a little too abstract for our purposes here. Use GCS. 

## 5. HTTPS
The GCS website URL should use [HTTPS](https://www.cloudflare.com/learning/ssl/what-is-https/) for security. You will need to use [a Cloud Load Balancer](https://cloud.google.com/load-balancing/docs/https) to help with this. Be aware - this will have a small cost to provision. You will also want to use [Cloud CDN](https://cloud.google.com/cdn) to cache your site - just check the box when configuring your load balancer backend.

## 6. DNS
Point a custom DNS domain name to the load balancer endpoint, so your resume can be accessed at something like `my-c00l-resume-website.com`. You can use [Cloud Domains](https://cloud.google.com/domains/docs) or any other DNS provider for this. A domain name usually costs about ten bucks to register.

## 7. Javascript
Your resume webpage should include a visitor counter that displays how many people have accessed the site. You will need to write a bit of [Javascript](https://developer.mozilla.org/en-US/docs/Web/JavaScript) to make this happen. Here is a [helpful tutorial](https://www.codecademy.com/learn/introduction-to-javascript) to get you started in the right direction.

## 8. Database
The visitor counter will need to retrieve and update its count in a database somewhere. I suggest you use Google Cloud's [Firestore](https://cloud.google.com/firestore) for this. (It might be a bit overkill to use [Distributed Counters](https://firebase.google.com/docs/firestore/solutions/counters), but it could also be fun!) Be aware that Firestore may incur small costs to store and manipulate data.

## 9. API
Do not communicate directly with Firestore from your Javascript code. Instead, you will need to create an [API](https://medium.com/@perrysetgo/what-exactly-is-an-api-69f36968a41f) that accepts requests from your web app and communicates with the database. I suggest using [Google Cloud Functions for this](https://cloud.google.com/functions) with an [HTTP trigger](https://cloud.google.com/functions/docs/calling/http). They will be free or close to free for what we are doing. 

## 10. Python
You will need to write a bit of code in the serverless function; you could use more Javascript, but it would be better for our purposes to explore Python -- a common language used in back-end programs and scripts -- and its [Google Cloud Client Libraries](https://cloud.google.com/python/docs/reference). Here is a good, free [Python tutorial](https://www.learnpython.org/).

## 11. Tests
You should also include some tests for your Python code. [Here are some resources](https://realpython.com/python-testing/) on writing good Python tests.

## 12. Infrastructure as Code
You should not be configuring your API resources -- the Firestore, the API Gateway, the serverless function -- manually, by clicking around in the Google Cloud console. Instead, define them in a [Terraform template](https://cloud.google.com/blog/topics/developers-practitioners/predictable-serverless-deployments-terraform) and deploy them using the Terraform CLI. This is called "[infrastructure as code](https://www.hashicorp.com/resources/what-is-infrastructure-as-code/)" or IaC. It saves you time in the long run.

## 13. Source Control
You do not want to be updating either your back-end API or your front-end website by making calls from your laptop, though. You want them to update automatically whenever you make a change to the code. (This is called [continuous integration and deployment, or CI/CD](https://help.github.com/en/actions/building-and-testing-code-with-continuous-integration/about-continuous-integration).) Create a [GitHub repository](https://help.github.com/en/github/creating-cloning-and-archiving-repositories/creating-a-new-repository) for your backend code. 

## 14. CI/CD (Back end)
Set up [Cloud Build](https://cloud.google.com/build) such that when you push an update to your Terraform config or Python code, your Python tests get run. If the tests pass, the application should get packaged and deployed to Google Cloud.

## 15. CI/CD (Front end)
Create a second GitHub repository for your website code. Create a Cloud Build configuration such that when you push new website code, the Cloud Storage bucket automatically gets updated. (You may need to [invalidate your Cloud CDN cache](https://cloud.google.com/cdn/docs/invalidating-cached-content) in the code as well.) *Important note: DO NOT commit Google Cloud credentials to source control! Bad hats will find them and use them against you!*

## 16. Blog post
Finally, in the text of your resume, you should link a short blog post describing some things you learned while working on this project. [Dev.to](https://dev.to) or [Hashnode](https://hashnode.com/) are great places to publish if you don't have your own blog.