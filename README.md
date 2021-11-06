## This AWS multi-tier Ecommerce Website was developed using React, HTML, typescript, and Javascript

## Overview

This AWS Ecommerce Website uses multiple purpose-built AWS databases for its features and native AWS components like Amazon API Gateway and AWS CodePipeline. This website has user accounts, a shopping cart, front end search, a checkout payment front end, and a top sellers list. 

## Frontend

Web asset resources are in a S3 bucket. Amazon CloudFront caches the frontend content from S3 and displays a CloudFront interface to users. The frontend interacts with Amazon Cognito and Amazon API Gateway only. Amazon Cognito is used for all logins and user accounts and API Gateway,Lambda is used for all API calls for communication between  DynamoDB, Elasticsearch, ElastiCache.

## Backend

The backend includes Amazon Cognito, Amazon DynamoDB, AWS Lambda, and Amazon API Gateway. The application leverages Amazon Cognito for user authentication, and Amazon DynamoDB to store all of the data for books, orders, and the checkout cart. As books and orders are added, Amazon DynamoDB Streams push updates to AWS Lambda functions that update the Amazon Elasticsearch cluster and Amazon ElasticCache for Redis cluster. Amazon Elasticsearch powers search functionality for books. Amazon ElasticCache for Redis powers the books leaderboard.
Example: AddToCart Lambda function that adds a specified book to the user's cart. Price is included in this function's request so that the price is passed into the cart table in DynamoDB.
AddToCartRequest {
    bookId: string
    quantity: number
    price: number
}

BooksTable {
  id: string (primary key)
  author: string
  category: string (index, GSI)
  cover: string (url to s3 file)
  name: string 
  price: number
  rating: number
}

OrdersTable {
    customerId: string (primary partition key)
    orderId: string (uuid, primary sort key)
    books: bookDetail[]
    orderDate: date 
}

CartTable {
    customerId: string (primary partition key)
    bookId: string (uuid, primary sort key)
    price: number
    quantity: number
}

## Amazon CloudFront hosts the web application frontend and gets web pages and images from S3 cloud storage using data from buckets.
## Database components
## Amazon Cognito is used for login and user accounts
* Amazon Cognito passes the CognitoIdentityID or customerID for every user and all Amazon API Gateway requests to Lambda functions

* Product catalog/shopping cart - Amazon DynamoDB stores information in tables about the product catalog, shopping cart and item orders using identifiers, titles, descriptions, quantities, locations, and price.
* Top sellers list - Amazon ElastiCache for Redis reads order information from Amazon DynamoDB Streams, creating a leaderboard of the “Top 20” purchased or rated books.

## Application components

* Serverless service backend – Amazon API Gateway powers the interface layer between the frontend and backend, and invokes serverless compute with AWS Lambda.  
* Web application blueprint – React web application with Bootstrap and React Router

## Production components

* Continuous deployment code pipeline – AWS CodePipeline and AWS CodeBuild help you build, test, and release your application code. 
* Serverless web application – Amazon CloudFront and Amazon S3 provide a globally-distributed application. 


