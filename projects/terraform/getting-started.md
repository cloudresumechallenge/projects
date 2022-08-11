---
title: "Getting Started with Infrastructure as Code"
---

| Challenge name | Cloud(s) | Challenge goal | Contributor |
| :--- | :--- | :--- | :--- |
| Getting Started with Infrastructure as Code | AWS, Google Cloud, Microsoft Azure | Explain the importance of infrastructure as code and how to scale it in an organization. Deploy an infrastructure resources to the cloud of your choice. | [@joatmon08](https://github.com/joatmon08), [@ksatirli](https://github.com/ksatirli) |

### Intro

Imagine you created your resume using a cloud provider's CLI or browser-based Console.

* What happens if you accidentally delete the underlying infrastructure for your resume?
* What if you want to change it to a different cloud provider?

How can you reproduce your resume easily if you delete it or want to move it to another cloud provider? When you create your infrastructure resources using a CLI or browser-based Console, you have to spend time remembering the steps to recreate your resume. What settings did you make for your DNS? What name does the storage bucket have?

To solve these problems, you'll extend your Cloud Resume Challenge project to deploy your resume to the cloud provider of your choice using Infrastructure as Code. [Infrastructure as Code](https://www.hashicorp.com/resources/what-is-infrastructure-as-code) captures and deploys the settings you need for your infrastructure in a codified manner. You can use it to quickly reproduce your resume across different cloud providers and make changes to underlying infrastructure.

You will use HashiCorp Terraform to write your Infrastructure as Code and deploy your resume. Terraform is an open source tool widely used to create Infrastructure as Code. You can choose to get the [Terraform Associate](https://www.hashicorp.com/certification/terraform-associate) certification, an introductory certification that orients you on the value of Infrastructure as Code and how HashiCorp Terraform can help you deploy more consistently. You can sit this exam online for USD 70.50. HashiCorp offers [tutorials](https://learn.hashicorp.com/collections/terraform/certification-associate-tutorials) for the Terraform Associate exam.

### Challenge Guide

1. Prerequisites
    * [Install Terraform.](https://learn.hashicorp.com/tutorials/terraform/install-cli)
    * An active account (and associated credentials) with AWS, Google Cloud, or Microsoft Azure.

1. Configure access credentials for your cloud provider's CLI. These will differ depending on your cloud provider.
   * [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html)
   * [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/authenticate-azure-cli)
   * [Google Cloud CLI](https://cloud.google.com/sdk/docs/initializing)

1. Write the [Terraform provider](https://www.terraform.io/language/providers/configuration) configuration for your cloud of choice.
    * Terraform providers require access credentials so that Terraform can interact with the API of your provider.
    * Optional steps:
      * You can provide access credentials either through your system's environment, or by defining them in the provider configuration block. If you set up your CLI, you do not need to write the credentials in the provider configuration.
      * [Pin your provider's version](https://www.terraform.io/language/providers/requirements) to create a more resilient codebase.

1. [Initialize](https://www.terraform.io/cli/init) your working directory with Terraform to download and set up the provider.

1. Convert your resume's storage bucket into Terraform configuration.
   You'll need to define the [Terraform resource](https://www.terraform.io/language/resources) for your cloud provider's storage service. You can find a list of providers and their resources in the [Terraform Registry](https://registry.terraform.io/).

   The main cloud providers offer the following resources:

   * [AWS S3 Bucket](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket)
   * [Azure Storage Blob](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/storage_blob)
   * [Google Storage Bucket](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/storage_bucket).

1. Preview the [execution plan](https://www.terraform.io/cli/commands/plan) for Terraform to make changes to your cloud provider. Terraform's plan should show a storage bucket getting added. You'll always want to review the plan before making changes.

1. Once you review the execution plan and are satisfied with the intended changes, [apply](https://www.terraform.io/cli/commands/apply) your change with Terraform to create the storage bucket.

1. Examine the [state file](https://www.terraform.io/language/state) for Terraform, you should find your bucket listed in the file. Terraform uses state to store information about the resources it created and its existence in the cloud provider.

1. Convert your resume's HTTPS infrastructure into Terraform configuration. Preview the plan and apply changes to set up HTTPS.
   * You can pass the domain name of the storage bucket to your HTTPS infrastructure by [referencing the resource attribute](https://www.terraform.io/language/expressions/references#references-to-resource-attributes) in your Terraform configuration.
   * You do not have to copy and paste the domain name as a string into your configuration.

1. Convert your resume's DNS infrastructure into Terraform configuration. Preview the plan and apply changes to set up DNS.

1. Convert your resume's database infrastructure into Terraform configuration. Preview the plan and apply changes to set up database.

1. Convert your resume's API (serverless functions and gateway) infrastructure that communicates with the database into Terraform configuration. Preview the plan and apply changes to set up the API.

1. Change an attribute in a Terraform resource, such as database capacity. Preview the plan and apply changes. Terraform's plan show that the resource will have a update.

1. Extra credit
    * [Destroy](https://www.terraform.io/cli/commands/destroy) your resources with Terraform and re-apply to reproduce your resume infrastructure.
    * Create a [GitHub repository](https://help.github.com/en/github/creating-cloning-and-archiving-repositories/creating-a-new-repository) for your Terraform configuration.
    * Automate your Terraform configuration with CI/CD to deploy changes to your resume's backend infrastructure. For example, you can use [Github Actions](https://learn.hashicorp.com/tutorials/terraform/github-actions) to control how Terraform applies changes.
    * In this challenge, you created new resources for your resume. Try [importing](https://learn.hashicorp.com/tutorials/terraform/state-import) your existing backend infrastructure into Terraform management.
    * In previous challenges, you might have used AWS CloudFormation or Azure Resource Manager to create your resume with Infrastructure as Code. Try translating your previous configuration to Terraform with the following approaches, from most
      to least ideal:
      * Terraform conversion tools from the community. such as [Azure Terrafy](https://github.com/Azure/aztfy)
      * [Import cloud resources to Terraform state](https://learn.hashicorp.com/tutorials/terraform/state-import) and rewrite from one language to Terraform
      * Define a Terraform resource for your Infastructure as Code tool, such as [AWS CloudFormation stack resource](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudformation_stack)

1. Finally, in the text of your resume, you should link a short blog post describing some things while creating your resume's infrastructure resources with Terraform.