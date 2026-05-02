# Resources 

- https://www.youtube.com/watch?v=w0SQGCt-6Ro

# Intro

In this course, we'll explore the evolution of networking in modern infrastructures :  
physical servers > virtual machines > containers > container orchestration tools  

# Use Case

Imagine we have built an e-commerce platform that has grown dramatically over the years.  
Let's trace its networking journey, from the early days of the Web to today's modern architecture.  

# Phase 1: The Physical Server Era (1990s)

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

## Limitations of having one physical server

So far, we've been running our e-commerce platform on a single server.  
- **Single point of failure**: what if something happens to this server?
- **Limited scalability**: even a powerful server might not be enough to handle a sudden increase in client requests
- **Inefficient resource utilization**: what if activity decreases and you're paying for more resources than you need?
- **Downtime during maintenance**: your platform remains unavailable until maintenance is over 

# Phase 2: Virtual Machines (VMs)

## The virtualization revolution (2000s)

To answer the limitations of the old infrastructure model, we moved to virtualization.  
Running multiple virtual machines on one physical server.  

A VM is an independent, fully functional computer created by software and running inside a real physical server.  

Each VM gets its own slice of system resources from the host system: vCPUs, vRAM, storage space, and network access.  
Every VM runs its own guest OS, onto which it can install apps, set configurations, and host network connections.  

VMs are strongly isolated from each other and from the host system.  
They can communicate over a virtual network created by the hypervisor.  
This virtual network is like having invisible network cables connecting virtual computers inside our physical server.  

>[!important]
>The hypervisor is a special program that sits between the physical server and the virtual machines.
>It lets the physical server shares its hardware resources with the VMs we create.

## Benefits for our e-commerce web app

Using VMs gives us:
- isolation between services: a crash in one VM does not affect others
- better resource utilization
- portability
- easy backups: their entire state (OS, data, configuration) can be saved as a snapshot file
- easy recovery: snapshots can be quickly restored, or copied to another physical server

And if the physical server that hosts our VMs stops working, we can easily restore them on another server, as long as we had external backups.  

## Main Networking Components of VMs

When you run multiple VMs inside one physical server, each VM has a virtual network interface, which in turn has: 
- a unique private IP address: which allows VMs to talk to each other
- a firewall: which checks incoming and outgoing traffic based on rules we specify

Main **firewall checks** include:
- verifying the sender's identity
- what port they're trying to reach
- whether they're allowed to talk to that VM

All internal traffic is routed and managed by the **hypervisor**, which also keeps outsiders out unless invited.  

If a VM needs to communicate with the outside world, its traffic goes from the internal virtual network out to the Internet through the physical server's public IP.  

This process uses **Network Address Translation** (NAT) to convert the private internal IP addresses to the public one.  

And every bit of traffic is filtered by **software firewalls**, which check the data, enforce security policies, and only allow safe permitted requests and responses to go through, which keeps the entire communication secure.  

# Phase 3: Cloud Networking

Our e-commerce platform kept growing, and maintainning and configuring our physical servers and VMs became a hassle.  
Which is why we decided to rent our VMs instead of owning them.  

We chose a cloud provider, and all our VMs now run within a VPC = a Virtual Private Cloud.  
Our VPC is divided into private and public subnets:
- VMs in public subnets are accessible to any device connected to the Internet
- VMs in private subnets are used for databases and applications that only our internal staff has access to

---
21/38
