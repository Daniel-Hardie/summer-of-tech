# Amazon API Gateway

## Overview

[Amazon API Gateway](https://aws.amazon.com/api-gateway/) allows you to create APIs in AWS. The API Gateway is commonly used as a triggering point for some process, e.g. a payload is received by an API within the API Gateway and its contents are then sent to another AWS service for processing.

## What is an API?

An Application Programming Interface (API) is a software component which allows two different applications to talk to each other. An API is often the entry point for modern applications, where you can have a vast number of APIs as the entry points for different things. APIs also contain a layer of security, so they can help protect your application and ensure no malicious access is given.

For an example, imagine you walk into a fish and chip shop. You previously ordered online and are there to pay and pick up your order. Think of yourself as an application, the kitchen as another application and the person at the counter as the API. When you say I am here to pay and pick up my online order under Daniel, you are authenticating with the person at the counter. They look at the tickets behind the counter and see an order for Daniel, so they know who you are. Now queue the API call, you hand them the cash to pay for your order. The person behind the counter takes the money and puts it in the cash register and then goes into the kitchen (other application) to grab the payload (1 scoop of chips, 2 fish and 1 spring roll). They then come back out the front and give you the payload in return. You have now just successfully called an API to pass through data (paying with money), which triggered a payload to be created in the other application (kitchen) and received that payload in return (your dinner).

If you wish to hit/test/exercise your API, a good tool to use is [Postman](https://www.postman.com/downloads/). It is simple to set up, easy to use and there is a heap of support online for it if you get stuck.

## Getting started

For this getting started exercise, we will create an API Gateway that sends a payload to an AWS Lambda function.

Prerequisites to getting started:

- You are logged in to the AWS Console with an account which has sysadmin privileges. If not and you are unsure how to do this, please follow through [Getting started with AWS](./Getting%20started%20with%20AWS.md) to set yourself up
- You have created a lambda function. If you have not yet done this, please head over to the [AWS Lambda page](./AWS%20Lambda.md)

To get started, in the AWS Console search for API Gateway in the search box and click on the top link to open the API Gateway service page. Upon the page loading click on the "Create API" button.

At this point, you will then be prompted to pick the type of API you want to create. For the purposes of this exercise, we will pick the [REST API](https://restfulapi.net/) type, which is probably the most common type of API used. Press the "Build" button on the non-private REST API type, as shown below:

![API Gateway REST API type](images/API_Gateway_1.png)

You will now need to configure the properties of this REST API. First of all, we want to select REST as the protocol and then we want to create a New API. In the settings sections, write in a descriptive API name and description; leave the Endpoint type as Regional. Press the "Create API" button when finished.

![API Gateway properties](images/API_Gateway_2.png)

Now we need to set up the resources and methods. A resource can be described as the container that holds a collection of methods. A method is a single API endpoint for a given [HTTP Request Method](https://www.w3schools.com/tags/ref_httpmethods.asp). A resource can only have one method of each of these request methods, where request methods include GET, POST, PUT, etc. Each request method has a specific purpose, e.g. the GET is like a read to retrieve information and a POST is to submit new information to create or update something.

Setting up a new resource is quite easy, all you need to do is click on the "Actions" dropdown and select the "Create Resource" option, as shown below

![API Gateway create resource](images/API_Gateway_3.png)

On the New Child Resource page, you will just need to add a Resource Name. The Resource Name should encapsulate just one part/entity of your entire system that you can perform different actions on. For example in Snotbot, calling it sick-leave is a suitable name as you can view how much sick leave is left, request to take sick leave, add sick leave days, etc. Here is an example of what I did using sick-leave:

![API Gateway resource properties](images/API_Gateway_4.png)

Now that we have our resource set up, we need to add a method to it. To do this, click on the "Actions" dropdown menu, and select "Create Method"

![API Gateway create method](images/API_Gateway_5.png)

This will then allow you to select the type ([HTTP Request Method](https://www.w3schools.com/tags/ref_httpmethods.asp)) for your new method. This is dependent on what you wish this method to achieve. For Snotbot a POST was used because we want to send the employee's name and leave reason to AWS from Slack.

![API Gateway select method type](images/API_Gateway_6.png)

Now you will want to set the properties of the new method you have just created. Keep the integration type as Lambda for this exercise and do **NOT** select "Use Lambda Proxy Integration". You will then need to select your lambda function from the dropdown menu. If it is not appearing, you are probably looking in the wrong region. To find what region you created your AWS lambda on, go back to your lambda function and click on the geographic location on the top right of your naviation bar. This will drop down and tell you the code for the region that your lambda is in. For Snotbot, we used Oregon, which has a region code of us-west-2. In the case of this API Gateway method, I selected us-west-2 as the region as shown in the screenshot below. This might be different for you, depending on where your lambda was created. Once this is all done, click "Save".

![API Gateway method properties](images/API_Gateway_7.png)

A popup should now appear asking permission to invoke your lambda function. Press the "Ok" button to allow this. What this will do under the hood is update your IAM permissions for your lambda and add a new policy to your lambda role that allows your lambda function to receive data from this API Gateway.

![API Gateway add lambda permissions](images/API_Gateway_8.png)

Finally, you should be taken back to the Resources screen. This will now show you that you have a REST API endpoint that when invoked sends a payload to your specified lambda function. In response, the lambda function then sends back an OK, which gets returns to the API Gateway, the API Gateway will then return to whatever called the API. Seems simple enough? :P Don't worry if this all does not make sense, the best thing is just to try and get the overview of what is happening. Learning about the more in depth stuff will come with experience and playing around with different services.

![API Gateway overview](images/API_Gateway_9.png)
