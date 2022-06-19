---
title: "Contribute"
weight: 99
---
It's time for a meta-challenge: if you've built or benefited from the Cloud Resume Challenge, why not take the step of becoming an open-source contributor to [the project itself](https://github.com/cloudresumechallenge/projects)?

## Ways to contribute to the Cloud Resume Challenge
1. **Update [the challenge documentation](https://github.com/cloudresumechallenge/projects)**.
   A great way to take your first step into open source. Fix a typo, add a link to a helpful resource, etc.
1. **Port a challenge extension to another cloud.** The core Cloud Resume Challenge includes parallel sets of instructions for AWS, Azure, and Google Cloud, but not every challenge extension does the same. If you have, say, Azure expertise, you could help future Azure challengers by translating an existing AWS-only challenge for them.
1. **Write a new extension to the Cloud Resume Challenge** (see below!) 

## A blueprint for writing your own challenge extension

Cloud Resume Challenge extensions build on the core resume site to give additional hands-on practice with cloud development, automation, or architecture. We are always looking for more extensions to the challenge!

If you would like to contribute a challenge, copy the following markdown into a new file. Update the placeholder text in brackets with the elements of your challenge, then pull request it to the appropriate folder in the ["projects" section](https://github.com/cloudresumechallenge/projects/tree/main/projects) of the repo.

| Challenge name | Cloud(s) | Challenge goal | Contributor |
| :--- | :--- | :--- | :--- |
| ["Securing Your Software Supply Chain"] | [Google Cloud, AWS] | [1-2 sentences describing the learning objectives of this project - why might hiring managers be impressed by this project?] | [Your name or Github handle (feel free to link to your blog / twitter /etc )] |

### Challenge Guide
1. [Prerequisites: provide a short bullet list with download links/setup guides to any major languages, tools or frameworks learners will need to use in this project]

1. [Diagram: Provide a small diagram showing the cloud services used in the project and how they fit together. This can be high-level/ conceptual]

1. Challenge steps

Now you will provide the steps of the challenge one by one.
* There should be around 6 to 12 steps - no more than 15.
* Each step gives the user a task to do, like connect a database to a BI service.
* The steps can link to helpful guides or tutorials, but you shouldn’t explain every single action the user needs to complete in order to complete the step.
* The learner is expected to be able to Google to figure out some things throughout the project.
You’re not creating a step-by-step tutorial; you’re providing a spec, it’s up to them to figure out exactly how to implement it.
* The last step of the challenge should ALWAYS be for them to write a short blog post explaining what they learned.

4. [Extra credit (optional): Provide 2-3 additional tweaks to the challenge for “extra credit”. Common ideas are: add CI/CD, add a front-end dashboard, etc]

5. How to use this challenge in a job interview

[Provide a paragraph or two explaining why this challenge is relevant for people looking to enhance their cloud skills. Give them a rousing call to action and wish them good luck!]
