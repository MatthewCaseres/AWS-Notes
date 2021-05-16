# Networking Basics

## IPv4

IP addresses specify the location of devices on the internet. IPv4 is a type of IP address. There are 32 bits in an IPv4 address, for a total of 2^32 (about 4 billion) IPv4 addresses. IPv4 is the most common way to do addressing, but only having 4 billion addresses has led to the creation of IPv6 (IPv6 isn't a major exam topic).

IP addresses are represented in "dot decimal" notation. There are four numbers 0-255 separated by decimals. So `120.247.236.38` is an IP address. IP addresses can be broken up into two parts, the **network prefix** which specifies the location of the network, and the **host identifier** which specifies a device on the network.

![IPv4 address in dotted-decimal notation](/source/images/ipv4-dotdecimal.png)

So maybe the network is specified by `120.247.236` and the host address is specified by `.38`. But how do we know where to split the address?

[IPv4 on Wikipedia](https://en.wikipedia.org/wiki/IPv4)

## CIDR

CIDR is a way of specifying ranges of IP addresses. In `120.247.236.0/24` the `/24` means that the first 24 bits (`120.247.236`) are the network identifier and that the network contains device ranging from `120.247.236.0` to `120.247.236.255`.

If we had something like `120.247.236.38/32` then every bit in the IP address is in the network prefix, and the network contains only a single device at `120.247.236.38/32`.

Here is a chart from the official specification:

![](/source/images/CIDR.png)

When we day 0.0.0.0/0 we are specifying all IPv4 addresses. This is can be used in AWS to say that any IP address can access a resource.

The term for the number that specifies the IP range in CIDR (i.e. `/24`, `/30`, etc.) is the **netmask**.

## Private Addresses

Some address ranges are private, meaning they are used for something like a private company wide 'intranet' but aren't sent over the public internet. 

These IP addressses are reserved and are in the ranges 
* `10.0.0.0 – 10.255.255.255`, CIDR `10.0.0.0/8` 
* `172.16.0.0 – 172.31.255.255`, CIDR `172.16.0.0/12`
* `192.168.0.0 – 192.168.255.255`, CIDR `	192.168.0.0/16`

Can you make sense of the relationship between the CIDR block and the IP range?

[CIDR on Wikipedia](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing)