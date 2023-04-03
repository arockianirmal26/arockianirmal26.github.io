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
After the above step you need to verify your email address with a one time password which will be sent to your root email address.<br> 

<b>Step 1</b>: After the email verification, you are asked to create a password for a root user. AWS requires that your password meet the following conditions: It must have a minimum of 8 characters and a maximum of 128 characters. Make sure to create a strong password with special characters.<br>  

<b>Step 2</b>: Here you will asked for your contact information and your usage type (choose Personal- for your own projects).<br>  

<b>Step 3</b>: Now its time for entering your billing information. Your credit/debit card will be validated in this step. <br> 

<b>Step 4</b>: Your identity will be confirmed in this step. You could opt to receive either a text message or a voice call.<br> 

<b>Step 5</b>: You will be asked to select a support plan. It is recommended to opt for 'Basic support - Free' plan for new users who are just getting started with AWS.<br>  

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

<p>
When setting up a new AWS account, you create a root user account. The root user is a special entity that has full access to the account, and can perform all actions, including changing the payment methods or closing the account. Due to this level of permissions, set up additional users to perform daily tasks related to your account. It is recommended that you create separate users for specific roles and functions.<br> 
Again, we'll use the IAM service to create users and assign them permissions. Before setting up a new user, we'll create a user group. User groups let you specify permissions for multiple users, which can make it easier to manage the permissions for those users. For example, you could have a user group called Admins and give that user group typical administrator permissions. Any user in that user group automatically has Admins group permissions.<br> 
In the IAM console, choose User groups in the left-side navigation and then choose Create group. Enter the User group name (in this case, Admins), then scroll down to the Attach permissions policies section. Search for "AdministratorAccess", then select the box next to the policy with the name "AdministratorAccess", scroll down, and choose Create group.
Once the user group has been created, select Users in the left-side navigation bar and then choose Add users and link it with the user group like below.<br> 
</p>

![Create Admin User](/assets/1/admin_user1.png)
_Create Admin User_

![Assign Admin Group](/assets/1/admin_user2.png)
_Assign Admin Group_

<p>
Once you review and create the new user, the console sign-in details will be shown which includes URL, username and password. Don't forget to secure this user too with MFA.
</p>


<h1>Setup account alias</h1>

<p>
Let's set an alias for your account, which should be easier to remember than the 12-digit account ID. To set it, navigate to the Identity and Access Management (IAM) dashboard. Find the account ID on the right-hand side and click Create or Change under the AWS account alias. This alias needs to be globally unique across all AWS accounts, so your first choice may not be available.
</p>


<h1>Change payment currency preference</h1>

<p>
This prevents our card issuer to charge a fee for transactions in other currencies. Click your Account Name (Top Right) -> Account to find the section Payment Currency Preference.
</p>

![Currency Preference](/assets/1/currency.png)
_Currency Preference_


<h1>Update security challenge questions</h1>

<p>
Improve the security of your AWS account by adding security challenge questions. AWS use these to help identify you as the owner of your AWS account if you ever need to contact AWS customer service for help. Click your Account Name (Top Right) -> Account to find the section Configure Security Challenge Questions.
</p>


<h1>Setup default region/language</h1>

<p>
Click your Account Name (Top Right) -> Account to find the section Unified Settings where you set the default region and language. Setting default region isn't just an issue for newbies, it would save a lot of mini heart attacks when people log in to an account and think they're missing resources, only to find out they're in the wrong region!
</p>


<h1>Set up the AWS CLI</h1>

<p>
The AWS CLI is a unified tool to manage your AWS services. With just one tool to download and configure, you can control multiple AWS services from the command line and automate them through scripts. <br> 
Go to IAM -> Users -> (newly created user) -> Under 'Security Credentials' go to 'Access Keys' -> 'Create Access Key'. In the next window 'Access key best practices & alternatives' choose 'Command Line Interface (CLI) ' and then create the access key (adding Tags is optional). Now save the access key and the secret access key (download the .csv file). Follow the instructions below to install the CLI based on your OS.
</p>

**[AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)**.

<p>
once the installation is complete, we could confirm the installation using the version command in the terminal/powershell (windows) like below and you would see a version number.
</p>

```shell
aws --version
```
{: .nolineno }

<p>
To configure the credentials, use the following command in the CLI and add the access key ID and secret access key credentials of the user created earlier. You also need to mention the default region name. The default output format can be json.
</p>

```shell
aws configure
```
{: .nolineno }

<p>
After this you could run the aws ec2 describe-vpcs command to check if the configuration is correct. Each new AWS account has default VPCs configured. In the output section, you can view the VPCs in your AWS account.
</p>

```shell
aws ec2 describe-vpcs
```
{: .nolineno }


<h1>Billing alerts/alarm</h1>

<p>
Search for 'Billing' in AWS home. You would land in AWS Billing Dashboard. In the navigation pane, choose Billing Preferences under Preferences. Select Receive Billing Alerts And click save preferences. You could also select 'Receive PDF Invoice By Email' and 'Receive Free Tier Usage Alerts' if needed. Now the billing alerts are enabled.<br> 
Billing metrics are located in us-east-1 region. Make sure the Console is switched to that region by selecting US East (N. Virginia) us-east-1 in the region selector (top right corner, next to Support button).<br> 
Follow the instructions below to create/delete an alarm. In my case I set an alarm when the overall costs goes more than 10 Dollars.
</p>

**[Billing Alarm](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/monitor_estimated_charges_with_cloudwatch.html)**.


<h1>Best practices & Recommendations</h1>

<ul>
  <li>Rotate all your access key pairs / root user passwords regularly</li>
  <li>Limit the tasks you perform with the root user (creating an administrative user, change account settings and closing AWS account etc.) More details are in the link below. Never create access keys for the root user. If you need to have one then rotate access keys regularly</li>
  <li>When creating IAM users make sure that the IAM users have the most restrictive policies possible, with only enough permissions to allow them to complete their intended tasks</li>
  <li>Frequently audit your IAM roles/Policies</li>
  <li>To protect secrets in AWS, configure them in AWS Secrets Manager, then insert a descriptive reference to them in the application code. For example, the password for a production database can be stored in Secrets Manager and named my_db_password_production.
Use AWS Cost Explorer which enables you to view and analyze your costs and usage. Using the Cost Explorer user interface is free of charge</li>
  <li>Make use of AWS Free Tier</li>
  <li>Use Tags to organize resources and to track you AWS costs on a detailed level</li>

</ul>


