<h1 = align=center>NETWORK MONITORING LAB - WITH VIRTUAL ROUTER REDUNDANCY PROTOCOL (VRRP) </h1>

<p align="center">
<img width="756" height="883" alt="Untitled Diagram drawio (3)" src="https://raw.githubusercontent.com/DanielTsang26/network-monitoring-lab/refs/heads/main/network_admin_lab.png" />
</p>

## 📌 Introduction

This lab introduces essential network administration tasks such as system logging, traffic monitoring, and router redundancy.  There will be configurations Syslog for centralized logging, NetFlow for traffic analysis, and VRRP for high availability.


## 🛠️ TECHNOLOGY & TOOLS UTILIZED
- **`VirtualBox:`**  
  Used as the primary virtualization platform to host multiple virtual machines in an isolated local environment for cybersecurity testing and infrastructure simulation.

- **`NetFlow (Traffic Monitoring):`**  
  Monitors and exports IP traffic data to a collector

- **`OS/Platform:`**  
  Linux;Hosts router/firewall, `syslog server` , `NetFlow` exporter/collector

- **`VRRP (Virtual Router Redundancy Protocol):`**  
A protocol that is used to provide redundancy and failover in a network. It enables the routers in a virtual router group to sharet he same IP address and provides a mechanism for quickly switching the IP address from one router to another in the event of a failure.


## OBJECTIVES:

The objective of the Network Monitoring Lab is to provide hands-on experience in configuring and monitoring essential network services. 
Specifically this lab aims to:

- Configure and verify Syslog for centralized event logging.
- Set up and analyze NetFlow exports for traffic monitoring.
- Implement VRRP for router redundancy and high availability.
- View and interpret interface statistics to assess network device health.

## Step-by-Step Instructions

###  Step 1: Establish the Telnet Connection

Launch the PuTTY SSH Client. The PuTTY Configuration dialog box will appear on the screen

## Step 2: Host name & Port & Telnet

Type Host Name as 192.169.116.128 and port as 5003

<img width="431" height="421" alt="Lab 1" src="https://raw.githubusercontent.com/DanielTsang26/network-monitoring-lab/refs/heads/main/network_admin_lab2.png" /></br>

<img width="131" height="121" alt="Lab 1" src="https://raw.githubusercontent.com/DanielTsang26/network-monitoring-lab/refs/heads/main/network_admin_lab3.png" /></br>

<img width="431" height="321" alt="Lab 1" src="https://raw.githubusercontent.com/DanielTsang26/network-monitoring-lab/refs/heads/main/network_admin_lab4.png" /></br>

## Step 3: Configuring Syslog and Observing the Log Settings

Execute the following comands to enter into the configuration mode and configure Syslog:

```bash
- configure terminal
- logging console 7
- logging monitor debug
- logging buffered 4
- logging host 192.168.2.100
- logging trap warning
- end
```
<img width="431" height="421" alt="Lab 1" src="https://raw.githubusercontent.com/DanielTsang26/network-monitoring-lab/refs/heads/main/network_admin_lab5.png" /></br>

**NOTE:**
- The `configure terminal` command allows users to enter globabl mode/configuration commands.
- The `logging console 7` command causes IOS to send severity level 0-7 messages to the console.
- The `logging monitor debug` command limits messages logged to the terminal lines.
- THe `logging buffered 4` command logs messages to an internal buffer. The default buffer size is 4096
- The logging host `192.168.2.100` command logs messages to a UNIX Syslog server host.
- The `logging trap warning` command limits messages logged  to the Syslog servers.

## Step 4: Show Logging 

Execute the  following command to display the state of system logging (Syslog) and the contents of the standard system logging buffer. Afterwards, you may close the terminal.

```bash
show logging
```
<img width="531" height="521" alt="Lab 1" src="https://raw.githubusercontent.com/DanielTsang26/network-monitoring-lab/refs/heads/main/network_admin_lab6.png" /></br>

## Step 5: Viewing Interface Statistics and Status:

Execute the following command to display information of about the status, configuration, and statistics of interface e0/0:

```bash
show interface eo/0
```
<img width="531" height="521" alt="Lab 1" src="https://raw.githubusercontent.com/DanielTsang26/network-monitoring-lab/refs/heads/main/network_admin_lab7.png" /></br>

## Step 6: Configuring NetFlow

Open the PuTTY SSH Client Configuration and type Host Name as 192.169.116.128 and port as 5017.

<img width="531" height="521" alt="Lab 1" src="https://raw.githubusercontent.com/DanielTsang26/network-monitoring-lab/refs/heads/main/network_admin_lab8.png" /></br>

After the terminal is opened up, configure the NetFlow with the following commands:

```bash
- configure terminal
- ip flow-export version 9
- ip flow-export destination 192.168.0.100 9999
- interface e0/0
- ip flow ingress
- end

```

<img width="531" height="521" alt="Lab 1" src="https://raw.githubusercontent.com/DanielTsang26/network-monitoring-lab/refs/heads/main/network_admin9.png" /></br>

**NOTES:**
- The `configure terminal` command allows users to enter globabl mode/configuration commands.
- The `ip flow-export version 9` command instructs the router to export flow data in NetFlow version 9 format when sending it to the NetFlow collector.
- The ` ip flow-export destination` 192.168.0.100 9999 command is used to set the destination Ip address to 192.168.0.100 and the port number to 9999.
- The `interface e0/0` command is uesd to specify and enter interface configuration mode for the Ethernet interface 0/0.
- The `ip flow ingress` command is used to enable NetFlow ont he ingress(incoming) traffic of an interface.
- The `ip flow egress` command is used to enable NetFlow on the egress (outgoing) traffic of an interface.

 ## Step 7: Verifying NetFlow

 In the terminal where NetFlow is being executed, verify netFlow with the following commands:

```bash
show ip flow interace
show ip flow export
```


<img width="531" height="521" alt="Lab 1" src="https://raw.githubusercontent.com/DanielTsang26/network-monitoring-lab/refs/heads/main/network_admin_lab10.png" /></br>


## Step 8: Configuration of Virtual Router Redundancy Protocol (VRRP)

Open the PuTTY SSH Client Configuration and type Host Name as 192.169.116.128 and port as 5010, along with the `Other` radio button selected.

<img width="431" height="421" alt="Lab 1" src="https://raw.githubusercontent.com/DanielTsang26/network-monitoring-lab/refs/heads/main/network_admin_lab11.png" /></br>

<img width="131" height="121" alt="Lab 1" src="https://raw.githubusercontent.com/DanielTsang26/network-monitoring-lab/refs/heads/main/network_admin_lab12.png" /></br>

<img width="431" height="321" alt="Lab 1" src="https://raw.githubusercontent.com/DanielTsang26/network-monitoring-lab/refs/heads/main/network_admin_lab13.png" /></br>

Enter the following commands:

```bash
- configure terminal
- int e0/0
- vrrp 20 ip 10.0.0.3
```
<img width="431" height="421" alt="Lab 1" src="https://raw.githubusercontent.com/DanielTsang26/network-monitoring-lab/refs/heads/main/network_admin_lab14.png" /></br>

**NOTES:**
- The `configure terminal` command allows users to enter globabl mode/configuration commands.
- The `int e0/0` command is used to specify the interface 0/0.
- The `vrrp 20 ip 10.0.0.3` command enables VRRP on the interface e0/0

After you minimize the terminal involving VRRP. Open the PuTTY SSH Client Configuration and type Host Name as 192.169.116.128 and port as 5011, along with the `Other` radio button selected.

Enter the following commands:

```bash
- configure terminal
- int e0/0
- vrrp 20 ip 10.0.0.3
```

<img width="431" height="421" alt="Lab 1" src="https://raw.githubusercontent.com/DanielTsang26/network-monitoring-lab/refs/heads/main/network_admin_lab15.png" /></br>

The state of the VRRP group, which can be one of the following: 
- Master/ Active: The router that is currently serving as the active virtual router and forwarding traffic for the group
- backup/Standby: he routers that are in standby mode, ready to take over if the master router fails.
- Init: The intial state whe VRRP is first started or during intialization
- Other: A transitional state while the router is the process of transistioning between active and standby role.

Close all windows after this is setup.

---

*This hands-on exercise provided a practical understanding of network health through monitoring and tracking traffic using tools like Syslog and NetFlow.

### 🔑 Key Takeaways

-  Learned how to configure routers to export system logs to a centralized Syslog server, enabling real-time monitoring of network events and device status.
-  Set up NetFlow to collect and analyze IP traffic patterns, providing visibility into bandwidth usage, communication paths, and network behavior.
-  Implemented VRRP to ensure continuous connectivity by assigning a virtual IP to multiple routers, demonstrating failover capabilities and network resilience.
-  Viewed and interpreted interface statistics to assess operational status, detect packet loss or errors, and confirm link health.
-  Through configuring services and observing behavior, gained practical skills in maintaining, troubleshooting, and securing a basic network infrastructure.
