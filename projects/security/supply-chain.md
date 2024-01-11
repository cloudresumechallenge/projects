---
title: "Securing your software supply chain"
---

| Challenge name | Cloud(s) | Challenge goal | Contributor |
| :--- | :--- | :--- | :--- |
| Securing Your Software Supply Chain | Google Cloud, AWS, Azure | Improve the security of your resume site by protecting your software dependencies from attack | [@forrestbrazeal](https://twitter.com/forrestbrazeal) |

### Intro
The [software supply chain](https://tanzu.vmware.com/what-is-a-secure-software-supply-chain) is everything involved in getting code from your laptop to production: the code and configuration you write as well as any underlying packages and libraries they rely on (also known as "dependencies"). Securing the software supply chain, particularly these dependencies, from compromise is an emerging discipline in modern software development and infosec. The stakes couldn't be higher - just check out [this list of recent high-profile supply chain attacks](https://github.com/cncf/tag-security/tree/main/supply-chain-security/compromises).

In this challenge, you'll extend your Cloud Resume Challenge project to add protections to your code and dependencies.


### Helpful reading

* Check out [Microsoft's software supply chain best practices](https://docs.microsoft.com/en-us/nuget/concepts/security-best-practices). These recommendations are based around NuGet, the package manager for Microsoft's .NET ecosystem, but much of the advice generalizes well.
* Take a whirl through the Cloud Native Computing Foundation's [software supply chain repo](https://github.com/cncf/tag-security), particularly the [compromise definitions](https://github.com/cncf/tag-security/blob/main/supply-chain-security/compromises/compromise-definitions.md) and the [whitepaper](https://github.com/cncf/tag-security/blob/main/supply-chain-security/supply-chain-security-paper/CNCF_SSCP_v1.pdf).
* Here's [a helpful video](https://www.youtube.com/watch?v=7CMhIDAPjEs&t=876s) walking through supply chain attacks in the Kubernetes ecosystem.
* Get familiar with [GitHub's security features](https://docs.github.com/en/code-security/getting-started/github-security-features); a decent percentage of real-world software supply chain protection is just "turning the right knobs in GitHub", it seems.
* Supply chain Levels for Software Artifacts (SLSA) provides information around supply chain threats and best practices. There is also a cool badge for your repository. Read more at [slsa.dev](https://slsa.dev/) and their [quick start guide](https://slsa.dev/get-started)

### Challenge steps

1. **[Sign your Git commits](https://docs.github.com/en/authentication/managing-commit-signature-verification/signing-commits)** to both the front end and back end resume repositories. You'll need to [set up a GPG key](https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key) to do this. You'll know it's working when you see the "Verified" badge next to the commit in the GitHub console. 
1. **Use [status checks](https://github.blog/2015-09-03-protected-branches-and-required-status-checks/)** to ensure that only signed commits can be merged into your repository.
1. **Set up [automated code scanning](https://docs.github.com/en/code-security/code-scanning/automatically-scanning-your-code-for-vulnerabilities-and-errors)** using GitHub's CodeQL code analysis tool on GitHub Actions. Note that you will need to make your repositories public for this to work. You should automatically run the code scan any time a pull request is merged to your main branch and fail the merge if security issues at level "High" or higher are detected. You should also guard against dependency decay by running the scan on a schedule once per month. You will have to edit a config file to adjust the schedule.
1. **Generate an SBOM (Software Bill of Materials).** An [SBOM](https://www.cisa.gov/sbom) is a manifest that lists all the packages shipped in your container image or other code environment. As part of the build step in your back-end repository's CI/CD pipeline, generate an SBOM attestation file for your deployment artifact using the open source tool [Syft](https://github.com/anchore/syft). (If you are shipping your code and dependencies as a zip file on AWS Lambda, not using a container image, you should still be able to point Syft at the unzipped deployment artifact to get an attestation.)
1. **Automate at least one additional vulnerability check in your CI/CD workflow.** Using the package list in your SBOM, write some automation to run at least one other dependency check besides the GitHub automated scanning. Vulnerability databases are not always equally reliable, and it's a good idea to check a couple of sources to provide defense-in-depth. [Grype](https://github.com/anchore/grype) is a scanner that works well with Syft (and has its own GitHub Action). You could also consult an API such as [OSV](https://osv.dev/). Fail the build with an appropriate error message if you encounter a compromised dependency.
1. [For container users only] **Sign your container image using [Cosign](https://github.com/sigstore/cosign).** If your Cloud Resume Challenge workflow involves building a container image, generate a KMS key on your cloud provider of choice using AWS KMS, Google Cloud KMS, or Azure Key Vault, then sign the container image with Sigstore's Cosign tool before uploading it to AWS Elastic Container Registry (ECR), Google Cloud's Artifact Registry, or Azure Container Registry. Make sure to include the Syft attestation from the previous step. This will verify for other consumers of this container that you have shipped the packages you said you shipped.
1. [For AWS Lambda users only] AWS Lambda, which does not use a container-based deployment artifact by default, has [its own code signing feature](https://docs.aws.amazon.com/lambda/latest/dg/configuration-codesigning.html). Add code signing into your infrastructure-as-code definition for your API.
1. Write up a blog post about what you learned! Include a diagram showing how code flows through your system and where attacks can be detected / mitigated. Reflect on where you may still have risks, and what other steps you might take if this were a more sensitive project, or involved multiple collaborators.


