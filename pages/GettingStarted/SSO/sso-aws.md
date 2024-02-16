---
title: AWS SSO Integration
keywords: sso, setup, onboarding
tags: [onboarding, sso]
sidebar: mydoc_sidebar
permalink: sso-aws.html
folder: GettingStarted
series: [Onboarding, SSO]
weight: 1.0
---

# How to use AWS SSO for nOps #


In the nOps platform, [navigate to the SSO Configuration settings](https://app.nops.io/v3/settings?tab=SSO) to enable SSO


 **Steps to configure AWS SSO integration with nOps**


- **Prerequisites:** 

1. You must be logged in to your nOps and AWS management account account. 

2. IAM Identity Center must be enabled.

- **About AWS SSO:** 

AWS SSO (Amazon Web Services Single Sign-On) is a service offered by Amazon Web Services (AWS) that simplifies access management for AWS accounts and business applications. It is designed to centrally manage user access, permissions, and authentication across multiple AWS accounts and third-party applications.

- **Using AWS SSO with nOps**

It’s now quick and easy to integrate SSO from your preferred SAML 2.0 provider, for enhanced security and simplified access management. Here are the steps. 

**Steps to configure**

Note: We suggest that you keep both the AWS and nOps platform open in the same browser to switch between during the steps. 

**Step1: Create an Application with SAML 2.0 configuration.**

- Within your AWS Platform, Navigate to **IAM Identity Center → Applications → Add Application**

- Select **I have an Application I want to set up**

- Select **Application Type: SAML 2.0**

- Provide a suitable **Display name** & **Description** to configure
<br>
![](https://lh7-us.googleusercontent.com/_Ej88Q-JIC0kMqVsoVWw_23ISVqrx4Bi-nJdchpkGk1DAiVn2KrP3oKspgVjPK5U0rTLr8ZIrvQvDTtv6FYShp0N1X9IDWk-42L6plr5BUmH28aUz8VvlNtSQZ5EGInpsFRvIUxZBXXe1oXjGcHXnFY)
<br>

**Step2: On the nOps platform, and navigate to Organizational Settings → SSO to Enable SSO.** 
<br>
![](https://lh7-us.googleusercontent.com/wp4Od6Ghlklv2C7edo1WyxfU92n-HI2iBRFESJ2TVix5lOiHB-XGjaIABSxqAptAeM2NQR0YByDtrbS-MPGYc6VodSYdqRpR1b_ROCpGRH9n5jSkAbtiwJ4VjNQC1hTXec2HcVbkOnbzBIv-mo7XUTo)
<br>

**Step3: Perform the following steps on the AWS platform where Application creation is in progress.**

-Copy the **IAM Identity Center SAML Issuer URL** from AWS. In the nOps platform browser tab, paste the URL into the fields: **Issuer URL (entityId)** & **SAML 2.0 Endpoint (HTTP) (singleSignOnService: URL)**

-Copy the **Assertion Consumer Service URL** from **nOps** **SSO Integration Details** and paste it into  **Application ACS URL**.

-Copy the **Entity ID** from **nOps SSO integration Details** and paste it into the  **Application MetaData** field **Application SAML audience**
<br>
![](https://lh7-us.googleusercontent.com/73lg69U2gUGKpd-afGO8vZN_GWZX6F9Cwr8_-eJCzcILWc-R4mHpSV27F4Zm23mnFJ6lJwN8kfafG7fFRampimPZIVjNApjoRV7OPMgm4lXsVRXKJi8sOYLSy5eNOIsgc1cYS86pwyZ5uXMkfNxO8s4)

<br>

**Step4: Download the IAM Identity Certificate**


- Switch to the AWS platform and download the IAM Identity Certificate

- Open the IAM Identity Certificate into a text editor such as Notepad 

- Copy the Certificate data and paste it into the **nOps platform** **→** **Organization Settings** **→** **SSO** **→** **Your** **SSO** **Details** section field: **X.509 Certificate**
<br>
![](https://lh7-us.googleusercontent.com/n32Id8ZKiboWjKWQaTVtHj-X4KeKsPbI-Gz88thJOh3vpdCg5r9k4SztuB-DykdqbNxZFHxBKtRRaz8TLEfJPvQQ7eKuTO8PYEkrit0FgF5SZYSA-NR0BR5lwbLU986ZQaZQHU8ZIb0wxdSry9p71_M)

<br>


**Step5: Create an Application in the IAM Identity Center with filled configuration details and configure Attribute mappings.**

- Click on the **Actions** button and then in **Edit attribute mappings** in an Application to configure **Attribute Mappings** for the nOps Application.

- Add the below mentioned attributes and save changes.

|                 |                    |              |
| --------------- | ------------------ | ------------ |
| **Application** | **Maps**           | **Format**   |
| Subject         | ${user:subject}    | emailAddress |
| User.Email      | ${user:email}      | basic        |
| User.FirstName  | ${user:givenName}  | basic        |
| User.LastName   | ${user:familyName} | basic        |

<br>

![](https://lh7-us.googleusercontent.com/39XtfaWyScJVMNsBmdr_xM4sGSEJkj9IKEEbWAl45x-cbrSZgHSZ_43UK-jKloIwg44qYtD2v866xskEjlvY4bp0Wzmh3MGXTy5HwKu5Fo7w8TVnbNtjPQJ-9Mq6vQ3dTRzCKhWB6x2Dao28wnwV1EQ)

<br>

**Step6: Provide default roles in the nOps platform.**

- Navigate to **Organization Settings** **→** **SSO** and select **Default roles** for your User/Groups.

- Click on **Setup SSO Configuration**.

![](https://lh7-us.googleusercontent.com/0OHLPR0GJgJETZ_M65UdiZ-0sT_xf4-eoNxhSr8AgBdDbfF9pimUntFDJ9O1-NXpiqaMjFOLMZ6BxIrs2mMcpSJCR8om7yeVg0Aux9h1uNHyPsstuBk9H-w1wb0dRYNbo4VuF3lf3xR8S7iRkbvQI48)

<br>

**Step7: Switch to AWS IAM Identity Center to Create Groups and Users, and assign them in the nOps Application.** 

- Navigate to **Groups** in the left panel of the **IAM Identity Center**

- Create a **Group** and provide **Group details**

- Create **Users** in the left panel of the **IAM Identity Center** and add these users to the created **Group**.

- Redirect to **Application → Application → Customer Managed →** open **nOps Application** and **Assign Users or Group** to this Application.

<br>

![](https://lh7-us.googleusercontent.com/jwYMhP04aclYsPhm__PLhRphXMg7G-QYY-5AzsTsbVAPNEOoIY6D7ib-ynCoGDFQ9YJaU0rPvP1LlkGBGoUC1_fqOelnNqYyGH3RhDzCXECT_a_pnf4GVkCCDHVLpwRBQZgoal727MstiTVyVRLqTA4)

**Note**: Ensure user access and user status are enabled.

**Step8: Accept the Invitation in your \[added users in nOps application] email received from AWS with the subject: Invitation to join AWS IAM Identity Center (successor to AWS Single Sign-On).**

- Accept the invitation received on your email as shown below.

- Using the AWS access portal URL given in the email, set up the credentials **\[note: use the given username in the email]**

- Once you set up the credentials, you will be redirected to the AWS portal where you can view the created **nOps Application** 



![](https://lh7-us.googleusercontent.com/vE_zj6Dp52B-D8_dqQCBhYIWOtGRq3dNw_BZs3K5SML_0KjfyGBr1w5H8XtrvO9SZ7083TU8tuCmQVK5mLJpdRWss7CwPEM5T2oeRbFv8FnitmriPaRO2MMEtKHJ2NUpu_YkhTplN5pqYU4aC4f0AfI)

<br>
<br>
- Click on the nOps Application to be redirected to the nOps platform with no Sign-in required. 

<br>


![](https://lh7-us.googleusercontent.com/iVs_UcQNc_OCh1zy2EzotOUSxB3ZpcMUl-86YMC9L8cgLq5V1uIRakKRFCdR-sh6BmMh5up3yyN11SLj5sAvpfJiwJIJ0TBKlS7k9Wb-5CEOWH5pfrT_k4jiYxNKJI5Cl2iVdIaFRMECFgAPmY6w5yk)

**Step9: You will receive an email confirming that you wish to allow SSO access.** 

![](https://lh7-us.googleusercontent.com/SXmg4bNvn-eFRGPRvxr7COdWsI0PyYZnNF2hif5lbueM-nSw-Jj3AlSXe8F3kCLVwmSE22JWBzfWAxIutcJC-KD66X1uxkaZkBMvaQC_QqVWn0AvfPLCi4t0CYwLMXoUVrMldyVS8VtBRXqGsGXczcg)

**Step10: You will be able to use the AWS access portal URL given in the email to directly access the nOps Application.** 








<br/><br/>

{% include custom/series_related.html %}



