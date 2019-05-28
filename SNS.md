[< Back](README.md)

# AWS SNS

## Overview

Amazon Simple Notification Service (Amazon SNS) is a web service that coordinates and manages the delivery or sending 
of messages to subscribing endpoints or clients. In Amazon SNS, there are two types of clients—publishers and 
subscribers—also referred to as producers and consumers. Publishers communicate asynchronously with subscribers by 
producing and sending a message to a topic, which is a logical access point and communication channel. Subscribers 
(i.e., web servers, email addresses, Amazon SQS queues, AWS Lambda functions) consume or receive the message or 
notification over one of the supported protocols (i.e., Amazon SQS, HTTP/S, email, SMS, Lambda) when they are subscribed
to the topic.

## Key Concepts

* **topic** - a communication channel with defined set of permissions
* **publisher** - a producer of messages sending them to a topic
* **subscriber** - a consumer of the message being notified about it

Communication is push based, that is: a producer sends the message to the topic, which is then pushed to all subscribers 
without the need of polling.

Possible types of subscribers:
* Lambda function
* SQS queue
* HTTP(S) endpoint
* SMS
* Mobile push
* E-mail

SNS supports **message attributes** which are optional and delivered along with the message body. They are way to provide 
additional metadata. In order to include message attributes `Raw Message Delivery` must be set to `True`. Each message 
attribute has a name, type and value.   

By default, subscribers receive every message published to the topic. A subscriber can assign a **filter policy** to the 
topic subscription. Filtering is based on message attributes. Filtering policy can specify which attributes should be 
checked for a matched:
* String attributes can be checked for exact match (whitelist), anything-but (blacklist) or prefix
* Numeric values can be checked for exact match or a range match
* logical AND/OR operations can be used

SNS supports relatively large payloads, from 64 to 256 kilobytes. Large payloads require using SDK supporting Singature 
Version 4.  

SNS Topics support tagging. Tag-based access control isn't available yet.

## General usage

* Fanout of messages - one published messages delivered to multiple subscribers of various types
* Delivery of application and system alerts - alters are published to SNS Topic and consumed by subscribers
* Delivery of services notification (ie. new file in S3)
* Sending push email and sms messages
* Mobile push notifications 


## Monitoring and logging

* Message delivery status can be logged into CloudWatch. It will contain information like status, response from SNS 
  enpoint and dwell time (time between publishing and handing of to SNS)
* List of allowed metrics can be found at https://docs.aws.amazon.com/sns/latest/dg/sns-monitoring-using-cloudwatch.html
* SNS is integrated with CloudTrail. All SNS API calls will be logged as events. Full list of actions that can be logged
  can be found at https://docs.aws.amazon.com/sns/latest/dg/sns-logging-using-cloudtrail.html

## Security

Access to SNS can be controlled through access control policies (IAM). Valid SNS policy actions are listed at
https://docs.aws.amazon.com/sns/latest/api/API_Operations.html
They allow to control publishing, subscription, permission management, topic management, etc.

The following keys can be used to control subscribe requests:
* sns:Endpoint
* sns:Protocol

It is possible to enable SSE with SNS. SNS uses keys managed in AWS KMS. Once the message is received it is encrypted 
and stored in an encrypted version. Before delivering the message to the subscribers the message get decrypted. SSE 
encrypts the body of the message. SSE doesn't encrypt the following:
* topic metadata (name and attributes)
* message metadata (subject, message ID, timestamp and attributes) 
* per-topic metrics

Backlogged messages don't get encrypted when encryption is enabled on topic.
Existing encrypted messages don't get decrypted when you disable encryption on topic.

It is possible to setup an Interface VPC Endpoint between SNS and your VPC. This way message will not have to go 
through internet. 

## Limits

For up to date information check: https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html

Default resource limits:
* 100,000 topics per account
* 12,500,000 subscriptions per topic
* 5,000 pending subscriptions
* 10 deliveries of email messages per second, 20 for SMS

API hard limits:
* list operations at 30 req/s, beside ListPlatformApplications which is 15 req/s
* subscribe/unsunscribe 100 req/s

API soft limits:
* publishing depends on the regions and varies from 300, through 1,500, 9,000 up to 30,000 in US East

## Pricing model

No minimum fee, pay only for what you use:
* $0.50 per 1m SNS requests
* $0.06 per 100,000 notification deliveries over HTTP
* $2.00 per 100,000 notification deliveries over email.
* 100 free SMS deliveries, price differs by country
* Free Tier is included.


## Resources

* [Documentation](https://docs.aws.amazon.com/sns/index.html)
* [FAQ](https://aws.amazon.com/sns/faqs/)
* [Interface VPC Endpoints](https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html)
