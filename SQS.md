[< Back](README.md)

# AWS SQS

## Overview

Amazon Simple Queue Service (Amazon SQS) offers a secure, durable, and available hosted queue that lets you integrate 
and decouple distributed software systems and components. Amazon SQS offers common constructs such as dead-letter queues 
and cost allocation tags. It provides a generic web services API and it can be accessed by any programming language 
that the AWS SDK supports. Amazon SQS supports both standard and FIFO queues.

## Key Concepts

* **standard queue**, provides nearly unlimited throughput, at least once delivery and best effort ordering
* **FIFO queue**, high throughput, exactly once processing, first in first our delivery

## General usages

Todo

## Monitoring and logging

Todo

## Security

Todo

## Limits

Queue limits:
* delay queue: 0 (default) to 15 minutes
* inflight messages: 120,000 per standard queue, 20,000 per fifo queue
* listed queues: 1,000 per request
* queue name: 80 characters
* queue tags: up to 50

Message limits:
* batched message idL up to 80 characters
* message attributes: up to 10
* message batch: up to 10
* message content: XML, JSON and unformatted text
* message retention: default 4 days, minimum 60 seconds, maximum 14 days
* message throughput: standard queue nearly unlimited, FIFO 3,000 messages per second with braching, 300 messages per 
  second per action
* message timer: default 0, maximum 15 minutes
* message size: 1 byte to 256 KB. [Amazon SQS Extended Client Library for Java](https://github.com/awslabs/amazon-sqs-java-extended-client-lib)
  allows sending messages with a reference to S3 with maximum payload of 2GB
* message visibility timeout: default 30 seconds, minimum 0, maximum 12 hours.

Policy limits:
* bytes: 8,192
* Conditions: 10
* Principals: 50
* Statements: 20

## Pricing model

Todo

## Resources

* [Documentation](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/welcome.html)
* [FAQ](https://aws.amazon.com/sqs/faqs/)