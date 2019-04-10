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
A CDN service keep the data in cache to speed up delivery of web and mobile application content. It also helps
the scaling since it reduces the direct request to server.

Consists of: 
* A distribution 
* Edge locations
* Regional edge caches  
![cloud_front](/img/in-post/aws_learning/cloud_front.jpg)


## Search: AWS CloudSearch  
A dedicated search engine to help improve user experience and maximize engagement.

Search Engines need to have features:
* fast
* reliable
* best results based on relevancy to the query

![cloud_search](/img/in-post/aws_learning/cloud_search.jpg)



## Serverless architectures: API gateway
Let the app uses the API gateway when API is required for an application.  
![api_gateway](/img/in-post/aws_learning/api_gateway.jpg)

Additional features: 
* Multiple versions and release stages
* Automatic SDK generation 
* monitoring and logging


## Serverless architectures: AWS Lambda

Two components:
* The lambda function itself (custom code uploaded to the server)
* Event source 
  - Other services of AWS
  - Custom applications
  


# Security
Shared security by both users and AWS together.

* Iaas(Infrastructure as a Service): The user takes more responsibilities
* Paas(Platform as a Service): AWS takes more responsibilities
* Saas(Software as a service): The user takes the least responsibilities


# optimize for Cost








# Set Up a Web Application Architecture with Servers




# Go Serverless




