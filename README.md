![Aqua Security Software](https://github.com/kenmccann/advanced-tier-offering/blob/master/image/aqua-logo-black.png?raw=true)

# Advanced Tier Work Package
*Produced by Daniel Cave, 
DevSecOps Architect, Aqua Security. January 2022.*

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

At a high level, Aqua can be configured to scan container images from several supported container registries.

The Venn diagram below represents the relationships between each of the Aqua Components.

![](https://github.com/kenmccann/advanced-tier-offering/blob/master/image/3vens.png?raw=true)
Vulnerability scanning cannot happen without integrating the customer’s container registries into Aqua and image scanning is dependent upon those registries existing within the Aqua console.

By default, Aqua's registry configuration provides an existing container registry integration out of the box, which is Docker Hub. This can be used to scan public images and is a good starting point to show customers if they want to see this work out of the box.

Additionally,  Image Assurance policies cannot be applied to images from a repo, unless they originate from a configured container registry.  

Aqua provides a set of baseline Image Assurance Policies out of the box, that provide several controls that are applied to the images from the repositories in each container registry.

## Registry Integration

**Session aim**:  to produce a list of the container registries with the customer which they are using and to create registry integrations within their SaaS console so that the customer can begin to scan images from their registry.

As the customer’s consultant you will need to establish whether the customer’s registries are hosted on premise or if they’re using cloud hosted registries, such as Azure ACR, AWS ECR or Google GCR, additionally the other registries that we support are listed here  
[https://docs.aquasec.com/docs/image-registries-and-repositories#section-registry-details-tab](https://docs.aquasec.com/docs/image-registries-and-repositories#section-registry-details-tab)

Where a customer is using on-premises container registries and the Aqua SaaS instance, you will need to configure the Aqua cloud connector before any images from repos can be scanned by Aqua.

Information on how the Aqua cloud connector works and how it is deployed is covered in the link below.  
[https://docs.aquasec.com/docs/aqua-cloud-connector#introduction](https://docs.aquasec.com/docs/aqua-cloud-connector#introduction)

We recommend that you take time to do this in advance to check it works per the customers use case(s) and that you can scan images from the customers on premises registry _or a replicated one of the same type in your own environment_. Allocate at least four hours to configure an on-premises container registry which is the. Same as your customer in conjunction with the Aqua Cloud Connector deployment and config.

## Image Assurance Policies

**Session Aim:** Help the customer identify which Image assurance controls they wish to use for their business and use case and explore which controls fit their needs. It will be of benefit for the customer to show them what happens when one policy control is activated and applied and what the impact is on the scanned images and how a control makes the image non-compliant.  
  
### Understanding Image Assurance controls

Since Aqua provides two baseline policies for image assurance, one being the **Default** image policy and the other is for **DTA**.

The **Default** image assurance policy is enough to get the customer started however it does not include any additional controls which means that you will need to get a better understanding of what they will want to include in their policy.

### Creating a custom policy for your customers use case
One of the ways to do this is to start with a custom policy with a handful of controls such as the one shown below. It's a good idea to start with a few controls within one policy to keep it simple, this makes interpreting and acting upon the results easier for the customer to digest as they learn how Aqua's IA works, instead of creating a policy with all the controls and potentially overwhelming the customer with far too much information to process.

In any customer setup you would start with a few basic policy controls such as :
 - Malware
 - Sensitive Data
 - Vulnerability Score &/or Severity
 
 The vulnerability score can be modified on the sliding scale depending on the customers policy or posture towards risk according to their environments.

![Example Image Assurance Policy](https://github.com/kenmccann/advanced-tier-offering/blob/master/image/policy1.png?raw=true)
This example policy would mark any container image which has been scanned, or any new images that are scanned subsequently that contain any of the risk controls, as non compliant, in this example use case as they do not comply to this policy.

We have provided a copy of this policy in JSON format which is saved to SharePoint in the PS architects [Policy Examples folder](https://aquasecurity.sharepoint.com/:u:/s/CustomerSuccessArchitects/Ef8DeoDr4V9Dl0HKaEZnopwBLGoIJC_uLILvPTWurlaKdg?e=bbDNwu) 

You can customise this policy further with the customer by selecting and deselecting the existing controls and even explore small changes with them in their console.

There is also a set of documents in the [PS Architecture SharePoint](https://aquasecurity.sharepoint.com/sites/CustomerSuccessArchitects/Shared%20Documents/Forms/AllItems.aspx?id=%2Fsites%2FCustomerSuccessArchitects%2FShared%20Documents%2FGuides%2FPolicy%20Configuration&viewid=2c0cd9c5%2Dfb91%2D4dd5%2D8362%2D3f8bb3e566f9) that covers best practices for Image Assurance

### Additional customised Policies

Since it is possible to create multiple custom policies they will all be applied  and combined in a layered fashion,  thus control will be applied to all images which have been scanned within the Aqua SaaS console and effect the results against each image and additional images that are scanned thereafter.

The impact of this means that if the image does not comply with the assurance polices, that image is deemed as non-compliant. More information about IA can be found on the Documentation portal.


### GitOps  
  
_Do we want to cover this by explaining how policies within aqua can be created, then stored within Github, and for any policy to updated & pushed programmatically into the console using the API via a CI job so that change control can be managed and preventing human error – where policies are applied between Dev/Test –> Non Prod -> Production environments?_

## Vulnerability Scanning

Once your customer has integrated their container registry into the Aqua Saas console, you will be able to guide the customer as to how they start scanning images and producing vulnerability reports.

**Session aim**: The consultant should work with the customer to provide a high-level view and example of scanning images from a public docker repo, explaining the Vulnerability results and Risk based insights using the SaaS console.  Explaining to the customer how to interpret and understand the results and what they mean.

### Understanding Image Scanning within Aqua
First start by selecting a couple of images from Docker hub, such as alpine:3.4 and ubuntu:14.04 to show the customer the kind of information which is obtained when they are scanned and what vulnerabilies & CVE's are likely to exist for images within the container.

### Invoking a Manual Scan

Images can be scanned independently by using the "Add Images" button within the Images part of the UI.   The  documentation link  [here](https://docs.aquasec.com/docs/repository-operations) explains more about how this process works - it's  largely intuitive - it also covers more details about the registry settings and configurations used by customers.

For our example use case, we have added the alpine:3:4 image to the scan queue which then invokes the scan (via a docker pull). The Aqua scanner scans the container image, reports the results back to the console which can be seen in the UI against the registry and repo name.

Some customers may ask:

> How does Aqua get the information about vulnerabilities and CVE's from the container?

***Answer**: Basically, the Aqua scanner decomposes the container image and scans each layer and creates a *sha256* hash of each file/binary within that layer. 

The results containing all the hashes and details of the container, including it's digest and content hash are sent to Cybercenter [ our cloud vulnerability DB ]  for it to process and identify which files and pakages it recognises that contain vulnerabilties, then Cybercenter sends those results back for the console to process the results within the UI.* 

*Most customer  facing questions  can be answered via a support ticket to support@aquasec.com* if you need an answer to something that you cannot resolve yourself or via the support portal/Knowledge Base articles.

This is the high level view of what you see in the screen shot below. Our Alpine:3.4 image that's been scanned within the console.

*Also highlight to the customer that they can find out about a particular image by clicking on the image name in the UI – as highlighted below with the sky blue text and navy blue comments.*
![Images Screen](https://github.com/kenmccann/advanced-tier-offering/blob/master/image/vulnerabilities.png?raw=true)
We can see that there are 44  vulnerabilities found within the image that are categorised with the following severity & colour :

 - 2 Critical			 
 - 15 High			 
 - 21 Medium	  
 - 6 Low				 
 - 0 Low				 

Additional details about the image can be obtained from the scan results and provide valuable information about the image data obtained during scanning. 

This can be viewed within the UI, via the tabs named below and are hyperlinked to the Aqua documentation page relevant that sub-category.

 - [Vulnerabilties](https://docs.aquasec.com/docs/vulnerabilities-tab)
 - [Layers](https://docs.aquasec.com/docs/layers-tab)
 - [Resources](https://docs.aquasec.com/docs/resources-tab)
 - [Sensitive Data](https://docs.aquasec.com/docs/sensitive-data-tab)
 - [Malware](https://docs.aquasec.com/docs/malware-tab)
 - [Information](https://docs.aquasec.com/docs/information-tab)
 - [Scan history](https://docs.aquasec.com/docs/scan-history-tab)
 - [Audit](https://docs.aquasec.com/docs/audit-tab)

![Image Detail](https://github.com/kenmccann/advanced-tier-offering/blob/master/image/image-detail.png?raw=true)
### Understanding The Scope of Vulnerabilities 

Since the scanned image is marked as compliant aginst the **Default** image assurance policy, we can take a closer look into what vulnerabilities the container image has  within it and how that relates to files and packages. This can be done using the Vulnerabilities tab.
![container image cve list](https://github.com/kenmccann/advanced-tier-offering/blob/master/image/vulns-list-pkgs.png?raw=true)
Aqua will show all the vulnerabilities  within that image by showing the associated packages and files that they belong to.  We  see the  first  few  of columns which shows  the CVE's by name and Severity, which are  Critical  and High  Cve's  for  the  first few rows. 

Clicking on one of the package vulnerabilities in the UI will provide  information related to that vulnerability and what information that the vendor holds about it. 
![container image cve list](https://github.com/kenmccann/advanced-tier-offering/blob/master/image/vendor-cve.png?raw=true)

You can see more  about this in this [link](https://docs.aquasec.com/docs/vulnerabilities-tab#section-description)

It's useful to go through this with the  customer, referring  each of the vulnerability details that are highlighed,  relating to the affected packages  so the customer can gain  valuable insights of the CVE's found and how they might want to think about tackling those by acknowledging and fixing these. 

###  How to approach remediation of vulnerabilities

Your customer  might  want  to [manage and   acknowledge](https://docs.aquasec.com/docs/apply-and-manage-security-issue-acknowledgments)   the vulnerabiltiies which they  have indentified to  work  through.  The  documetnation  link covers  several  sets  of  features  which  can  make  the task  of handling vulnerabilties within  Aqua easier to handle. 
 
There is  also  a section in  our documentation  dedicated to [Reactive Risk Management](https://docs.aquasec.com/docs/reactive-risk-management) -   this covers the  following items:

 - Risk Based Insights
 - Managing  Vulnerabilities
 - Eliminating vulnerabilties by updating  resources
 - Applying a  vShield to a package/image
 - Acknowledging/unackknowleding vulnerabilities
 - Allowing  and Blocking images
 - Assigning  custom severity labels  to selected vulnerabilities
 - Managing Malware
 - Managing Sensitive Data
 - Managing Image Assurance Policiy Violations

### How the "Example" Image Assurance Policy effects the compliance of scan results

![Applied custom image assurance policy](https://github.com/kenmccann/advanced-tier-offering/blob/master/image/alpine-ex-ia-pol-scan.png?raw=true)
Here we can see our  custom Image Assurance  policy applied to our alpine:3.4 image and it's quite different to the results from the default policy. You can see that the image is still compliant  but has failed some  of the  image assurance  controls against Vulnerability  Severity  and  Super User control.

The **Actions Needed**  show the customer what is needed to  remediate the issues are shown. 


## CI/CD Integration

**Session Aim:** Introduce the customer to the Aqua scanner and integrate it into an example CI build pipeline step as part of a base image or application image creation, being part of the SDLC build. (potentially using the customer’s CI tool)

At a high level Aqua can work scan container images in an ad-hoc manner when combined with a variety of CI tools. It is not uncommon for customers or Enterprise to distribute their development teams across different application types and platform architectures, such as Linux x86 64 bit and Windows Server platforms.  

This could mean that an organisation might have a variety of different CI tools, for example a TeamCity CI platform for Windows images and applications and Jenkins or GitLabs for Linux containers and Linux based Apps, or even Azure DevOps.

A list of supported CI/CD integrations is provided [here](https://docs.aquasec.com/docs/cicd-integrations)

Speaking with your customer can give you an understanding of their environment and application landscape before embarking on this task as part of your ongoing workshop.

Build pipelines can be configured to use the scanner for a customer and scan images either using the proprietary Aqua CI tool scanner plug-in or vi[enter link description here](https://docs.aquasec.com/docs/jenkins-image-scanning-integration#section-jenkins-plugin-image-scanning-results)a pipeline step by invoking docker or another supported  container runtime.

1. Show the customer how easy it is to scan an image, [by creating a Jenkins pipeline](https://docs.aquasec.com/docs/jenkins-image-scanning-integration) -   the link  provides  all t he  instructions  to do this and how to use the Aqua scanner Plug-in and parametrise the _Image Name_ as a variable so that any image can be scanned using a Jenkins job by providing build parameters.
2. Demonstrate this pipeline working and explain how this can be used by others in the organisation indirectly without needing to access the Aqua console. I.e., a developer or member of a DevOps team can scan images, as part of the first step to making images compliant.
3. Highlight how Aqua will **_fail_** the pipeline scan if the image being scanned fails the existing Image Assurance policies – you can modify the controls accordingly to show that.
4. Highlight how the image scan results are presented within Jenkins CI as part of the completed job ID and that it’s an HTML representation of the CI/CD scan step which is also present in the Images > CI/CD scans within the UI. This is  covered in the documenation site page  here
5. Using the Image Scan Webhook to send scan results and integrate with [Postee](https://github.com/aquasecurity/postee) to provide image build notifications. 

This provides integration between Aqua and several backend systems where a customer would like their developer team(s) to receive scan results and alerts for images delivered to Slack, Microsoft Teams, Email, ServiceNow & Jira. Additional webhook integrations can be added as well as rules for alerting based on specific image criticality/severity etc.

### Aqua SSO  and  SAML  Integration
Aqua  Enterprise SaaS edition  can  easily be integrated  with  a  number of third  party SSO and SAML based IPD  systems. 
We cover the  supported IDP's  and  configuration methods in our [documentation](https://docs.aquasec.com/docs/saml-authentication-integration#configure-saml-authentication-with-an-idp)  and  you will most likely want  to discuss this with  your customer to get a better understanding  of what their organisational authentication system is  and how they can work beyond having  to configure local user access from the get-go.

There is also  a PDF document *published by the Customer Success team at Aqua* titled "Aqua with Azure AD - SAML.pdf". It explains how  to  integrate  with Active  Directory  which  can be obtiained on request  that helps  most customers to  set  this up.

Customers who integrate SSO/SAML within their deployment, allows them to take advantage of a single authentication mechanism for users of Aqua.  
It also provides capbility to combine the use of application  scopes & permission sets, that are part of the [Aqua RBAC](https://docs.aquasec.com/docs/rbac-overview)  functionality, thus enabling security and developer teams to align group and role authentication for  security auditing, vulnerability managers  and administrator  teams and groups within AD,  giving an additional layer of granularity and access to the images, vulnerabilties and applications  which matter most to them. 

### SIEM and logging  Integration
As we know, customers love looking at data relating their security and workloads. 

Audit data is created from events and displayed in the UI when using the Aqua UI and API.

You can read more about the information we provide about auditing [here](https://docs.aquasec.com/docs/view-audit-events).

Aqua provides numerous options for customers who wish to send their audit event data & scan logs from the console to third party logging systems such as Amazon Cloud Watch, Elasticsearch, Syslog and Webhooks, and SIEM solutions such as Splunk, QRadar, Sumo Logic and other popular tools.

It is likely that your customer will want to discuss this with you. Ask them whether their Security Operations Center (SOC) are using a SIEM platform such as Splunk for monitoring access and security events, generated from infrastructure and workload access.

Our list of supported integrations for logging are provided as well as the list of supported SIEM tools which Aqua supports  [here](https://docs.aquasec.com/docs/external-log-collector)  you can discuss these options with the customer.

We have a best practices page within our documentation regarding SIEM too use that you can read [here].(https://docs.aquasec.com/docs/security-best-practices-integrations#use-a-siem-for-container-logs-for-operational-metrics)

Once you have a clearer idea of the customers logging requirements and use-case, you try and assist the customer with task of integrating this in their environment.
<!--stackedit_data:
eyJoaXN0b3J5IjpbODIwNzAyNTUwLC0xNzQ2NDEwODEzLC0xND
MwODI5NDAzLDE1MzkyNjc0NzgsMTYyMjIwOTY5NiwtMTUzNjE3
ODk4OSwxNTM2MDk4NTMwLC02Nzk1OTU4NTEsNDM2OTQzMTI3LD
E1NjIzOTQwMDgsLTE2MzMwNTA5NDYsLTE3MDAxMzAzNjYsODA2
ODE3NjE0LC00NDAwODgxNSwtNzk1ODcwMjc1LDIwMDc2MDQ3NT
YsLTE3MTY4OTMzMzIsMTQ4OTI5MTU1LDIwMjk2NzkwNCwtMTY1
MTQ3NzM0MF19
-->