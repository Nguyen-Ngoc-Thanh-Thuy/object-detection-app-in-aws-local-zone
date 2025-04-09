---
title : "Install and configure Openswan VPN in the AWS Local Zone"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 5.3 </b> "
---

**1. Access EC2 Instance**
+ Go to [EC2 service management console](https://console.aws.amazon.com/ec2/v2/home).
+ Select the **'LocalZone-vpn-instance'** created earlier in step 1 of section C.
![EC2 Security Group](/images/5.sectionc/025-ec2security.png)
+ Update its security group:
  - Choose the security group **my-vpnlocalzone-sg**.
  ![Security Group](/images/5.sectionc/026-sg.png)
  - Select **"Edit inbound rules"**.
  ![Security Group](/images/5.sectionc/027-sg.png)
  - **Modify inbound rules**: Open TCP ports 4500 and 500 for the public IP address found in the Openswan configuration file. Remove "0.0.0.0/0" in the inbound rules, and instead add the Public IP from the Openswan configuration file.
  ![VPN configuration file](/images/5.sectionc/024-configfile.png)
  ![Edit inbound rules](/images/5.sectionc/028-inboundrule.png)
+ Connect to the VPN instance using **AWS SSM**.
![SSM Connect](/images/5.sectionc/029-ssmconnect.png)
![SSM Connect](/images/5.sectionc/030-ssmconnect.png)

**2. Install Openswan**
```
/bin/bash
sudo su
yum install openswan -y
```
![Openswan](/images/5.sectionc/031-openswan.png)

**3. Configure Openswan**
+ Edit the **sysctl.conf** file.
```
vi /etc/sysctl.conf
```
![Openswan](/images/5.sectionc/032-openswan.png)
+ Add the following lines.
```
net.ipv4.ip_forward = 1
net.ipv4.conf.default.rp_filter = 0
net.ipv4.conf.default.accept_source_route = 0
```
![Openswan](/images/5.sectionc/033-openswan.png)

+ Run this command.
```
sysctl -p
```
![Openswan](/images/5.sectionc/034-openswan.png)

**4. Configure IPSec**
+ Edit the file **/etc/ipsec.conf**:
```
vi /etc/ipsec.conf
```
![Openswan](/images/5.sectionc/035-openswan.png)

+ Ensure the line **#include /etc/ipsec.d/*.conf** is uncommented (no # at the beginning).
![Openswan](/images/5.sectionc/036-openswan.png)

+ Open the file **/etc/ipsec.d/aws.conf**.
![Openswan](/images/5.sectionc/037-openswan.png)
+ Replace placeholders with actual values from our Openswan configuration file:
  - Public IP of OpenSwan/CGW → Public IP of the VPN EC2 instance.
  - Public IP of VGW - Tunnel 1 → Public IP from the Openswan config file.
  - LOCAL NETWORK → The AWS Local Zone CIDR (```10.0.0.0/24```).
  - REMOTE NETWORK → Our stimulated on-premise CIDR (```172.16.0.0/24```).
  ```
  conn Tunnel1
    authby=secret
    auto=start
    left=%defaultroute
    leftid=<Public IP of OpenSwan/CGW>
    right=<Public IP of VGW - Tunnel 1>
    type=tunnel
    ikelifetime=8h
    keylife=1h
    phase2alg=aes128-sha1;modp1024
    ike=aes128-sha1;modp1024
    keyingtries=%forever
    keyexchange=ike
    leftsubnet=<LOCAL NETWORK>
    rightsubnet=<REMOTE NETWORK>
    dpddelay=10
    dpdtimeout=30
    dpdaction=restart_by_peer
  ```
  ![Openswan](/images/5.sectionc/038-openswan.png)
  

**5. Create secrets file**
+ Copy the secret from our Openswan configuration file.
![Openswan](/images/5.sectionc/039-openswan.png)

+ Create the file **/etc/ipsec.d/aws.secrets**.
```
vi /etc/ipsec.d/aws.secrets 
```
![Openswan](/images/5.sectionc/040-openswan.png)

+ Paste the **pre-shared-key value**.
```
Customer-GW-IP  Virtual Private Gateway-IP:  PSK  "<Pre-Shared-key value>"
```
![Openswan](/images/5.sectionc/041-openswan.png)


**6. Start Openswan VPN Service**
+ Run the following commands to start the Openswan VPN service and check its status.
```
systemctl start ipsec
systemctl status ipsec
```
![Openswan](/images/5.sectionc/042-openswan.png)


**7. Verify VPN Connection**
+ Search for **VPC** in the console. On the left panel, select **Site-to-Site VPN connections**.
+ Select the **"vpn-OnPremise-LocalZone"** connection and ensure the status is **"Up"** (it may take up to 5 minutes).
![Openswan](/images/5.sectionc/043-openswan.png)


  {{%notice info%}}
  Only 1 tunnel should be **"Up"** for this workshop.
  {{% /notice %}}