## This AWS multi-tier Ecommerce Website was developed using React, HTML, typescript, and Javascript

## Overview

The goal of the AWS Bookstore Demo App is to provide a fully-functional web application that utilizes multiple purpose-built AWS databases and native AWS components like Amazon API Gateway and AWS CodePipeline. Increasingly, modern web apps are built using a multitude of different databases. Developers break their large applications into individual components and select the best database for each job. Let's consider the AWS Bookstore Demo App as an example. The app contains multiple experiences such a shopping cart, product search and a top sellers list. For each of these use cases, the app makes use of a purpose-built database.
This website uses a CloudFormation template:

## Database components

* Product catalog/shopping cart - Amazon DynamoDB offers fast, predictable performance for the key-value lookups needed in the product catalog, as well as the shopping cart and order history.  In this implementation, we have unique identifiers, titles, descriptions, quantities, locations, and price.
* Search - Amazon Elasticsearch Service enables full-text search for our storefront, enabling users to find products based on a variety of terms including author, title, and category.
* Top sellers list - Amazon ElastiCache for Redis reads order information from Amazon DynamoDB Streams, creating a leaderboard of the “Top 20” purchased or rated books.

## Application components

* Serverless service backend – Amazon API Gateway powers the interface layer between the frontend and backend, and invokes serverless compute with AWS Lambda.  
* Web application blueprint – React web application with Bootstrap and React Router

## Infrastructure components

* Continuous deployment code pipeline – AWS CodePipeline and AWS CodeBuild help you build, test, and release your application code. 
* Serverless web application – Amazon CloudFront and Amazon S3 provide a globally-distributed application. 


