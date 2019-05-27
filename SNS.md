# AWS SNS

## Overview

Amazon Simple Notification Service (Amazon SNS) is a web service that coordinates and manages the delivery or sending of messages to subscribing endpoints or clients. In Amazon SNS, there are two types of clients—publishers and subscribers—also referred to as producers and consumers. Publishers communicate asynchronously with subscribers by producing and sending a message to a topic, which is a logical access point and communication channel. Subscribers (i.e., web servers, email addresses, Amazon SQS queues, AWS Lambda functions) consume or receive the message or notification over one of the supported protocols (i.e., Amazon SQS, HTTP/S, email, SMS, Lambda) when they are subscribed to the topic.

## Key Concepts

* **topic** - a communication channel with defined set of permissions
* **publisher** - a producer of messages sending them to a topic
* **subscriber** - a consumer of the message being notified about it

Communication is push based, that is: a producer sends the message to the topic, which is then pushed to all subscribers without
the need of polling.

Possbile types of subscribers:
* Lambda function
* SQS queue
* HTTP(S) endpoint
* SMS
* Mobile push
* E-mail

## General usage

* Fanout of messages - one published messages delivered to multiple subscribers of various types
* Delivery of application and system alerts - alters are published to SNS Topic and consumed by subscribers
* Sending push email and sms messages
* Mobile push notifications 

## Monitoting and logging

* Message delivery status can be logged into CloudWatch. It will contain information like status, response from SNS enpoint
  and dwell time (time between publishing and handing of to SNS)

## Security

## Limits

## Pricing model

## Others

## Resources