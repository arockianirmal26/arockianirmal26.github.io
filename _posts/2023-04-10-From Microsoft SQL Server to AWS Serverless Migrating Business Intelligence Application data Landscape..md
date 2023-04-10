---
title: From On-Prem Microsoft SQL Server to AWS Serverless - Migrating Business Intelligence, Application data Landscape
date: 2023-04-09 09:54:50 +/-TTTT
categories: [Tech, AWS_Data_Architecture]
tags: [aws]     # TAG names should always be lowercase
---


<h1>Introduction</h1>

<p>
In today's fast-paced business world, companies are constantly seeking ways to streamline their operations, increase efficiency, and reduce costs. One way to achieve these goals is by leveraging the power of cloud computing and serverless technologies. This was the case for a company that I was working for and had been using Microsoft SQL Server, SSIS ETL tool and Reporting Services for their business intelligence/internal application needs. <br>
In this blog post, I will summarize how we successfully migrated the complete business intelligence (OLAP) and application (OLTP) databases setup to AWS serverless services, including Amazon Aurora RDS, Lambda, Event Bridge, Glue, S3, Redshift and Quick Sight. In this post I summarise high level details about the architecture and the process.
</p>

<h1>Old Architecture (On-Premises)</h1>

![Old Architecture](/assets/2/old_setup.jpg)
_Old Architecture_

<p>
In the company we mainly had two categories of data, the first set is the worldwide sales/product data which is refreshed every morning and available as flat files in the company intranet which is available to the subsidiaries worldwide. The second set is the local sales data from the European subsidiary. <br>

<b>Part 1 </b>: A python script is scheduled using windows task scheduler on a on-prem windows server. Every morning this script downloads the worldwide sales/product data flat files from the intranet and places in the same on-prem windows server of our European subsidiary. Once the flat files are arrived in the folder, the SSIS ETL packages will get triggered. <br>

<b>Part 2 </b>: The SSIS ETL packages will now read the flat files, transform and load the product metadata/worldwide sales data  into the European SQL Server staging database. The product metadata is used by the European sales website as well as by the CRM. The sales data is used for analysis purposes.

 <br>

<b>Part 3 </b>: The data in the staging database is further transformed into Facts and dimensions and are available as base tables for reporting. Once the ETL jobs are completed the internal employees are notified with an email and they can access the business intelligence/sales SSRS reports. 


<h3>Drawbacks of the above architecture:</h3>

<ol>
  <li>Though we enjoyed full ownership of the data infrastructure on-premises, over the period of time we noticed performance degradation since the data we process everyday increased exponentially. Scalability and performance became major concern.</li>
  <li>We always relied on an expert freelancer consultant who set up the data infrastructure to analyze and fix the infrastructure issues.</li>
  <li>Security patches and upgrades must be done manually which further complicated the maintenance </li>
  <li>Increasing costs for the hardware and licenses were also an additional issue </li>
</ol>

</p>


<h1>New Architecture (AWS Serverless)</h1>

<p>
Considering the above drawbacks, we decided to move the complete data landscape to AWS. Given the knowledge bases and documentation available online we decided to first build a PoC. We could able to successfully negotiate with the management with the PoC. Below is the rough illustration of the new architecture we developed over the time. 
</p>

![New Architecture](/assets/2/new_setup.jpg)
_New Architecture_

<p>

<b>Part 1</b>: We created and scheduled a Lambda function using Eventbridge which would download the required flat files every morning and put into the Raw bucket in our S3 Datalake. <br>
<b>Part 2</b>: Once the files are in the Raw bucket, a Glue ETL job will be triggered which will refine the data in the flat files. For example, here we copy only the required columns from Raw to Refined stage. <br>
<b>Part 3</b>: Once the files are in the Refined bucket, another set of Glue ETL jobs will be triggered which will transform the data and copy the required data rows into Aurora Serverless RDS, Redshift serverless and Reporting S3 bucket. To reduce the costs, we periodically unload cold data defined by our business departments into Refined S3 bucket.<br>
<b>Part 4</b>: Aurora Serverless RDS is our OLTP database which is used by our Sales Apps and CRM which now contains the European sales and customer data. For our datawarehousing and analysis/reporting purposes we move the necessary data from the OLTP database to Redshift on a hourly basis using another set of Glue ETL jobs. <br>
<b>Part 5</b>: We have a set of reports in Quicksight that connects with Redshift datawarehouse and S3 reporting bucket. To query the data from S3 we leverage the features of Glue crawler, data catalog and athena. <br>
<b>Initial Database Migration</b>: We performed our initial database migration with AWS Database Migration Service and Schema Conversion Tool. DMS features like data validation and setting up ongoing replication from source target enabled smooth transition. Earlier we used SQL Server both as OLTP and OLAP databases but now we have Aurora as OLTP and Redshift as OLAP. <br>

<h3>Best Practices & Things we gained after moving to AWS</h3>

<ol>
<li>The main advantage for us is the flexibility in terms of cost and scalability. We are now aware of our exact expenses for each AWS service, which inturn helps us fine tune our use cases. We have also set up database auto scaling policies based on usage</li>
<li>We always offloaded the read traffic from the main writer database instance by having a separate read only instances which boosted the performance further</li>
<li>Database backups & replications are easier to setup</li>
<li>We started using Infrastructure as Code with Terraform to provision AWS resources and version controlling for our data infrastructure</li>
<li>Since we opted for mostly serverless services, now we worry no more about managing the hardware</li>
</ol>

<br><br>

Migrating to AWS was the best decision made by the company and they are now exploring many new AWS services like EMR, Sagemaker etc., to dive deep into the data to extract insights from the data. Thanks for reading the article and feel free to add comments or write me about your thoughts!  

</p>
