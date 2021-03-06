---
layout: default
course_number: CS497
title: "Lab 5 - TCP/IP Attack Lab"
---

# TCP/IP Attack Lab

### Lab Description and Tasks

[TCP/IP Attack Lab](TCP_Attacks.pdf)

Additional information on the SEED project [site](http://www.cis.syr.edu/~wedu/seed/Labs_16.04/Networking/TCP_Attacks/). 

### Reference Slides

- [Networks: IP and TCP](../lectures/Ch05-NetworksTCP-IP.pdf)
- [CS 330 Transport Layer](tcp/lecture6_transport_layer.pdf) - slide 48 may help

### Source Files
- [Task 2 skeleton code](tcp/rst_attack.py)
- [Task 4 skeleton code](tcp/session_hijack.py)

### Grading

Post your report in [Marmoset](https://cs.ycp.edu/marmoset) by the scheduled due date in the syllabus. Your grade for this lab will be composed of:
- 30% - Design
- 30% - Observations
- 40% - Explanation
- **You must provide a screenshot of the network traffic with each attack.**
- *You also need to provide explanation to the observations that are interesting or surprising.*
- *Extra Credit* if you pursue further investigation, beyond what is required by the lab description.

### Tips
- Install scapy by ```sudo apt install python-scapy```  
- Use ```netstat -na | grep tcp``` to check teh usage of the *TCP* queue before and after each attack. 
- Wireshark
  - To enable auto scroll: Go -> Auto Scroll in Live Capture 
  - To view the ```Next Sequence Number``` - find a TCP packet that doesn't have a zero length payload (```tcp.len > 0``` filter)
  - To filter only telnet packets, use ```tcp.port=23``` 
- **Task #1** - you can use ```raw``` for the ```-s``` option, for example: ```netwox 76 -i 192.168.1.73 -p 23 -s raw```
- **Task #2** - use ```netwox 40``` instead of ```netwox 78```
- **Task #3** - use ```netwox 78``` 
- **Task #4** - create a directory on the server with a single file in it. Try to delete the file by injecting malicious contents into the client server telnet session. Use ```\r rm *\n\r```.
- To make your script executable: ``` $ chmod +x your_script.py```
- **Task #5** - start the listener ```nc lv 9090``` before you launch the attack 

### Expected Behavior 
- Task 1 - SYN Flooding
  - <a href="./tcp/syn_flooding_attack.png" target="_blank">SYS Flooding Attack</a> - you can see many half open connections from random IP addresses. 
  - <a href="./tcp/syn_flooding_attack_netstat.png" target="_blank">SYS Flooding Attack - netstat</a> - same here, just using ```netstat -na | grep tcp```
- Task 2 - running the attack kills the TCP connection
  - <a href="./tcp/tcp_rst_attack_telnet.png" target="_blank">TCP RST Attack on telnet</a> 
  - <a href="./tcp/tcp_rst_attack_ssh.png" target="_blank">TCP RST Attack on ssh</a> 
- Task 4 
  - <a href="./tcp/tcp_session_hijack.png" target="_blank">TCP Session Hijack</a> 
- Task 5 - Reverse Shell 
  - <a href="./tcp/reverse_shell.png" target="_blank">Creating Reverse Shell using TCP Session Hajacking</a> via scapy and the <a href="./tcp/reverse_shell_scrapy_file.png" target="_blank">file</a> I used 
  - <a href="./tcp/reverse_shell_netwox.png" target="_blank">Creating Reverse Shell using TCP Session Hajacking</a> via netwox 
