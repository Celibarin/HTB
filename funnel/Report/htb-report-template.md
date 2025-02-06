---
title: "Hack the Box XXXXXXXXXXXXXXX Report"
author: ["Celibarin"]
date: "2020-07-25"
subject: "Markdown"
keywords: [Markdown, Example]
subtitle: "Hack the Box XXXXXXXXXXXXXXX Report"
lang: "en"
titlepage: true
titlepage-color: "1E90FF"
titlepage-text-color: "FFFAFA"
titlepage-rule-color: "FFFAFA"
titlepage-rule-height: 2
book: true
classoption: oneside
code-block-font-size: \scriptsize
---
# Hack the Box XXXXXXXXXXXXXXX Report

## Introduction

This Hack the Box penetration test report contains all efforts that were conducted in order to compromise this Hack the Box XXXXXXXXXXXXXXX system.

## Objective

The objective of this assessment is to perform an internal penetration test against the Hack the Box XXXXXXXXXXXXXXX system.

# High-Level Summary

I was tasked with performing an internal penetration test towards Hack the Box XXXXXXXXXXXXXXX.
An internal penetration test is a dedicated attack against internally connected systems.
The focus of this test is to perform attacks, similar to those of a hacker and attempt to infiltrate the XXXXXXXXXXXXXXX system.
My overall objective was to evaluate the network, identify systems, and exploit flaws while reporting the findings.

When performing the internal penetration test, there were several alarming vulnerabilities that were identified on XXXXXXXXXXXXXXX.
When performing the attacks, I was able to gain access to the machine, primarily due to XXXXXXXXXXXXXXX.
The system was successfully exploited and access granted.
The system as well as a brief description on how access was obtained is listed below:

- 10.10.10.xx (hostname) - Name of initial exploit

## Recommendations

I recommend patching the vulnerabilities identified during the testing to ensure that an attacker cannot exploit these systems in the future.
One thing to remember is that these systems require frequent patching and once patched, should remain on a regular patch program to protect additional vulnerabilities that are discovered at a later date.

# Methodologies

I utilized a widely adopted approach to performing penetration testing that is effective in testing how well the XXXXXXXXXXXXXXX system is secured.
Below is a breakout of how I was able to identify and exploit the system and includes all individual vulnerabilities found.

## Information Gathering

The information gathering portion of a penetration test focuses on identifying the scope of the penetration test.
During this penetration test, I was tasked with exploiting XXXXXXXXXXXXXXX.
The specific IP address was:

- 10.10.10.xx

## Penetration

The penetration testing portions of the assessment focus heavily on gaining access to the XXXXXXXXXXXXXXX system.
During this penetration test, I was able to successfully gain access to the system.

### System IP: 192.168.x.x

#### Service Enumeration

The service enumeration portion of a penetration test focuses on gathering information about what services are alive on a system or systems.
This is valuable for an attacker as it provides detailed information on potential attack vectors into a system.
Understanding what applications are running on the system gives an attacker needed information before performing the actual penetration test.
In some cases, some ports may not be listed.

Server IP Address | Ports Open
------------------|----------------------------------------
192.168.x.x       | **TCP**: \
**UDP**: 

**Nmap Scan Results:**

*Initial Shell Vulnerability Exploited*

*Additional info about where the initial shell was acquired from*

**Vulnerability Explanation:**

**Vulnerability Fix:**

**Severity:**

**Proof of Concept Code Here:**

**Local.txt Proof Screenshot**

**Local.txt Contents**

#### Privilege Escalation

*Additional Priv Esc info*

**Vulnerability Exploited:**

**Vulnerability Explanation:**

**Vulnerability Fix:**

**Severity:**

**Exploit Code:**

**Proof Screenshot Here:**

**Proof.txt Contents:**


## Maintaining Access

Maintaining access to a system is important to us as attackers, ensuring that we can get back into a system after it has been exploited is invaluable.
The maintaining access phase of the penetration test focuses on ensuring that once the focused attack has occurred (i.e. a buffer overflow), we have administrative access over the system again.
Many exploits may only be exploitable once and we may never be able to get back into a system after we have already performed the exploit.

## House Cleaning

The house cleaning portions of the assessment ensures that remnants of the penetration test are removed.
Often fragments of tools or user accounts are left on an organization's computer which can cause security issues down the road.
Ensuring that we are meticulous and no remnants of our penetration test are left over is important.

After collecting trophies from the exam network was completed, I removed all user accounts and passwords as well as the Meterpreter services installed on the system.
Offensive Security should not have to remove any user accounts or services from the system.

# Additional Items

## Appendix - Proof and Local Contents:

IP (Hostname) | user.txt Contents  | root.txt Contents
--------------|--------------------|-------------------
10.10.10..x   | hash_here          | hash_here


## Appendix - Complete Walkthrough

```
code here
```
