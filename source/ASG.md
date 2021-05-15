# Auto Scaling

[fdsfds](#what-is-amazon-ec2-auto-scaling)

## What is Amazon EC2 Auto Scaling?

You create collections of EC2 instances, called Auto Scaling groups. 

* Specify the **minimum** number of instances in each Auto Scaling group, and Amazon EC2 Auto Scaling ensures that your group never goes below this size. 
* Specify the **maximum** number of instances in each Auto Scaling group, and Amazon EC2 Auto Scaling ensures that your group never goes above this size. 
* If you specify the **desired capacity**, either when you create the group or at any time thereafter, Amazon EC2 Auto Scaling ensures that your group has this many instances.

![Diagram of auto-scaling group](./images/asg.png)

[What is auto-scaling docs](https://docs.aws.amazon.com/autoscaling/ec2/userguide/what-is-amazon-ec2-auto-scaling.html)

## Auto scaling benefits

* Better fault tolerance. 
  * Amazon EC2 Auto Scaling can detect when an instance is unhealthy, terminate it, and launch an instance to replace it. 
  * You can configure Amazon EC2 Auto Scaling to use multiple Availability Zones. If one Availability Zone becomes unavailable, Amazon EC2 Auto Scaling can launch instances in another one to compensate.
* Better availability by increasing compute to meet needs.
* Cost savings by not buying too much, scale up to what you need.

## Dynamic Scaling Policy Types

Configure how your Auto Scaling group scales using dynamic scaling. There is an Amazon service called CloudWatch that can monitor things like CPU utilization of your EC2 instances. You can use a dynamic scaling policy to make sure that your Auto Scaling group meets a certain cloudwatch metric, like 50% CPU utilization.

There are three types of scaling policies:

* **Target tracking scaling** - Increase or decrease the current capacity of the group based on a target value for a specific metric.
  * Our example where we track 50% CPU Utilization is an example of target tracking scaling.
* **Step/simple scaling** - Increase or decrease by a fixed amount when we hit a certain metric.
  * Add 1 EC2 instance if capacity is under 40%. Remove 1 EC2 instance if capacity is over 60%.
* **Based on SQS** - If you are processing messages from an SQS queue you can scale based on how many messages are in the queue.
  * An SQS queue is a line of messages waiting to be processes by an EC2 instance.

[Scaling Policy Types](https://docs.aws.amazon.com/autoscaling/ec2/userguide/as-scale-based-on-demand.html#as-scaling-types)

## Scaling Cooldowns

A scaling cooldown helps you prevent your Auto Scaling group from launching or terminating additional instances before the effects of previous activities are visible.

When you use simple scaling, after the Auto Scaling group scales using a simple scaling policy, it waits for a cooldown period to complete before any further scaling activities initiated by simple scaling policies can start. An adequate cooldown period helps to prevent the initiation of an additional scaling activity based on stale metrics. By default, all simple scaling policies use the default cooldown period associated with your Auto Scaling group, but you can configure a different cooldown period for certain policies.

## Scheduled Scaling

Scheduled scaling helps you to set up your own scaling schedule according to predictable load changes. For example, let's say that every week the traffic to your web application starts to increase on Wednesday, remains high on Thursday, and starts to decrease on Friday. You can configure a schedule for Amazon EC2 Auto Scaling to increase capacity on Wednesday and decrease capacity on Friday.

To use scheduled scaling, you create **scheduled actions**. Scheduled actions are performed automatically as a function of date and time. When you create a scheduled action, you specify when the scaling activity should occur and the new desired, minimum, and maximum sizes for the scaling action. You can create scheduled actions that scale one time only or that scale on a recurring schedule.

## Lifecycle Hooks

You can run a lifecycle hook to respond to events in the lifecycle of EC2 instances in an auto-scaling group. 

When scaling out you might want to run a script to download and install some software.

When terminating an instance you might want to perform some clean up actions.

![ASG Lifecycle Hooks](./images/asg-lifecycle.png)

## Health Checks

The health status of an Auto Scaling instance is either healthy or unhealthy. All instances in your Auto Scaling group start in the healthy state. Instances are assumed to be healthy unless Amazon EC2 Auto Scaling receives notification that they are unhealthy. This notification can come from one or more of the following sources: Amazon EC2, Elastic Load Balancing (ELB), or a custom health check.

After Amazon EC2 Auto Scaling marks an instance as unhealthy, it is scheduled for replacement.

