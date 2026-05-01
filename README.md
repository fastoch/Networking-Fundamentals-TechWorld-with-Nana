# Resources 

- https://www.youtube.com/watch?v=w0SQGCt-6Ro

# Intro

In this course, we'll explore the evolution of networking in modern infrastructures :  
physical servers > virtual machines > containers > container orchestration tools  

# Use Case

Imagine we have built an e-commerce platform that has grown dramatically over the years.  
Let's trace its networking journey, from the early days (1990) of the Web to today's modern architecture.  

# Phase 1: The Physical Server Era

When our e-commerce platform first launched, everything ran on a single physical server.  
One powerful machine in a data center running our web application, database, and all the services, using a single public IP address.  

This IP address tells other computers where to send data (or requests) in order to communicate with our server.  
IP stands for Internet Protocol. Currently, we use two version of this protocol: IPv4 and IPv6.  

## How do networks communicate?

A network is the interconnection of multiple devices located in the same area, just like neurons in your brain.  

The Internet is the interconnection of all networks across the world.  
To connect two networks together, we use special devices named **routers**.  

## How do humans communicate with remote servers over the Web?

Web sites and Web applications are hosted on Web servers.  

Thanks to **DNS**, "Domain Name System", we can use human-readable addresses (URLs) to communicate with any web server.  
Those addresses are automatically translated into IP addresses which computing devices can "understand" and work with.  

There are DNS servers scattered all across the world to enable this perpetual automatic translation between URLs and IP addresses.   

## How does communication between end users and web applications work?

When we browse the web and interact with web applications via our web browser, we send HTTP requests to web servers.  
In return, they serve us the web pages and all the data we're asking for.  

**HTTP** is the protocol used for communication between web servers.  
It stands for Hyper-Text Transfer Protocol.  

Once the (client) requests we make reach the targeted web servers, how do they get to the actual web application that is running on those servers?  
- Data leaves our computer through a **network interface** and travels over the Internet until it reaches a server's network interface
- Most common interfaces are: **eth0** (first Ethernet interface), eth1, **wlan0** (first Wi-Fi interface), wlan1, and **lo** (loopback)
- each network interface has an **IP address** associated with it
- each IP address has many **ports** that can be open or closed to communication
- each open port can be used by an application to "listen" to incoming traffic
- for HTTP and HTTPS traffic, respective port numbers are 80 and 443
- There's a list of common ports (known ports) for each type of application/service
- The Operating System is in charge of routing incoming traffic to the proper application/service

## Limitation 1: Single Point of Failure

So far, we've been running our e-commerce web application on a single server.  
What if something happens to this server?  

# Phase 2: Virtual Machines (VMs)



---
9/38
