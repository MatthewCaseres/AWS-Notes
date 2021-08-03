# Amazon Simple Queue Service (SQS)

## What is SQS?

Amazon Simple Queue Service helps you decouple message producers and message consumers.

Suppose you have an online voting application that will have millions of people voting at once. It would be hard to handle millions of messages per second, but with SQS you can have a queue that stores all the votes and then you process them as they come.

A queue is just a fancy word for a line, you take all the votes and you make them sit in a line until you are ready to process them, just like lines work at the grocery store.

[What are possible use cases for Amazon SQS - StackOverflow
](https://stackoverflow.com/questions/31752503/what-are-the-possible-use-cases-for-amazon-sqs-or-any-queue-service)

## Standard vs. FIFO

There are standard and there are FIFO queues.

- Standard queues
  - Nearly unlimited number of transactions per second.
  - Messages are delivered at least once, but sometimes more than once.
  - Best effort ordering. Occasionally, messages will be delivered out of the order they were sent in.
  - Useful for very high throughput.
- FIFO queues
  - Up to 3000 messages per second, standard is nearly unlimited.
  - First-in-first-out means the first message in the first message out of the queue, compare this to standard queues which are best effort ordering.
  - No duplicates, messages delivered exactly once.

## Configuration

- **Message Visibility Timeout**: The queue holds messages but the consumer must ask for the message, it doesn't "push" messages. Once a consumer asks for a message, the message disappears so that no other consumers ask for the same message while it is being processed.
  - The default visibility is 30 seconds, so once the message is consumed you have 30 seconds to process **and delete** the message before it will be returned to the queue.
  - If you do not delete the message before the timeout is up it will be returned to the queue.
- **Message Retention Period**: If a message is not deleted from the queue it will stay until the message retention period is over.
  - The default message retention period is 4 days, so after 4 days a message will automatically be deleted from the queue.
- **Delivery Delay**: By default the delay is 0 seconds. When you send a message to the queue the consumers can't access it until the delivery delay is over.

## Access Policy

<!-- TODO: Expand this -->

You can manage access with IAM, but just like S3 buckets have their own access policies, SQS queues have their own access policies written in JSON. Here is the default policy saying that only the owner of the queue can send and receive messages from the queue.

```
{
  "Version": "2008-10-17",
  "Id": "__default_policy_ID",
  "Statement": [
    {
      "Sid": "__owner_statement",
      "Effect": "Allow",
      "Principal": {
        "AWS": "889703873633"
      },
      "Action": [
        "SQS:*"
      ],
      "Resource": "arn:aws:sqs:us-east-2:889703873633:"
    }
  ]
}
```

## Server-side encryption

SQS messages are encrypted in-flight by default, but not at rest. You can encrypt them at rest with server-side encryption and amazon will encrypt the messages in the queue with KMS and decrypt them when received by a consumer.

## Dead-letter queue

We usually want to delete a message after using it, when a message has been received too many times we think something is wrong. We can configure how many times a message is received before we send it to the dead-letter queue.

The dead letter queue is just another SQS queue. You can look at the messages in the DLQ to see what is failing to process. It is recommended to set the DLQ retention period to be longer than your other queues, because it's expiration is based on when it entered the first queue, not when it entered the DLQ.
