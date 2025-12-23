# Testing VPC Connectivity

**Project Link:** https://learn.nextwork.org/projects/aws-networks-connectivity  
**Author:** Shane Brown  

---

## Overview

This project focuses on testing and validating connectivity within an Amazon Virtual Private Cloud (VPC). The goal is to understand how routing, security groups, and network ACLs work together to either allow or block communication between cloud resources and the internet.

By actively testing connectivity and troubleshooting failures, this project reinforces how layered security controls impact real-world cloud networking behavior. :contentReference[oaicite:0]{index=0}

---

## What I built

I tested connectivity across a custom VPC environment that included both public and private EC2 instances. This involved:

- Connecting to a public EC2 instance using EC2 Instance Connect  
- Testing communication between public and private EC2 instances  
- Verifying security group and network ACL behavior  
- Testing outbound internet access from a public server  
- Troubleshooting blocked traffic and validating fixes  

This setup reflects common cloud troubleshooting scenarios faced by cloud and security engineers. :contentReference[oaicite:1]{index=1}

---

## Key concepts learned

- What connectivity means in a cloud networking context  
- How EC2 Instance Connect uses SSH for secure access  
- How security groups and network ACLs affect traffic flow  
- How ICMP traffic is used to test internal connectivity  
- How HTTP requests confirm internet access  
- Why multiple layers must be checked when troubleshooting network issues :contentReference[oaicite:2]{index=2}

---

## Testing internal connectivity

I used the `ping` command to test connectivity between my public and private EC2 instances. This confirmed whether ICMP traffic was allowed between subnets.

When the ping failed, it showed that traffic was being blocked. By updating the private subnet’s network ACL and the private server’s security group to allow ICMP traffic from trusted sources, connectivity was successfully restored. :contentReference[oaicite:3]{index=3}

---

## Testing internet connectivity

I used the `curl` command to test whether my public EC2 instance could access external websites. Receiving a valid HTTP response confirmed that:

- The public subnet had a route to the Internet Gateway  
- Security groups allowed outbound traffic  
- The VPC networking configuration was working correctly  

This demonstrated how public servers communicate with the internet while private servers remain isolated. :contentReference[oaicite:4]{index=4}

---

## Ping vs Curl

- **Ping**
  - Uses ICMP to test basic network reachability  
  - Confirms whether two systems can communicate  

- **Curl**
  - Uses HTTP/HTTPS to request real data  
  - Confirms both connectivity and application-layer access  

Using both tools provides a complete picture of network health and accessibility. :contentReference[oaicite:5]{index=5}

---

## Why this project matters

Connectivity testing and troubleshooting are essential skills for cloud engineers and security professionals. Understanding how and why traffic is blocked helps prevent misconfigurations, improves security posture, and ensures applications function reliably.

This project demonstrates how cloud networking issues are identified and resolved by examining each layer of the VPC architecture. :contentReference[oaicite:6]{index=6}

---

## Documentation

📄 **Full project documentation:**  
[documentation.md](./documentation.md)

This file includes detailed testing steps, troubleshooting actions, command examples, and reflections from completing the project.

---

## Credits

Built as part of the **NextWork** AWS networking learning series.
