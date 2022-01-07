# Advanced Tier Work Package
The consultant will lead the end customer to cover the subjects mentioned below over a one to two day period using this guide. These sessions will be a combination of instructor led training and examples based on real world use cases and provide the customer with the opportunity to carry out the scenarios for themselves.

Topics to cover:
-   Registry Integration
-   Vulnerability Scanning
-   Assurance Policies – Images
-   CI/CD integration
-   SSO/SAML integration

You can break down the time spent working with the customer on these subjects over six to eight sections lasting around two to three hours for each section. Some scenarios may be much shorter to do [ TBD ]

[ insert table and time allocation when other content is defined]

## Showing the relationship between Aqua capabilities

At a high level, Aquasec can be configured to scan container images from several supported container registries.

The Venn diagram below represents the relationships between each of the Aqua Components.

[insert diagram]

<![endif]-->

Naturally, vulnerability scanning cannot happen without integrating the customer’s container registries, and image scanning is dependent upon those registries existing within the Aquasec console.

By default, Aquasec provides an existing container registry integration out of the box, which is Docker Hub. This can be used to scan public images and is a good starting point to show customers if they want to see this work out of the box.

Additionally, no Image Assurance policies can be applied to images from a repo, without a container registry existing, after the results of an image being pulled and scanned from the image repo within the registry for a particular image.

Aquasec provides a set of baseline Image Assurance Policies out of the box, that provide several controls that are applied to the images from the repositories in each container registry.

## Registry Integration

**Session aim**:  to produce a list of the container registries with the customer which they are using and to create registry integrations within their SaaS console so that the customer can begin to scan images from their registry.

As the customer’s consultant you will need to establish whether the customer’s registries are hosted on premise or if they’re using cloud hosted registries, such as Azure ACR, AWS ECR or Google GCR, additionally the other registries that we support are listed here  
[https://docs.aquasec.com/docs/image-registries-and-repositories#section-registry-details-tab](https://docs.aquasec.com/docs/image-registries-and-repositories#section-registry-details-tab)

Where a customer is using on-premises container registries and the Aqua SaaS instance, you will need to configure the Aqua cloud connector before any images from repos can be scanned by Aquasec.

Information on how the Aqua cloud connector works and how it is deployed is covered in the link below.  
[https://docs.aquasec.com/docs/aqua-cloud-connector#introduction](https://docs.aquasec.com/docs/aqua-cloud-connector#introduction)

We recommend that you take time to do this in advance to check it works per the customers use case(s) and that you can scan images from the customers on premises registry _or a replicated one of the same type in your own environment_. Allocate at least four hours to configure an on-premises container registry which is the. Same as your customer in conjunction with the Aqua Cloud Connector deployment and config.

## Image Assurance Policies

**Session Aim:** Help the customer identify which Image assurance controls they wish to use for their business and use case and explore which controls fit their needs. It will be of benefit for the customer to show them what happens when one policy control is activated and applied and what the impact is on the scanned images and how a control makes the image non-compliant.  
  
Since Aquasec provides two baseline policies for image assurance, one being the **Default** image policy and the other is for **DTA**.

The Default image assurance policy is enough to get the customer started however it does not include any additional controls which means that you will need to get a better understanding of what they will want to include in their policy.

One of the ways to do this is to start with a custom policy with a handful of controls such as the one shown below.
![Example Image Assurance Policy](https://github.com/kenmccann/advanced-tier-offering/blob/master/image/policy1.png?raw=true)

We have provided a copy of this policy in JSON format which is saved to SharePoint in the PS architects [Policy Examples folder](https://aquasecurity.sharepoint.com/:u:/s/CustomerSuccessArchitects/Ef8DeoDr4V9Dl0HKaEZnopwBLGoIJC_uLILvPTWurlaKdg?e=bbDNwu) 

You can customise this policy with the customer by selecting and deselecting the existing controls and even explore small changes with them in their console.

There is also a set of documents in the [PS Architecture SharePoint](https://aquasecurity.sharepoint.com/sites/CustomerSuccessArchitects/Shared%20Documents/Forms/AllItems.aspx?id=%2Fsites%2FCustomerSuccessArchitects%2FShared%20Documents%2FGuides%2FPolicy%20Configuration&viewid=2c0cd9c5%2Dfb91%2D4dd5%2D8362%2D3f8bb3e566f9) that covers best practices for Image Assurance

Since all the Image Assurance policies can be created and applied in a layered fashion, they will control within the policies apply to all images which have been scanned within the Aqua SaaS console and effect the results against each image and additional images that are scanned thereafter.

The impact of this means that if the image does not comply with the assurance polices, that image is deemed as non-compliant. More information about IA can be found on the Documentation portal.

### GitOps  
  
_Do we want to cover this by explaining how policies within aqua can be created, then stored within Github, and for any policy to updated & pushed programmatically into the console using the API via a CI job so that change control can be managed and preventing human error – where policies are applied between Dev/Test –> Non Prod -> Production environments?_

## Vulnerability Scanning

Once your customer has integrated their container registry into the Aquasec Saas console, you will be able to guide the customer as to how they start scanning images and producing vulnerability reports.

  
**Session aim**: The consultant should work with the customer to provide a high-level view and example of scanning images from a public docker repo, explaining the Vulnerability results and Risk based insights using the SaaS console.  Explaining to the customer how to interpret and understand the results and what they mean.

First start by selecting a couple of images from Docker hub, such as alpine:3.4 and ubuntu:14.04 to show the customer the kind of information which is obtained about images when they are scanned etc.

You should guide the customer through the scan results for the selected images and provide advice and direction of what this means and cover the tabs and data collected about the image within the UI.  
  

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTkyMTg4Njc5OCwtMTczMzMwMzU4OCwxNz
Q3NzY3NDA4XX0=
-->