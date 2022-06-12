+++
description = "Follow these steps to complete the Cloud Resume Challenge using Microsoft Azure as your cloud provider."
title = "The Cloud Resume Challenge - Azure"

+++

| Challenge name | Cloud(s) | Challenge goal | Contributor |
| :--- | :--- | :--- | :--- |
| The Cloud Resume Challenge | Microsoft Azure | "Create a portfolio site that shows off your cloud and DevOps skills." | [@forrestbrazeal](https://twitter.com/forrestbrazeal) |

## 1. Certification

Your resume needs to have the [AZ-900 certification](https://docs.microsoft.com/en-us/learn/certifications/exams/az-900) on it. This is an introductory certification that orients you on the Azure cloud -- if you have a more advanced Azure cert, that's fine but not expected. You can sit this exam online for $100 USD. [A Cloud Guru offers exam prep resources](https://acloudguru.com/course/az-900-microsoft-azure-fundamentals). 

## 2. HTML

 Your resume needs to be written in [HTML](https://developer.mozilla.org/en-US/docs/Web/HTML). Not a Word doc, not a PDF. [Here is an example of what I mean](https://codepen.io/emzarts/pen/OXzmym).

## 3. CSS
Your resume needs to be styled with [CSS](https://www.w3schools.com/css/). No worries if you're not a designer -- neither am I. It doesn't have to be fancy. But we need to see something other than raw HTML when we open the webpage.

## 4. Static Website
Your HTML resume should be deployed online as an [Azure Storage static website](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blob-static-website). Services like Netlify and GitHub Pages are great and I would normally recommend them for personal static site deployments, but they make things a little too abstract for our purposes here. Use Azure Storage. 

## 5. HTTPS
The Azure Storage website URL should use [HTTPS](https://www.cloudflare.com/learning/ssl/what-is-https/) for security. You will need to use [Azure CDN](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-custom-domain-name?tabs=azure-portal#map-a-custom-domain-with-https-enabled) to help with this.

## 6. DNS
Point a custom DNS domain name to the Azure CDN endpoint, so your resume can be accessed at something like `my-c00l-resume-website.com`. You can use [Azure DNS](https://docs.microsoft.com/en-us/azure/cdn/cdn-map-content-to-custom-domain) or any other DNS provider for this. A domain name usually costs about ten bucks to register.

## 7. Javascript
Your resume webpage should include a visitor counter that displays how many people have accessed the site. You will need to write a bit of [Javascript](https://developer.mozilla.org/en-US/docs/Web/JavaScript) to make this happen. Here is a [helpful tutorial](https://www.codecademy.com/learn/introduction-to-javascript) to get you started in the right direction.

## 8. Database
The visitor counter will need to retrieve and update its count in a database somewhere. I suggest you use the [Table API](https://docs.microsoft.com/en-us/azure/cosmos-db/table/introduction) of Azure's [CosmosDB](https://docs.microsoft.com/en-us/azure/cosmos-db/introduction) for this. (Use [serverless capacity mode](https://docs.microsoft.com/en-us/azure/cosmos-db/serverless) for the database and you'll pay essentially nothing, unless you store or retrieve much more data than this project requires.)

## 9. API
Do not communicate directly with CosmosDB from your Javascript code. Instead, you will need to create an [API](https://medium.com/@perrysetgo/what-exactly-is-an-api-69f36968a41f) that accepts requests from your web app and communicates with the database. I suggest using [Azure Functions with an HTTP trigger](https://docs.microsoft.com/en-us/azure/azure-functions/functions-bindings-http-webhook) for this. They will be free or close to free for what we are doing. 

## 10. Python
You will need to write a bit of code in the Azure Function; you could use more Javascript, but it would be better for our purposes to explore Python -- a common language used in back-end programs and scripts -- and its [Azure SDK](https://github.com/Azure/azure-sdk-for-python). Here is a good, free [Python tutorial](https://www.learnpython.org/).

## 11. Tests
You should also include some tests for your Python code. [Here are some resources](https://realpython.com/python-testing/) on writing good Python tests.

## 12. Infrastructure as Code
You should not be configuring your API resources -- the Azure Function, the CosmosDB -- manually, by clicking around in the Azure console. Instead, define them in an [Azure Resource Manager (ARM) template](https://docs.microsoft.com/en-us/azure/azure-functions/functions-infrastructure-as-code) on a [Consumption plan](https://azure.microsoft.com/en-us/resources/templates/function-app-create-dynamic/). This is called "[infrastructure as code](https://www.hashicorp.com/resources/what-is-infrastructure-as-code/)" or IaC. It saves you time in the long run.

## 13. Source Control
You do not want to be updating either your back-end API or your front-end website by making calls from your laptop, though. You want them to update automatically whenever you make a change to the code. (This is called [continuous integration and deployment, or CI/CD](https://help.github.com/en/actions/building-and-testing-code-with-continuous-integration/about-continuous-integration).) Create a [GitHub repository](https://help.github.com/en/github/creating-cloning-and-archiving-repositories/creating-a-new-repository) for your backend code. 

## 14. CI/CD (Back end)
Set up [GitHub Actions](https://help.github.com/en/actions/getting-started-with-github-actions/about-github-actions) such that when you push an update to your ARM template or Python code, your Python tests get run. If the tests pass, the ARM application should get packaged and deployed to Azure.

## 15. CI/CD (Front end)
Create a second GitHub repository for your website code. Create GitHub Actions such that when you push new website code, the Azure Storage blob automatically gets updated. (You may need to [purge your Azure CDN endpoint](https://docs.microsoft.com/en-us/azure/cdn/cdn-purge-endpoint) in the code as well.) *Important note: DO NOT commit Azure credentials to source control! Bad hats will find them and use them against you!*

## 16. Blog post
Finally, in the text of your resume, you should link a short blog post describing some things you learned while working on this project. [Dev.to](https://dev.to) or [Hashnode](https://hashnode.com/) are great places to publish if you don't have your own blog.