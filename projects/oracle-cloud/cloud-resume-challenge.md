+++
description = "Follow these steps to complete the Cloud Resume Challenge using Oracle Cloud Infrastructure as your cloud provider."
title = "The Cloud Resume Challenge - OCI"

+++

| Challenge name | Cloud(s) | Challenge goal | Contributor |
| :--- | :--- | :--- | :--- |
| The Cloud Resume Challenge | OCI | "Create a portfolio site that shows off your cloud and DevOps skills." | [Graham-Baggett](https://github.com/Graham-Baggett) |

## 1. Certification

Your resume needs to have the [OCI Certified Foundations Associate certification](https://education.oracle.com/oracle-cloud-infrastructure-2022-foundations-associate/pexam_1Z0-1085-22) on it. This is an introductory certification that orients you on the Oracle cloud -- if you have a more advanced OCI cert, that's fine but not expected. You can sit this exam online for free. 

## 2. HTML

 Your resume needs to be written in [HTML](https://developer.mozilla.org/en-US/docs/Web/HTML). Not a Word doc, not a PDF. [Here is an example of what I mean](https://codepen.io/emzarts/pen/OXzmym).

## 3. CSS
Your resume needs to be styled with [CSS](https://www.w3schools.com/css/). No worries if you're not a designer -- neither am I. It doesn't have to be fancy. But we need to see something other than raw HTML when we open the webpage.

## 4. Static Website
Your HTML resume should be deployed online as a static website. Use Object Storage to store your website files. 

## 5. DNS
Point a custom DNS domain name to the CloudFront distribution, so your resume can be accessed at something like `my-c00l-resume-website.com`. You can use any DNS provider for this. A domain name usually costs about twelve bucks to register.

## 6. Javascript
Your resume webpage should include a visitor counter that displays how many people have accessed the site. You will need to write a bit of [Javascript](https://developer.mozilla.org/en-US/docs/Web/JavaScript) to make this happen. Here is a [helpful tutorial](https://www.codecademy.com/learn/introduction-to-javascript) to get you started in the right direction.

## 7. Database
The visitor counter will need to retrieve and update its count in a database somewhere. I suggest you use Oracle's [NoSQL Database](https://www.oracle.com/database/nosql/) for this. (Use on-demand pricing for the database and you'll pay essentially nothing, unless you store or retrieve much more data than this project requires.)

## 8. API
Do not communicate directly with NoSQL Database from your Javascript code. Instead, you will need to create an [API](https://medium.com/@perrysetgo/what-exactly-is-an-api-69f36968a41f) that accepts requests from your web app and communicates with the database. I suggest using OCI's API Gateway and Functions services for this. They will be free or close to free for what we are doing. 

## 9. Python
You will need to write a bit of code in OCI Functions; you could use more Javascript, but it would be better for our purposes to explore Python -- a common language used in back-end programs and scripts -- and its [borneo library for OCI](https://nosql-python-sdk.readthedocs.io/en/latest/index.html). Here is a good, free [Python tutorial](https://www.learnpython.org/).

## 10. Tests
You should also include some tests for your Python code. [Here are some resources](https://realpython.com/python-testing/) on writing good Python tests.

## 11. Infrastructure as Code
You should not be configuring your API resources -- the NoSQL Database table, the API Gateway, the Functions function -- manually, by clicking around in the AWS console. Instead, define them in a [Terraform template](https://www.terraform.io/) and deploy them using the [OCI Resource Manager](https://docs.oracle.com/en-us/iaas/Content/ResourceManager/home.htm#ResourceManager). This is called "[infrastructure as code](https://www.hashicorp.com/resources/what-is-infrastructure-as-code/)" or IaC. It saves you time in the long run.

## 12. Source Control
You do not want to be updating either your back-end API or your front-end website by making calls from your laptop, though. You want them to update automatically whenever you make a change to the code. (This is called [continuous integration and deployment, or CI/CD](https://help.github.com/en/actions/building-and-testing-code-with-continuous-integration/about-continuous-integration).) Create a [GitHub repository](https://help.github.com/en/github/creating-cloning-and-archiving-repositories/creating-a-new-repository) for your backend code. 

## 13. CI/CD (Back end)
Set up [GitHub Actions](https://help.github.com/en/actions/getting-started-with-github-actions/about-github-actions) such that when you push an update to your Terraform template or Python code, your Python tests get run. If the tests pass, the resources defined in Terraform should get deployed to OCI.

## 14. CI/CD (Front end)
Create a second GitHub repository for your website code. Create GitHub Actions such that when you push new website code, the Object Storage bucket automatically gets updated.  *Important note: DO NOT commit OCI keys or fingerprints to source control! Bad hats will find them and use them against you!*

## 15. Blog post
Finally, you should write a short blog post describing some things you learned while working on this project. [LinkedIn](https://www.linkedin.com/feed/) is a nice place to publish if you don't have your own blog.

Congratulations on completing the OCI Cloud Resume Challenge! I encourage you to keep learning and find new ways to utilize your Cloud and DevOps skills.
