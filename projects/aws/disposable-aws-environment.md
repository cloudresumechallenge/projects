| Challenge name | Cloud(s) | Challenge goal | Contributor |
| :--- | :--- | :--- | :--- |
| Build an automated, disposable AWS development environment | AWS | In this challenge, you will build a simple template to start an AWS Cloud9 environment, along with a CodeCommit repository holding setup scripts. You will be able to quickly initialize a fresh useful isolated development system with fast networking and whatever CPU and RAM you need whenever you need it, and throw it away without fear when you are finished with it. | [Jennine Townsend](https://twitter.com/jt7d) |

## Introduction
AWS's Cloud9 is a cloud-hosted development environment. You might prefer another IDE, or often use Docker or a virtual machine for isolated environments, but sometimes it's handy to be able to quickly spin up a whole isolated environment in the cloud, with the advantage that you can just throw it away and spin up a fresh one whenever you like!

## Prerequisites and helpful resources
Some familiarity with CloudFormation or a similar tool would be helpful. Note that this is quite a simple and self-contained template, so this project in itself could be helpful in learning your chosen tool.
67
* [Cloud9 documentation](https://aws.amazon.com/cloud9)
* ["How does AWS Cloud9 work?"](https://docs.aws.amazon.com/cloud9/latest/user-guide/welcome.html#how-does-it-work), including a nice diagram
* [Jared Short's blog post](https://www.trek10.com/blog/i-buy-a-new-work-machine-everyday) about his Cloud9 setup
* [Documentation for the Cloud9 CloudFormation resource](https://docs.aws.amazon.com/AWSCloudFo rmation/latest/UserGuide/aws-resource-cloud9-environmentec2.html)
* Here’s [a recent post on the AWS Architecture Blog](https://aws.amazon.com/blogs/architecture/field-notes-use-aws-cloud9-to-power-your-visual-studio-code-ide/) that might give you some ideas 

## Challenge steps
1. Cloud9 initial exploration
If you have never tried Cloud9, go ahead and click through the console setup for an "EC2" environment, and get a feel for what it does. Notice how the system will "stop" after being idle for a while (so you’re not paying for CPU+RAM while it’s stopped), and then auto-starts when you resume work.

Read Jared Short's blog post, and try to absorb the view of Cloud9 environments as temporary and easily replaced.

Don't forget to destroy the environment (and all the resources you use) when you're done! The console is convenient, but gets tiresome if you recreate an environment frequently, so we’ll quickly move on to better automation.

2. Simple template
The CloudFormation `AWS::Cloud9::EnvironmentEC2` resource is pretty simple. You can start out really just specifying the instance type, so do that!

There’s [a fairly complicated and slightly out of date template](https://github.com/aws-samples/aws-cloud9-bootstrapping-example/) available, but you can start out with a very minimal one. Make sure you check the CloudFormation documentation for `AWS::Cloud9::EnvironmentEC2` for the current available parameters.

Then look at the other things you can set, such as what OS to run, and what CodeCommit git repositories to clone.

Try out your template, create and destroy a few environments, and try out a couple of the OSes.

### Add a setup script
You might have a script you run on a new system, to set up your prompt and install your preferred tools and so forth. Try running that on Cloud9, and tweak it to work well there.

Jared Short mentioned Ansible in his blog post; Ansible is a configuration management tool, so it is very well-suited to this kind of thing. My setup script is a shell script that installs or upgrades packages on the basis of environment variables, and it configures git, sets up convenient aliases and shell completions, and even grows the disk if I choose!

### Have Cloud9 check out your script at startup
Recall that an environment can check out a CodeCommit git repository upon startup so it's already there when you first log in. Now have a look at the CodeCommit console, and create a repository there (I call mine "cloud9-cfg"). Depending on your familiarity with git, you could check in your script, or just upload it to the repository from the console.

Now add that repository to your template, and next time you start an environment, your script will already be available on the instance! You might want to add more repositories to the list (I check out my personal FAQs repository in every environment, for example).

### Now think about what you might use this for!
* As you work on a project, you might want to add the project repository to the list in the template, or check it out in the setup script.
* Have you wanted to try out a new version of a language, but don't want to risk colliding libraries on your own system? Make another script in your setup repository that installs the language tools of the specific version you want to try out.
* Are you writing code that does a lot of network calls while you're developing and testing it? It's convenient to have an environment in the cloud, where the network is very fast.
* Are you trying out something new, that's changing rapidly? While AWS CDK was in constant flux, I tried it out using Cloud 9, and just constantly updated the version that my script would install.
* Do you want to collaborate with others? Cloud9 includes collaboration capabilities.
* Do you *sometimes* need more power? You can even launch an environment with 32 CPUs and 128 GiB of RAM for less than $5 for three hours -- but be extra sure you don’t leave that running for long!
* If you’ll be teaching a workshop, consider using Cloud9 and providing setup scripts to save time spent helping each individual configure their laptop -- all they need is a web browser and an AWS account.

### [optional] Understand and tweak permissions
The user account on Cloud9 has your IAM permissions, in case you want to connect to other AWS services. You can attach an IAM role / instance profile, and configure Cloud9 to use that instead, if you prefer (for example to test code using the IAM role that its destination instance or service will have). Read the "Security" chapter in the Cloud9 User Guide, and particularly the "Identity and access management" section for details.

### [optional] Tweak networking
Read the Cloud9 documentation about networking. Try inbound and outbound connections, and understand the security implications of opening up an inbound connection.
72

### Consider security
Think about your attack surface. What is exposed? Does your development process involve web servers or other processes that listen on the network? Are they reachable from the Internet? What data do you have on the system? Does your setup script download and run code from elsewhere? Do you trust that code? Does your AWS account have permissions to affect other systems? Test and document all this.

### Write a blog post!
Re-read Jared Short's blog post. Now that you have this new tool available, how do you think you might use it? As your main development environment for day-to-day work? As an easily-disposable, but capable, blank-slate test environment? Will you use the collaboration possibilities? Would you like to try out an exotic new language?

## Extra credit
Here are several ideas you can use to spice up your environment or make the automation more flexible.

### One-click launch
Sometimes you’ll see a "Launch stack" button especially on [an AWS documentation site like this](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/sample-templates-applications-us -west-2.html). 

Figure out how that works! Set up your template with a form where you can specify the instance type and (via a Mapping) what OS to use. This makes it easier for you to show off your template to others: make sure that the "Launch stack" button works for others, setting up an environment in their account.

### URL output
Add a stack output that constructs the console URL to connect to the Cloud9 environment that the stack built, so you can quickly point your browser at it as soon as the stack completes, maybe even scripting the process of retrieving the URL and sending it to your browser.

### Persistent storage
Do you think you might want permanent storage that doesn’t go away each time you replace the environment? Look into S3 and EFS, or you might attach an EBS volume with a filesystem on it. Maybe you could keep data on S3, and copy it to the system’s local (temporary) storage in your startup script.

### Systems Manager
Understand the difference between "EC2" and "SSH" Cloud9 environments -- see the documentation to learn more. Instead of using a setup script, maybe you can use an AWS Systems Manager Run Command document to perform some setup steps.

### Elastic volumizer
Have your script grow the root volume.

Some hints: I get the instance ID using curl from instance meta-data, from that I use the AWS CLI to derive the root volume ID, and then use the CLI to modify the volume. After a few seconds’ sleep just in case, then it uses the Linux "growpart" utility to tell the system to notice the added space, and "resize2fs" to grow the filesystem to fill the space.

Figure out how to do this, and don’t worry about damaging the root filesystem -- if you make a mistake, you can just delete the CloudFormation stack (which terminates the system) and start over. Realize that the root volume goes away with the system, and is not permanent storage.

### Final takeaways
By now you realize that this challenge is really about two things: building familiarity with a genuinely useful AWS offering, and learning how to use CloudFormation to make creating and deleting cloud resources quick and easy. But there’s also an underlying purpose: solidifying the idea that cloud resources, even ones that feel as personal and customized as a development environment, should come and go quickly and easily.