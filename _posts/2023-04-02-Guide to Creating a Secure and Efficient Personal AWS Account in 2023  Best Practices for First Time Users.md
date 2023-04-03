---
title: Guide to Creating a Secure and Efficient Personal AWS Account in 2023 - Best Practices for First-Time Users
date: 2023-04-02 09:54:50 +/-TTTT
categories: [Tech, AWS_Account_Creation]
tags: [aws]     # TAG names should always be lowercase
---
<p>
Amazon Web Services (AWS) is a cloud computing platform that offers a wide range of services, including compute power, storage, and databases, as well as tools for machine learning, security, and more. Opening an AWS account is a simple process, but it's important to follow best practices to ensure that your account is secure and your resources are optimized for cost and performance. In this blog, I'll walk you through the steps of opening an AWS account and provide you with some key best practices to help you get started on the right foot. 
</p>


![Overview](/assets/1/new_aws.jpg)
_Overview_

<h1>Content of this Article</h1>

<ol>
  <li>Sign up for an AWS account</li>
  <li>Login as a root user & secure(MFA) root user</li>
  <li>Create an Admin user with required permissions</li>
  <li>Setup account alias</li>
  <li>Change payment currency preference</li>
  <li>Update security challenge questions</li>
  <li>Setup default region/language</li>
  <li>Set up the AWS CLI</li>
  <li>Billing alerts/alarm</li>
  <li>Best practices & Recommendations</li>
</ol>

<h1>Sign up for an AWS account</h1>

<p>Signing up for an AWS account is a 5 step process. The process can be started with the following link </p>

**[Sign up for AWS](https://portal.aws.amazon.com/billing/signup#/start/email)**.

<p>
In the initial step, you will be asked for a root user email address and an account name. Root user must be strictly used only for administrative functions like account recovery, billing etc. For developing/using services in AWS, it is always recommended to create separate users with minimal or required privileges. We will create an Admin user later in this article.
After the above step you need to verify your email address with a one time password which will be sent to your root email address.

__Step 1__: After the email verification, you are asked to create a password for a root user. AWS requires that your password meet the following conditions: It must have a minimum of 8 characters and a maximum of 128 characters. Make sure to create a strong password with special characters.  

__Step 2__: Here you will asked for your contact information and your usage type (choose Personal- for your own projects).  

__Step 3__: Now its time for entering your billing information. Your credit/debit card will be validated in this step.  

__Step 4__: Your identity will be confirmed in this step. You could opt to receive either a text message or a voice call.  

__Step 5__: You will be asked to select a support plan. It is recommended to opt for 'Basic support - Free' plan for new users who are just getting started with AWS.  

Congratulations you are now successfully created your personal AWS account! Now we will perform some essential setups and also secure your AWS account.
</p>

<h1>Login as a root user & secure(MFA) root user</h1>

<p>
Once the account has been created, you might be redirected to the login page where you can login again as a root user. 
In order to secure the root user we need to add MFA(Multifactor Authentication) for the root user. Search for IAM in the home page of the AWS management console and open IAM dashboard.
</p>

![Secure User with MFA](/assets/1/MFA_Root.png)
_Secure User with MFA_

<p>
Under 'security recommendations' click 'Add MFA' and follow the instructions. For example you could use Google/Microsoft authenticator in your smartphone for this purpose. Also make sure that the root user have no active access keys since root user will not be used to perform daily tasks.
</p>

<h1>Create an Admin user with required permissions</h1>

<h1>Setup account alias</h1>

<h1>Change payment currency preference</h1>

<h1>Update security challenge questions</h1>

<h1>Setup default region/language</h1>

<h1>Set up the AWS CLI</h1>

<h1>Billing alerts/alarm</h1>

<h1>Best practices & Recommendations</h1>


