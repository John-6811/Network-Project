# TechNova Ltd – Network Configuration and Access Control

This project documents the design and configuration of a departmental network for TechNova Ltd using Cisco Packet Tracer. It demonstrates IP address configuration, connectivity testing between departments, access control list (ACL) implementation, and controlled access to a server's HTTP service.

## Table of Contents

- Project Overview
- Network Topology
- Tools and Technologies
- Configuration Steps
- Results and Findings
- Author

## Project Overview

The purpose of this project was to configure and test a network environment for TechNova Ltd, connecting the IT, Sales, and Human Resources (HR) departments while applying access control to manage communication between devices.

The project focused on:

- Configuring IP addresses for departmental devices.
- Establishing and testing network connectivity.
- Using an Access Control List (ACL) to restrict selected traffic between departments.
- Verifying that Sales users could access the server's HTTP service.
- Testing network behaviour through successful and unsuccessful ping results.

This project demonstrates practical networking skills relevant to network administration, access management, and foundational cybersecurity.

## Network Topology

The network topology represents TechNova Ltd's departmental network, including IT, Sales, and HR devices and a server providing an HTTP service.

The documented tests show that HR could successfully ping an IT computer, while a ping from Sales to IT was unsuccessful. The project also includes an ACL configuration and a test demonstrating Sales access to the server's HTTP service.

The topology includes a central router connected to departmental switches, with end-user PCs and a server connected to the relevant switches. The documented IPv4 addressing uses separate subnets for each department.

- IT Department: `192.168.10.0/24`
- Sales Department: `192.168.20.0/24`
- HR Department: `192.168.30.0/24`

The router provides connectivity between the departmental networks, while an extended ACL controls selected traffic originating from Sales.

## Tools and Technologies

- Cisco Packet Tracer - network design, configuration, and simulation.
- Cisco router - inter-network routing and ACL implementation.
- Network switches - connecting departmental devices.
- End-user PCs - testing connectivity and access restrictions.
- Server - hosting the HTTP service.
- IPv4 addressing and subnetting - separating departmental networks.
- Cisco IOS CLI - configuring router access control.
- Ping (`ping`) - testing network connectivity.
- HTTP - verifying access to the server's web service.

## Configuration Steps

1. Designed the network topology
   - Created a central router connected to the IT, Sales, and HR departmental switches.
   - Connected departmental PCs and the server to the relevant switches.
2. Configured IP addressing
   - Configured the IT network using the `192.168.10.0/24` subnet.
   - Configured the Sales network using the `192.168.20.0/24` subnet.
   - Configured the HR network using the `192.168.30.0/24` subnet.
   - Set the relevant IP addresses, subnet masks, default gateways, and DNS settings on the end devices.
3. Tested connectivity between departments
   - Used `ping` from an HR PC to an IT PC to verify connectivity.
   - Used `ping` from a Sales PC to an IT PC to test the intended communication restriction.
4. Configured an extended access control list

   Created an ACL named `Sales-ACL` on the router to deny ICMP traffic from the Sales subnet to the IT subnet while permitting other IP traffic.
   ```
   Router(config)# ip access-list extended Sales-ACL
   Router(config-ext-nacl)# deny icmp 192.168.20.0 0.0.0.255 192.168.10.0 0.0.0.255
   Router(config-ext-nacl)# permit ip any any
   Router(config-ext-nacl)# interface g0/1
   Router(config-if)# ip access-group Sales-ACL in
   Router(config-if)# exit
   ```
   - Applied the ACL inbound on interface `g0/1`, as documented in the project.
   - The `deny icmp` rule blocks ICMP traffic from Sales to IT.
   - The `permit ip any any` rule permits other IP traffic not denied by earlier ACL entries.
5. Verified the ACL behaviour
   - Confirmed that the HR PC could successfully ping the IT PC.
   - Confirmed that the Sales PC could not successfully ping the IT PC.
   - These tests demonstrated the intended difference in ICMP connectivity.
6. Tested HTTP access
   - Opened the web browser on a Sales PC in Cisco Packet Tracer.
   - Accessed the TechNova Ltd server's HTTP service.
   - Confirmed that the server's web page was accessible from Sales, demonstrating that the ACL allowed this traffic.

## Results and Findings

The project achieved the following outcomes:

- Departmental network segmentation: IT, Sales, and HR were configured on separate IPv4 subnets.
- Successful HR-to-IT connectivity: The HR PC successfully pinged the IT PC.
- Restricted Sales-to-IT connectivity: The Sales PC's ping to the IT PC failed, consistent with the configured ICMP restriction.
- Controlled network access: The extended ACL demonstrated how traffic can be filtered according to its protocol and source and destination networks.
- HTTP service availability: Sales users could access the TechNova Ltd server's web service despite the ICMP restriction.

The project illustrates an important networking and cybersecurity principle: blocking one type of traffic does not necessarily prevent all communication. The ACL restricts ICMP traffic from Sales to IT while permitting other IP traffic, including HTTP, subject to routing and any other applicable controls.

The configuration is a practical demonstration of network segmentation, traffic filtering, connectivity testing, and basic access control. Further testing could verify other protocols and confirm that the ACL is applied to the intended interface and direction.

## Author

John Ndidi Okwudike

- Location: United Kingdom
- Field: Governance, Risk and Compliance (GRC), Networking, and Cybersecurity
- Career Goal: GRC Analyst
- Student ID: `GRC-C26-09-EU-009`
- GitHub: [Add your GitHub profile URL]
- LinkedIn: www.linkedin.com/in/john-n-okwudike
- Email: johnndidiokwudike@gmail.com
