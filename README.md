# SERVICE PRINCIPAL AND DEVOPS SERVICE CONNECTION: SCHEMA

Greetings my fellow Technology Advocates and Specialists.

In this Session, I will provide you real-time insights including food for thoughts on __Service Principal and DevOps Service Connection Schema__. 

| __IMPORTANT TO NOTE:-__ |
| --------- | 
| Here in this reference blog, we talk only about __Service Principal(s) which are created with the sole purpose of __Creating DevOps Service Connection(s) used for Running Pipelines for Infrastructure Deployment (IaC).__ |
| In most establishment(s), every project which is onboarded to cloud has its own Subscription (Per Environment - NonProd and Prod) and DevOps Project. |
| The DevOps Project will then have its own Service Connections for below - 1) __Running Pipelines for Infrastructure Deployment (IaC)__, and 2) __Running Pipelines for Application Deployment on the deployed Azure Services (by IaC).__ |


| __QUESTION HERE IS:-__ |
| --------- |
| Should we have - 1) __One Service Principal Per Project &  Environment (NonProd and Prod)__, or 2) __One Service Principal Per Project__ 3) __One Service Principal for All Projects.__ |


| __SCHEMA #1:-__ |
| --------- |


| __ONE SERVICE PRINCIPAL PER PROJECT AND ENVIRONMENT APPROACH:-__ |
| --------- |


| __PROJECT NAME__ | __ENVIRONMENT__ | __SERVICE PRINCIPAL NAME__ | __DEVOPS SERVICE CONNECTION NAME__ |
| --------- | --------- | --------- | --------- |
| Project A | NONPROD (Dev) | am-projectA-nonprod-dev-infra-spi | am-projectA-nonprod-dev-infra-spi |
| Project A | NONPROD (UAT) | am-projectA-nonprod-uat-infra-spi | am-projectA-nonprod-uat-infra-spi |
| Project A | PROD | am-projectA-prod-infra-spi | am-projectA-prod-infra-spi |
| Project B | PROD | am-projectB-prod-infra-spi | am-projectB-prod-infra-spi |


| __NOTE:-__ |
| --------- |
| Below is the Naming Convention for Service Principal and Azure DevOps Service Connection used in the Reference Example. __Both have Same Name.__ |
| __Establishment Name_Project Name_Environment Name_Category_Type___ |


| __RELEVANT SCREENSHOTS__:- |
| --------- |
| __All Service Principals relevant for Schema #1:-__ |
| ![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/frbmtr074u269vqmljnq.jpg) |
| __Service Connection(s) for DevOps Project A:-__ |
| ![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/d7rh5cetnxaioha9e7bd.jpg) |
| __Service Connection(s) for DevOps Project B:-__ |
| ![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/fa3anbqppqmds7ek0s87.jpg) |


| __PROS:-__ |
| --------- |
| If Service Principal is accidently deleted, only One Project and One Environment is affected. |


| __CONS:-__ |
| --------- |
| Multiple Individual Service Principal Management Per Environment - 1) Secret Expiry, 2) Key Vault Update Post Secret Renewal (Create a New Version, Disable Previous Version).
| Inventory Management. |
| Similar and Repetitive Microsoft Graph API rights (With Admin Consent) needs to be configured and applied to Service Principal Per Project and Environment. |


| __SCHEMA #2:-__ |
| --------- |


| __ONE SERVICE PRINCIPAL PER PROJECT APPROACH:-__ |
| --------- |


| __PROJECT NAME__ | __ENVIRONMENT__ | __SERVICE PRINCIPAL NAME__ | __DEVOPS SERVICE CONNECTION NAME__ | NOTES |
| --------- | --------- | --------- | --------- | --------- |
| Project A | NONPROD (Dev) | am-projectA-infra-spi | am-projectA-nonprod-dev-infra-spi | Secret is same for all environments (Dev, UAT and Prod) for each project. |
| Project A | NONPROD (UAT) | am-projectA-infra-spi | am-projectA-nonprod-uat-infra-spi | Secret is same for all environments (Dev, UAT and Prod) for each project. |
| Project A | PROD | am-projectA-infra-spi | am-projectA-prod-infra-spi | Secret is same for all environments (Dev, UAT and Prod) for each project. |
| Project B | PROD | am-projectB-infra-spi | am-projectB-prod-infra-spi | Secret is same for all environments (Dev, UAT and Prod) for each project. |


| __NOTE:-__ |
| --------- |
| Below is the Naming Convention for Service Principal and Azure DevOps Service Connection used in the Reference Example.__ |
| Service Principal Name = __Establishment Name_Project Name_Category_Type__ |
| DevOps Service Connection Name = __Establishment Name_Project Name_Environment Name_Category_Type__ |


| __RELEVANT SCREENSHOTS__:- |
| --------- |
| __All Service Principals relevant for Schema #2:-__ |
| ![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/yssf761hz2mi2gyuspr4.jpg) |
| __Service Connection(s) for DevOps Project A:-__ |
| ![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/9zfshl9v1jxirytk8i4k.jpg) |
| __Service Connection(s) for DevOps Project B:-__ |
| ![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/mbd23mxy7ztxuzvm61nn.jpg) |


| __PROS:-__ |
| --------- |
| If Service Principal is accidently deleted, only One Project (All Environments - Dev, UAT and PROD) is affected. |

| __IMPORTANT FACT:-__ |
| --------- |
| __Risk is Higher as compared to Pros of Schema #1__ |


| __CONS:-__ |
| --------- |
| Multiple Individual Service Principal Management Per Environment - 1) Secret Expiry, 2) Key Vault Update Post Secret Renewal (Create a New Version, Disable Previous Version). | 
| Inventory Management. |
| Similar and Repetitive Microsoft Graph API rights (With Admin Consent) needs to be configured and applied to Service Principal Per Project. |

| __IMPORTANT FACT:-__ |
| --------- |
| __Effort is Little less as compared to cons of Schema #1__ |


| __SCHEMA #3:-__ |
| --------- |


| __ONE SERVICE PRINCIPAL FOR ALL PROJECT APPROACH:-__ |
| --------- |


| __PROJECT NAME__ | __ENVIRONMENT__ | __SERVICE PRINCIPAL NAME__ | __DEVOPS SERVICE CONNECTION NAME__ | NOTES |
| --------- | --------- | --------- | --------- | --------- |
| Project A | NONPROD (Dev) | am-infra-spi | am-projectA-nonprod-dev-infra-spi | Individual Secret is Per Project and environments (Dev, UAT and Prod) within the Same Service Principal. |
| Project A | NONPROD (UAT) | am-infra-spi | am-projectA-nonprod-uat-infra-spi | Individual Secret is Per Project and environments (Dev, UAT and Prod) within the Same Service Principal. |
| Project A | PROD | am-infra-spi | am-projectA-prod-infra-spi | Individual Secret is Per Project and environments (Dev, UAT and Prod) within the Same Service Principal. |
| Project B | PROD | am-infra-spi | am-projectB-prod-infra-spi | Individual Secret is Per Project and environments (Dev, UAT and Prod) within the Same Service Principal. |


| __NOTE:-__ |
| --------- |
| Below is the Naming Convention for Service Principal and Azure DevOps Service Connection used in the Reference Example.__ |
| Service Principal Name = __Establishment Name_Category_Type__ |
| DevOps Service Connection Name = __Establishment Name_Project Name_Environment Name_Category_Type__ |


| __RELEVANT SCREENSHOTS__:- |
| --------- |
| __All Service Principals relevant for Schema #3:-__ |
| ![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/xgsvu8pp4npgkpg6etmo.jpg) |
| __One Service Principal, Multiple Secrets Per Projects and Environments__ |
| ![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/kpok3hrewj70zhqpha9r.jpg) |
| __Service Connection(s) for DevOps Project A:-__ |
| ![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/pitv2j0ir3rbm35tutbt.jpg) |
| __Service Connection(s) for DevOps Project B:-__ |
| ![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ph0jrdfdlem04xljbbp6.jpg) |


| __PROS:-__ |
| --------- |
| Service Principal Management (Secret Expiry) is much easier as all resides under the Same Service Principal. |
| No Overhead of Inventory Management. |
| No Similar and Repetitive Microsoft Graph API rights (With Admin Consent) needs to be configured and applied as there is only one Service Principal for all Projects. |


| __IMPORTANT FACT:-__ |
| --------- |
| __Effort is Much less as compared to cons of Schema #1__ |


| __CONS:-__ |
| --------- |
| If Service Principal is accidently deleted, All Projects and All Environments (Dev, UAT and PROD) in Each Project gets impacted at once. |


| __IMPORTANT FACT:-__ |
| --------- |
| __Risk is Much Higher as compared to Pros of Schema #1 and Schema #2__ |


So, in conclusion, it completely depends upon Azure Solutions and DevOps Architects of the Establishment which Schema/Schemas they would like to implement for Project(s) or across Project(s).

__Hope You Enjoyed the Session!!!__

__Stay Safe | Keep Learning | Spread Knowledge__
