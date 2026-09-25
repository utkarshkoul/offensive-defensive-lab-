# Basic Network Traffic Analysis with Wireshark

## Aim

To perform basic network traffic capture and analysis during an FTP session from Kali Linux to a target system using Wireshark.

## Theory

Wireshark is a network packet analyzer used to capture and inspect traffic flowing through a network. It helps in understanding how data is transmitted between devices and in identifying sensitive information exposed in transit.

FTP is a file transfer protocol that sends login credentials and file data in plain text unless protected by encryption. Because of this, attackers can use packet sniffing tools to capture and read user details such as usernames and passwords.

TCP divides data into packets and reassembles them at the receiver. Wireshark can follow a TCP stream to reconstruct the complete communication and reveal the actual contents of the session.

## Procedure

### 1. Obtain Target IP Address

Log in to Metasploitable 2 using credentials msfadmin/msfadmin and execute ifconfig to find the target IP address.

Commands used:
```bash
ifconfig
```

### 2. Run Nmap Port Scan

Open a terminal in Kali Linux and run the following command to confirm that port 21/tcp (FTP) is open.

Commands used:
```bash
sudo nmap -Pn <Target_IP>
```

### 3. Start Wireshark Capture

Launch Wireshark and double-click the active interface (eth0) to begin live packet capture.

Commands used:
```bash
wireshark &
```

![Step 1 Screenshot](screenshots/step_1.png)

### 4. Establish FTP Connection

In a terminal, connect to the target using FTP, log in with credentials msfadmin/msfadmin, and enter quit after successful authentication.

Commands used:
```bash
ftp <Target_IP>
```

Example login:
```bash
USER msfadmin
PASS msfadmin
quit
```

![Step 2 Screenshot](screenshots/step_2.jpeg)

### 5. Analyze TCP Stream

Stop the Wireshark capture, right-click any captured FTP/TCP packet, and select Follow -> TCP Stream.

Commands used:
```bash
tcp.stream eq 1
```

![Step 3 Screenshot](screenshots/step_3.jpeg)

Inspect the stream window to view the plain-text credentials (USER msfadmin and PASS msfadmin).

![Step 4 Screenshot](screenshots/step_4.jpeg)

![Step 5 Screenshot](screenshots/step_5.jpeg)

![Step 6 Screenshot](screenshots/step_6.jpeg)

## Result

Network traffic was successfully captured during the FTP session. Reassembling the TCP stream exposed the unencrypted login credentials (USER msfadmin / PASS msfadmin) transmitted across the wire.

## Conclusion

Basic network traffic analysis using Wireshark demonstrated that plain-text protocols like FTP transmit sensitive authentication data without encryption, making them vulnerable to network sniffing.
