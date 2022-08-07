+++
description = "Follow these steps to complete the Cloud Resume Challenge using Amazon Web Services as your cloud provider."
title = "The Cloud Resume Challenge - AWS"

+++

| Challenge name | Cloud(s) | Challenge goal | Contributor |
| :--- | :--- | :--- | :--- |
| The Cloud Resume Challenge | AWS | "Create a portfolio site that shows off your cloud and DevOps skills." | [@forrestbrazeal](https://twitter.com/forrestbrazeal) |

## 1. Certification

Your resume needs to have the [AWS Cloud Practitioner certification](https://aws.amazon.com/certification/certified-cloud-practitioner/) on it. This is an introductory certification that orients you on the industry-leading AWS cloud -- if you have a more advanced AWS cert, that's fine but not expected. You can sit this exam online for $100 USD. [A Cloud Guru offers exam prep resources](https://acloud.guru/learn/aws-certified-cloud-practitioner). 

## 2. HTML

 Your resume needs to be written in [HTML](https://developer.mozilla.org/en-US/docs/Web/HTML). Not a Word doc, not a PDF. [Here is an example of what I mean](https://codepen.io/emzarts/pen/OXzmym).

## 3. CSS
Your resume needs to be styled with [CSS](https://www.w3schools.com/css/). No worries if you're not a designer -- neither am I. It doesn't have to be fancy. But we need to see something other than raw HTML when we open the webpage.

## 4. Static Website
Your HTML resume should be deployed online as an [Amazon S3 static website](https://docs.aws.amazon.com/AmazonS3/latest/dev/WebsiteHosting.html). Services like Netlify and GitHub Pages are great and I would normally recommend them for personal static site deployments, but they make things a little too abstract for our purposes here. Use S3. 

## 5. HTTPS
The S3 website URL should use [HTTPS](https://www.cloudflare.com/learning/ssl/what-is-https/) for security. You will need to use [Amazon CloudFront](https://aws.amazon.com/blogs/networking-and-content-delivery/amazon-s3-amazon-cloudfront-a-match-made-in-the-cloud/) to help with this.

## 6. DNS
Point a custom DNS domain name to the CloudFront distribution, so your resume can be accessed at something like `my-c00l-resume-website.com`. You can use [Amazon Route 53](https://aws.amazon.com/route53/) or any other DNS provider for this. A domain name usually costs about ten bucks to register.

## 7. Javascript
Your resume webpage should include a visitor counter that displays how many people have accessed the site. You will need to write a bit of [Javascript](https://developer.mozilla.org/en-US/docs/Web/JavaScript) to make this happen. Here is a [helpful tutorial](https://www.codecademy.com/learn/introduction-to-javascript) to get you started in the right direction.

## 8. Database
The visitor counter will need to retrieve and update its count in a database somewhere. I suggest you use Amazon's [DynamoDB](https://aws.amazon.com/dynamodb/) for this. (Use on-demand pricing for the database and you'll pay essentially nothing, unless you store or retrieve much more data than this project requires.) Here is a [great free course](https://acloudguru.com/course/amazon-dynamodb-deep-dive) on DynamoDB (requires a free account).

## 9. API
Do not communicate directly with DynamoDB from your Javascript code. Instead, you will need to create an [API](https://medium.com/@perrysetgo/what-exactly-is-an-api-69f36968a41f) that accepts requests from your web app and communicates with the database. I suggest using AWS's API Gateway and Lambda services for this. They will be free or close to free for what we are doing. 

## 10. Python
You will need to write a bit of code in the Lambda function; you could use more Javascript, but it would be better for our purposes to explore Python -- a common language used in back-end programs and scripts -- and its [boto3 library for AWS](https://boto3.amazonaws.com/v1/documentation/api/latest/index.html). Here is a good, free [Python tutorial](https://www.learnpython.org/).

## 11. Tests
You should also include some tests for your Python code. [Here are some resources](https://realpython.com/python-testing/) on writing good Python tests.

## 12. Infrastructure as Code
You should not be configuring your API resources -- the DynamoDB table, the API Gateway, the Lambda function -- manually, by clicking around in the AWS console. Instead, define them in an [AWS Serverless Application Model (SAM) template](https://aws.amazon.com/serverless/sam/) and deploy them using the AWS SAM CLI. This is called "[infrastructure as code](https://www.hashicorp.com/resources/what-is-infrastructure-as-code/)" or IaC. It saves you time in the long run.

## 13. Source Control
You do not want to be updating either your back-end API or your front-end website by making calls from your laptop, though. You want them to update automatically whenever you make a change to the code. (This is called [continuous integration and deployment, or CI/CD](https://help.github.com/en/actions/building-and-testing-code-with-continuous-integration/about-continuous-integration).) Create a [GitHub repository](https://help.github.com/en/github/creating-cloning-and-archiving-repositories/creating-a-new-repository) for your backend code. 

## 14. CI/CD (Back end)
Set up [GitHub Actions](https://help.github.com/en/actions/getting-started-with-github-actions/about-github-actions) such that when you push an update to your Serverless Application Model template or Python code, your Python tests get run. If the tests pass, the SAM application should get packaged and deployed to AWS.

## 15. CI/CD (Front end)
Create a second GitHub repository for your website code. Create GitHub Actions such that when you push new website code, the S3 bucket automatically gets updated. (You may need to [invalidate your CloudFront cache](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Invalidation.html) in the code as well.) *Important note: DO NOT commit AWS credentials to source control! Bad hats will find them and use them against you!*

## 16. Blog post
Finally, in the text of your resume, you should link a short blog post describing some things you learned while working on this project. [Dev.to](https://dev.to) or [Hashnode](https://hashnode.com/) are great places to publish if you don't have your own blog.