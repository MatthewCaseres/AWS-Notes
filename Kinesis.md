# Amazon Kinesis

## What is Kinesis?

Amazon Kinesis makes it easy to collect, process, and analyze real-time, streaming data so you can get timely insights and react quickly to new information.

Traditionally data will be stored in a database and analyzed days or weeks later. With streaming, you analyze the data in real-time as it is collected. This lets you make decisions faster since you see analytics as the data is collected.

There are four parts of Amazon Kinesis

* Kinesis Video Streams
* Kinesis Data Streams
* Kinesis Data Firehose
* Kinesis Data Analytics

We don't worry about Kinesis Video Streams for this exam.

## Kinesis Data Streams

### Shards

For Kinesis Data Streams you provision capacity in units called *shards*. The more shards you provision, the more it costs. One shard provides 1MB/sec data input and 2MB/sec data output along with 1000 PUT records per second. So if we had 10 shards that is 10MB/sec input, 20MB/sec output, and 10,000 PUT records per second.

We can increase the data output of a shard by enabling *enhanced fan-out*, which lets you read 2MB/sec **per consumer** from a shard instead of 2MB/sec across all consumers.

### Records

A **record** is the unit of data stored in an Amazon Kinesis Data stream. Records have the following properties

* **Data blob**: The data of interest added to a data stream.
* **Partition key**: The partition key is defined by the data producer while adding data to the stream and determines which shard the record will go to.
* **Sequence number**: A sequence number is a unique identifier for each record that Amazon Kinesis adds when data is added to the stream 
  * Sequence numbers from the same shard are ordered.
  * Use a partition key to messages from the same message sender a consistent shard, which will make the sequence numbers for this messager ordered.

### Producers and Consumers

Data can be loaded into Kinesis Data streams using the API over HTTPS, the Kinesis Producer Library, and the Kinesis Agent.

You can read from data streams using AWS Lambda, Kinesis Data Analytics, Kinesis Data Firehose, or the Kinesis Client Library. The Kinesis Client Library lets you read from a data stream with a custom application, the library is available for Java, Node.js, .NET, Python, and Ruby.

## Kinesis Data Firehose

Kinesis Data Firehose is fully managed, unlike Kinesis Data Streams. Kinesis Data Firehose will automatically scale to match the throughput of your data and requires no administration.

Firehose can't send to a custom application. We can only send our data to Amazon S3, Amazon Redshift, Amazon Elasticsearch Service, HTTP, and some third party vendors that have integrations like MongoDB.

Kinesis Data Firehose is near-realtime, data is loaded within 60 seconds of being received. You can specify the **buffer size** and the **buffer interval** to determine how much data needs to be collected or how long to wait before delivering the data. For S3 the buffer size is between 1 and 128 MB and the buffer interval is between 60 and 900 seconds.

You can transform data that passes through Kinesis Data Firehose with a lambda function.

## Kinesis Data Analytics

Kinesis Data Analytics lets you apply complicated transformations to a stream of data. These transformations can be applied using SQL or a language that supports Apache Flink. 

* Input data must be 
  * A Kinesis data stream
  * A Kinesis data firehose delivery stream
* Data can be output to 
  * A Kinesis Data Stream
  * Kinesis Data Firehose
  * A lambda hose for post-processing
