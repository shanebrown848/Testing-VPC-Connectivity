<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Testing VPC Connectivity

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-connectivity)

**Author:** Shane Brown  
**Email:** shanebrown848@gmail.com

---

## Testing VPC Connectivity

![Image](http://learn.nextwork.org/encouraged_yellow_silly_yeti/uploads/aws-networks-connectivity_8ee57662)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is a service that lets you create your own private, isolated network within the AWS Cloud. It allows you to define IP address ranges, create public and private subnets, control routing, and apply security rules using security groups and network ACLs. Amazon VPC is useful because it gives you full control over how your AWS resources communicate, improves security by isolating resources, and provides a reliable and scalable foundation for building cloud applications.

### How I used Amazon VPC in this project

In today’s project, I used Amazon VPC to build and manage a custom network for my AWS resources. I configured public and private subnets, route tables, security groups, and network ACLs, then launched EC2 instances into each subnet. I also used the VPC to test connectivity between instances and the internet, troubleshooting access issues to confirm that the network was securely and correctly configured.

### One thing I didn't expect in this project was...

One thing I didn’t expect in this project was how many different networking components have to work together for connectivity to succeed. Even when the route tables were configured correctly, traffic was still blocked until both the network ACLs and security groups were updated, which showed me how important it is to check every layer when troubleshooting VPC connectivity.

### This project took me...

This project took me about 45 mins, due to the fact that I still had my resources from the other projects before this one.

---

## Connecting to an EC2 Instance

Connectivity means the ability for systems, devices, or resources to communicate with each other over a network. In AWS, it refers to how EC2 instances, subnets, and external networks send and receive data through routing, security groups, and network ACLs. Good connectivity ensures that data flows reliably and securely between resources so applications function as expected.

My first connectivity test was whether I could connect to the NextWork Public Server from the AWS Management Console using EC2 Instance Connect.

![Image](http://learn.nextwork.org/encouraged_yellow_silly_yeti/uploads/aws-networks-connectivity_88727bef)

---

## EC2 Instance Connect

I connected to my EC2 instance using EC2 Instance Connect, which is an AWS feature that allows me to securely access an EC2 instance through SSH directly from the AWS Management Console. It works by temporarily generating and using a one-time SSH key, so I don’t need to manage my own private key files. This makes it easier to connect to instances while still keeping the connection secure.

My first attempt at getting direct access to my public server resulted in an error because the security group attached to the instance did not allow inbound SSH traffic. The inbound rules only permitted HTTP traffic, so the SSH connection used by EC2 Instance Connect was blocked. Once I added an inbound SSH rule to the security group, the connection was successful.

I fixed this error by updating the security group attached to my public EC2 instance to allow inbound SSH traffic. I added a new inbound rule with the SSH type and set the source to Anywhere-IPv4 so EC2 Instance Connect could reach the instance. After saving the rule, I retried the connection and was able to successfully access the server.

![Image](http://learn.nextwork.org/encouraged_yellow_silly_yeti/uploads/aws-networks-connectivity_1cbb1b88)

---

## Connectivity Between Servers

Ping is a network testing tool that sends ICMP messages from one device to another to check whether they can communicate. I used ping to test the connectivity between my public EC2 instance and my private EC2 instance, and to confirm whether network settings like security groups and network ACLs were allowing traffic between them.

The ping command I ran was:
ping 10.0.1.104
This command sent ICMP echo requests from my public EC2 instance to the private IP address of my private EC2 instance to test connectivity between them.

The first ping returned only a single line showing that a ping request was sent, but there were no reply messages from the private server. This meant that the public server could send traffic, but the private server was not responding, which indicated that ICMP traffic was being blocked by the private subnet’s network ACLs or security group.

![Image](http://learn.nextwork.org/encouraged_yellow_silly_yeti/uploads/aws-networks-connectivity_defghijk)

---

## Troubleshooting Connectivity

I troubleshooted this by checking the private subnet’s route table, network ACL, and the private server’s security group to see what was blocking the ping. I found that the private network ACL was denying inbound and outbound traffic, so I added rules to allow All ICMP - IPv4 between the public subnet (10.0.0.0/24) and the private subnet. I also updated the NextWork Private Security Group to allow inbound ICMP from the NextWork Public Security Group. After saving those changes, the ping started returning replies, confirming connectivity.

![Image](http://learn.nextwork.org/encouraged_yellow_silly_yeti/uploads/aws-networks-connectivity_4a9e8014)

---

## Connectivity to the Internet

Curl is a command-line tool used to send requests to servers and transfer data over a network. It is commonly used to test internet connectivity, retrieve web content, and interact with APIs by making HTTP and HTTPS requests. In this project, curl confirmed that the public EC2 instance could successfully communicate with websites on the internet and receive data in response.

I used curl to test the connectivity between my public EC2 instance and the internet. By sending HTTP requests to external websites and receiving responses, curl confirmed that my public server could successfully access online resources through the internet gateway and that my VPC networking and security settings were working correctly.

### Ping vs Curl

Ping and curl are different because they test connectivity in different ways and at different layers of the network. Ping uses ICMP messages to check whether one machine can reach another and how long the communication takes, but it does not transfer application data. Curl uses application-layer protocols like HTTP or HTTPS to request and receive data from a server, which allows it to test both connectivity and data transfer.

---

## Connectivity to the Internet

I ran the curl command curl example.com, which returned the HTML content of the example.com website, confirming that my public EC2 instance was able to successfully connect to the internet and retrieve data from an external server.

![Image](http://learn.nextwork.org/encouraged_yellow_silly_yeti/uploads/aws-networks-connectivity_8ee57662)

---

---
