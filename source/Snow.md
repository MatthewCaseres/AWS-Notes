# Snow

## What is the AWS Snow Family?

### Storage

The AWS Snow Family is a collection of physical devices that help migrate large amounts of data into and out of the cloud without depending on networks.

How this works is AWS sends you a computer and you send it back to them. This might sound slow, but it can be faster than sending it over the internet if you have enough data. It would take 13 days to send 100TB at 100MB/s!

That is why it makes sense to physically ship your data to Amazon and they will put it in S3 for you.

### Compute

Since they are sending you a computer, you can use it as a computer. Maybe you want to process your data while it is in transit.

## Members of the Snow Family

### AWS Snowcone

Snowcone is small rugged, edge compute and data storage product. You can use Snowcone to collect, process, and transfer data to AWS, either offline by shipping the device, or online with AWS DataSync. Running applications in austere (non-data center) edge environments or where there is lack of consistent network connectivity or low bandwidth can be challenging because these locations often lack the space, power, and cooling needed for data center IT equipment. With 2 vCPUs, 4 GB of memory, and 8 TB of usable storage, Snowcone can run edge computing workloads that use Amazon EC2 instances, and store data securely. 

### AWS Snowball

AWS Snowball, a part of the AWS Snow Family, is an edge computing, data migration, and edge storage device that comes in two options. Snowball Edge Storage Optimized devices provide both block storage and Amazon S3-compatible object storage, and 40 vCPUs. They are well suited for local storage and large scale-data transfer. Snowball Edge Compute Optimized devices provide 52 vCPUs, block and object storage, and an optional GPU for use cases like advanced machine learning and full motion video analysis in disconnected environments. You can use these devices for data collection, machine learning and processing, and storage in environments with intermittent connectivity (like manufacturing, industrial, and transportation) or in extremely remote locations (like military or maritime operations) before shipping them back to AWS. These devices may also be rack mounted and clustered together to build larger temporary installations.

Snowball supports specific Amazon EC2 instance types and AWS Lambda functions, so you can develop and test in the AWS Cloud, then deploy applications on devices in remote locations to collect, pre-process, and ship the data to AWS. Common use cases include data migration, data transport, image collation, IoT sensor stream capture, and machine learning.

### AWS Snowmobile

AWS Snowmobile is an Exabyte-scale data transfer service used to move extremely large amounts of data to AWS. You can transfer up to 100PB per Snowmobile, a 45-foot long ruggedized shipping container, pulled by a semi-trailer truck.

When your Snowmobile is on site, AWS personnel will work with your team to connect a removable, high-speed network switch from Snowmobile to your local network and you can begin your high-speed data transfer from any number of sources within your data center to the Snowmobile. After your data is loaded, Snowmobile is driven back to AWS where your data is imported into Amazon S3.

Snowmobile uses multiple layers of security to help protect your data including dedicated security personnel, GPS tracking, alarm monitoring, 24/7 video surveillance, and an optional escort security vehicle while in transit. All data is encrypted with 256-bit encryption keys you manage through the AWS Key Management Service (KMS) and designed for security and full chain-of-custody of your data.