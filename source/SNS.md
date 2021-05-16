# Amazon Simple Notification Service \(SNS\)

## What is SNS?

Amazon SNS delivers messages from publishers to subscribers, this pattern is often called pub-sub. 
You can publish a message to an SNS topic and all of the subscribers to this topic will receive the message. 

Subscribers to the topic can be SQS queues, HTTP, email, mobile push notifications, and mobile text messages (SMS). The publishers are AWS services, an example use case is using SNS to send yourself a text message when you set off an Amazon CloudWatch alarm.

## Fanout pattern

A common use case is sending messages to many different subscribers. Having an SNS topic means our publisher only has to send data to one place, the SNS topic is used to "fanout" the message.

![SNS use case](./images/sns-use.png)

You can use the fanout pattern to replicate data sent to your production environment with your test environment, this way you can test your application with data received from your production application.

[Common SNS Scenarios - docs](https://docs.aws.amazon.com/sns/latest/dg/sns-common-scenarios.html)

## FIFO

Just like there are SQS standard and SQS FIFO, there are SNS standard and SNS FIFO. The differences are quite similar.

* Standard is best-effort message ordering, FIFO is always in the same order the message was sent.
* Standard is at-least once message delivery, FIFO is exactly-once message delivery.
* Standard has higher throughput than FIFO.
* Only FIFO SQS queues can subscribe to FIFO SNS topics. Lambda, HTTP, SMS, email, and mobile apps can all subscribe to standard SNS topics but not FIFO SNS topics.

Use FIFO SNS topics with FIFO SQS queues when you need to decouple an application and the order of messages is important.

## Message Filtering

By default, an Amazon SNS topic subscriber receives every message published to the topic. To receive a subset of the messages, a subscriber must assign a filter policy to the topic subscription.

Messages sent from an SNS topic can include a `MessageAttributes` field that can be filtered on by subscribers.

```json
{
   "Type": "Notification",
   "MessageId": "a1b2c34d-567e-8f90-g1h2-i345j67klmn8",
    ...,
   "MessageAttributes": {
      "customer_sport": {
         "Type": "String",
         "Value": "soccer"
      },
      "store": {
         "Type": "String",
         "Value":"example_corp"
      },
      "event": {
         "Type": "String",
         "Value": "order_placed"
      },
      "price_usd": {
         "Type": "Number", 
         "Value":210.75
      }
   }
}
```

In the subscription filter we can define a JSON policy that determines which messages we accept. Here is a policy that accepts.

```json
{
   "store": ["example_corp"],
   "event": [{"anything-but": "order_cancelled"}],
   "customer_interests": "soccer",
   "price_usd": [{"numeric": [">=", 100]}]
}
```

This should be detailed enough for the exam, but you can learn more in [the documentation](https://docs.aws.amazon.com/sns/latest/dg/sns-message-filtering.html).