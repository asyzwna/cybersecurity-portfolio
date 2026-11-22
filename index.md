---
layout: home
title: Cybersecurity Portfolio
---

Welcome to my cybersecurity portfolio.

## About me
I am a Master of Cybersecurity student at Universiti Malaya (UM). I completed my degree in Computer Science (Information Security) at Universiti Tun Hussein Onn Malaysia (UTHM), then worked as a Technology Engineer at Esri Malaysia, where I supported customer enablement through ArcGIS technology updates, workshops and system assessments.

Working with real systems and clients showed me how much organisations rely on technology that must be secure, and that motivated me to specialise in cybersecurity. I returned to study so I can move from building and supporting systems to protecting them.

My Master's coursework includes Network Technology and Security, Advanced Network Security Programming, and Advanced Computer Penetration and Defence, taking me from how networks work, to automating security tasks with Python, to testing systems for weaknesses and defending them. I apply these skills through hands-on lab projects, which I document in this portfolio.

## Technical skills

Levels: **Beginner** (learned and practised in guided settings), **Working knowledge** (can do it independently on routine tasks), **Confident** (can do it reliably and explain it to others).

| Skill | Level | Evidence |
|---|---|---|
| Virtual lab setup and network isolation (VirtualBox, Kali Linux, Metasploitable 2) | Working knowledge | [Virtual lab project](projects/virtual-lab-setup/) |
| Network scanning and service enumeration (Nmap) | Beginner | [Virtual lab project](projects/virtual-lab-setup/) |
| Interpreting scan results to identify risky services | Beginner | [Virtual lab project](projects/virtual-lab-setup/) |
| Email header and authentication analysis (SPF, DKIM, DMARC) | Beginner | [Email threat investigation](projects/email-threat-investigation/) |
| Phishing and business email compromise recognition | Working knowledge | [Email threat investigation](projects/email-threat-investigation/) |
| Networking fundamentals (TCP/IP, IP addressing, switching and routing) | Working knowledge | [CCNA: Introduction to Networks](https://www.credly.com/badges/c50cebea-07a5-4f18-b834-2d4e88a65c4b), HTB Network Foundations |
| Security fundamentals (threats, risk, controls) | Working knowledge | [CompTIA Security+](https://www.credly.com/badges/e1575d7c-ad23-44ce-8a2c-f59b09e2adf5), HTB Introduction to Information Security |
| Linux basics | Working knowledge | Degree coursework, TryHackMe Linux room |
| Technical workshops and customer system assessments | Confident | Experience at Esri Malaysia |

## Certifications and training

**Earned certifications**
- CompTIA Security+ ce, issued by CompTIA, December 2024 (expires December 2027). [Verify on Credly](https://www.credly.com/badges/e1575d7c-ad23-44ce-8a2c-f59b09e2adf5)

**In progress**
- ISC2 Certified in Cybersecurity (CC), target date: December 2027.
- TryHackMe Cyber Kill Chain room, target date: December 2026.
- Cybersecurity and Network for Industry 4.0 Programme, SHRDC, expected completion: December 2026.

**Training completed**
- CCNA: Introduction to Networks, Cisco Networking Academy, 2021. [Verify on Credly](https://www.credly.com/badges/c50cebea-07a5-4f18-b834-2d4e88a65c4b)
- Cybersecurity training, APAC Cybersecurity Fund Malaysia, 2026.

**Practice platforms**
- [Hack The Box Academy](https://profile.hackthebox.com/profile/01a0c7b5-683f-71a6-97d6-28ef84b45fba): Completed the Introduction to Academy, Introduction to Information Security and Network Foundations modules.
- [TryHackMe](https://tryhackme.com/p/syazweenalyaa): Completed five introductory rooms: Linux Fundamentals, Offensive Security Intro, Defensive Security Intro, Search Skills.

**Formal coursework:** MSc Cybersecurity, Universiti Malaya (in progress)

## Projects

### 1. Virtual lab setup and Nmap service scan
**Folder:** [projects/virtual-lab-setup](projects/virtual-lab-setup/)

I built an isolated VirtualBox lab with Kali Linux and Metasploitable 2 on a host-only network, proved it had no internet access, and ran an Nmap service and version scan to identify exposed services and explain why they are risky.

**Skills shown:** virtual lab setup, network isolation, Nmap service detection, interpreting scan results.

### 2. Email threat investigation
**Folder:** [projects/email-threat-investigation](projects/email-threat-investigation/)

I analysed 13 emails from a fictional finance executive's mailbox, checking headers, SPF, DKIM and DMARC results, links, attachments and social-engineering techniques, and classified each as safe, medium risk or suspicious. I also compiled the indicators of compromise and recommended actions.

**Skills shown:** email header and authentication analysis, phishing and business email compromise recognition, indicator collection, incident reporting.

## Learning journey

Moving from supporting customer systems to studying cybersecurity has changed how I approach technology. I now ask how a system could be attacked and how it should be defended.

In my virtual lab, I built an isolated VirtualBox network with Kali Linux and a deliberately vulnerable Metasploitable 2 machine, both on a host-only adapter. I confirmed the two machines could reach each other with ping, then proved the lab was isolated when Kali could not reach google.com. I then ran an Nmap service and version scan against the target, which found 23 open ports, including FTP, Telnet and a service Nmap described as a root shell. What I took from this is that a version scan turns a list of open ports into something I can reason about, because it names the software and its version and shows what to check and patch first.

In the network monitoring and tools topic, I learned how analysts see what is happening on a network and on endpoints. In my home lab, I used Wireshark to monitor live traffic, which let me look at the packets behind the activity on my network. Analysts use the same approach to spot unusual communication, such as a compromised computer contacting an unknown external address. I also learned how Wazuh collects logs and raises alerts on events such as a new user account or a changed system file. Separately, in a Wazuh course, I reviewed threat-hunting events, fixed a failed configuration check and confirmed with a vulnerability rescan that an issue was resolved. What I took from this is that monitoring and fixing belong together: an alert only matters if someone investigates it and checks that the fix worked.

One thing went wrong when I switched my VM to the host-only adapter and did not restart it. I expected the lab to be isolated, but the VM could still reach the internet. I checked the network connection and found it was still using NAT, so my change had not taken effect. I shut the VM down, set the adapter to host-only again and started it. Afterwards the internet test failed as it should, which confirmed that the lab was isolated. The lesson is that a setting changed in VirtualBox is not proof that it is active. I now test the behaviour, for example by trying to reach an external website, before I trust a setup.

One tool I still find challenging is GNS3, the network emulator. The hardest part is getting the device images to work: an image has to be obtained legitimately, imported correctly and compatible with the emulator before a device will start, and when one fails it is not always clear why. To improve, I am learning from the official GNS3 documentation and from community forums, and I am applying what I learn in a course assignment that uses GNS3.

My goal is to build a small GNS3 topology of my own, with at least two devices communicating, by 31 January 2027. I will measure this by publishing a short write-up in this portfolio with a topology screenshot and successful ping results between the devices.

Overall, these experiences taught me to check my assumptions with evidence, a habit I want to carry into my work as a cybersecurity consultant.

## Career objective
My goal is to become a cybersecurity consultant who helps organisations assess and strengthen the security of their systems. My background in information security, my CompTIA Security+ certification, and my experience delivering workshops and system assessments for customers at Esri Malaysia give me a view of both the technical and the client-facing side of this work.

My next steps are:
1. Complete my Master's in cybersecurity at UM, focusing on penetration testing and network defence.
2. Earn the ISC2 Certified in Cybersecurity (CC) certification by December 2027.
3. Publish at least two hands-on projects in this portfolio, including a vulnerability assessment of my own virtual lab, to show practical skills.

I also want to build my communication and reporting skills, since a consultant must explain technical risks clearly to non-technical decision makers.

## Contact information

- **Email:** syazweenalyaa@gmail.com
- **GitHub:** [github.com/asyzwna](https://github.com/asyzwna)
- **LinkedIn:** [linkedin.com/in/alya-syazweena](https://www.linkedin.com/in/alya-syazweena)
