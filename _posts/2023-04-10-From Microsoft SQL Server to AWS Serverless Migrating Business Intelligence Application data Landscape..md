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

![New Architecture](/assets/2/new_setup.jpg)
_New Architecture_
