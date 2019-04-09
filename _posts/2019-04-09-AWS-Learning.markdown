---
layout:     post
title:      "AWS: Self Learning"
subtitle:   " \"Essential Training\""
date:       2019-04-09 10:00:00
author:     "Ping"
header-img: "img/in-post/aws_learning/background_awscloud.jpg"
catalog: true
tags:
    - Technology
    - AWS
---

> Most resources in this post are from [Lynda.com AWS Essential Training](https://www.lynda.com/Amazon-Web-Services-tutorials/Amazon-Web-Services-Essential-Training/569195-2.html).

# Cloud Concepts






# Cloud Best Practices






# Design for Failures





# Implement Elasticity: Automate Infrastructure






# Decouple Components





# Optimize For Performance
## Caching: AWS Elasticache
Purpose of usage: Eliminate the database bottlenecks and speed up delivery of application data.    
Thus, it is designed for "HOT" (request frequently) data for better performance. Traditionally, the in-memory cache is not suitable for scalling, 
since the cache on certain server won't be available for newly added servers' access. This is where Elasticache helps, shown:
![elasticache](/img/in-post/aws_learning/elasticache.jpg)

It supports 2 types of caches:

* Memcached 
  - Store strings
  - Up to 1 MB value
  - No persistence
  - Easy to scale
* Redis
  - Support string data
  - Allows higher volume
  - Support persistence
  - Supports other data types, like lists, hashes, etc.
  
The way to choose which one depends on your use case (application). It is wiser to use Redis since it is easier to be expanded.  

* Write-Through Pattern
  - All data stored in memory -> Increased cache hit
  - Require a lot of memory
  
* Lazy Load
  - Only needed data are in cache -> Con of higher miss rate -> potential lower performance
  
**So both ways can be used with the help of TTLs by keeping memory need minimized.**

## caching: AWS CloudFront
## Search: AWS CloudSearch
## Serverless architectures: API gateway
## Serverless architectures: AWS Lambda




# Security




# optimize for Cost








# Set Up a Web Application Architecture with Servers




# Go Serverless




