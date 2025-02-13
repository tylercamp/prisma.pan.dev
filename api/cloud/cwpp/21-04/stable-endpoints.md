---
id: stable-endpoints
title: Stable Endpoints
sidebar_label: Stable Endpoints
---

Starting with 21.08, with every release the Compute APIs will be versioned to indicate the release number to which they correspond. 
The version-specific APIs will be supported for the subsequent two major releases. 
With API versioning, as your Console is upgraded to newer versions, you can continue to use older versioned APIs with stability and migrate to newer version APIs at your convenience within the N-2 support lifecycle. 
The deployment scripts and Twistcli that you download from Console, will use the Prisma Cloud Compute APIs associated with the specific version of Console. 
For example, the 21.08 release that is codenamed Iverson will be supported through the next two releases codenamed Joule and Kepler. When Langrage ships, the 21.08 API will no longer be supported. 


## Versioning

The Compute API is versioned as follows:

`/api/vX/route`

Where:

* `v1` - Always points to the latest API.
* `vVersion` - Points to a version-specific API, where `Version` specifies the major and minor parts of a release's version string.

For example, the following endpoint points to a 21.08 endpoint:

`api/v21.08/images`

As a best practice, update your scripts to use the version-specific API endpoints to ensure that your implementation is fully supported.
For the version-specific APIs, you will have access to the API Reference and Release Notes documentation for changes or updates that may impact you. 

When using the version-specific endpoints, you will need to update your automation scripts approximately once-a- year to stay in sync with the product [support lifecycle]( https://docs.paloaltonetworks.com/prisma/prisma-cloud/prisma-cloud-admin-compute/upgrade/support_lifecycle.html).

**Note**: If you have a mixed environment  of 21.08, 21.12, and 22.04 Defenders then use the version of the API that matches the earliest version, which in this example is API v/21.08.

If you use the /v1 APIs, Palo Alto Networks recommends that you consider revising your scripts to target the versioned API endpoints. 
If you opt to continue using the v1 API endpoints, please adhere the following practices guidelines:
* Review the list of v1 endpoints you are using and make sure the corresponding versioned endpoints are available.
v1 API are a larger subset and not all endpoints are supported. 
Only the versioned endpoints are supported and automatically mapped to the latest   release of the product.
* If you are using an API that is only in the /v1 category and does not have a corresponding versioned API, you must review your implementation and update your scripts to adapt them to ensure that you do not  experience a disruption.
* If you are using  /v1 endpoints that are not versioned and thereby are unsupported, you can submit a feature request. 
Your request for supporting the endpoint will be considered when planning the product roadmap for future releases.


## Supported Endpoints

The API Reference documentation for the Compute APIs includes the supported endpoints only.
From the Prisma Cloud Compute Console you can download a copy of the OpenAPI spec file.
This file lists all available endpoints, including unsupported endpoints. 
Use the supported endpoints for ensuring stability. 
Because the unsupported endpoints are not documented for use, they are subject to change, deprecation, or removal without notice.

In the OpenAPI spec, supported endpoints are tagged as supported.
For example, the `POST /api/vX/authenticate` endpoint is tagged as follows:

```
"tags": [
  "Authenticate",
  "Supported API"
]
```

## Supported Endpoint Categories

Supported endpoints tend to fall in one of the following categories:

* Reporting endpoints
* Config-as-code
* Deployment and config


### Reporting Endpoints

Reporting API calls are the ones used to download health or scan data such as vulnerabilities/compliance/runtime.   
Access to the underlying data in JSON and CSV formats allows customers to easily access and transform data into business intelligence in the forms that meet their needs.  
The output may be human-readable reports or, in other cases, the reporting data may feed automated decisions and processes.

These are mostly under **Monitor** section in the Compute Console.


### Config-as-Code

Configuration as code is the formal migration of config between environments, backed by a version control system. 
Customers who want to programmatically store and manage the configuration of infrastructure components, can utilize these to automate these components using the same approaches that they've used for production code and services. 


### Deployment and Config

Deployment and config endpoints are essential for properly being able to automate the installation of Console, Defenders, as well as any configuration that deals with integrations.  
These are useful to those who base their management of environments on automation, using tools such as Ansible, Puppet, Terraform etc to define desired configurations.
