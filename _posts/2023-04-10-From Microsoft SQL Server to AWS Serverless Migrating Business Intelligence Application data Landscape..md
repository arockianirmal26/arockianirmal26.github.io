---
title: From Microsoft SQL Server to AWS Serverless - Migrating Business Intelligence, Application data Landscape
date: 2023-04-09 09:54:50 +/-TTTT
categories: [Tech, AWS_Data_Architecture]
tags: [aws]     # TAG names should always be lowercase
---


<h1>Introduction</h1>

<p>
In today's fast-paced business world, companies are constantly seeking ways to streamline their operations, increase efficiency, and reduce costs. One way to achieve these goals is by leveraging the power of cloud computing and serverless technologies. This was the case for a company that I was working for and had been using Microsoft SQL Server, SSIS ETL tool and Reporting Services for their business intelligence/internal application needs. <br>
In this blog post, I will summarize how we successfully migrated the complete business intelligence (OLAP) and application (OLTP) databases setup to AWS serverless services, including Amazon Aurora RDS, Lambda, Event Bridge, Glue, S3, Redshift and Quick Sight. In this post I summarise high level details about the architecture and the process.
</p>
