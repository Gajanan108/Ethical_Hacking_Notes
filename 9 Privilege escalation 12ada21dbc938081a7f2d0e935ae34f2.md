# 9. Privilege escalation

Here’s a step-by-step guide to exploit the credentials obtained via shoulder surfing and escalate privileges to access root.txt on an Ubuntu machine.

---
Task: Privilege Escalation to Access root.txt
You observed a user entering credentials on an Ubuntu machine, which you’ve noted. Now, use these credentials to gain access to the system and perform vertical privilege escalation to get administrator (root) access and retrieve the root.txt file.

---
1. Assume the Environment Setup
Target Subnet: 192.168.0.0/24
Observed Username and Password: Assume username is user and password is user_password.
Target File: root.txt (located in the /root directory)
Tools: SSH, sudo, Linpeas (for privilege escalation checks)

---
Step-by-Step Guide:
Step 1: Identify the Target Machine
Use Nmap to scan the subnet and identify the IP address of the Ubuntu machine. You’re looking for machines with SSH open on port 22:
`nmap -p 22 192.168.0.0/24`
Note down the IP address of any machines that have port 22 open. Let’s assume the IP address of the target machine is 192.168.0.10.

Step 2: Access the Machine Using SSH
Now, use the credentials (user:user_password) you observed to log into the target machine via SSH:
`ssh user@192.168.0.10`
Enter the observed password (user_password). Once logged in, verify you have user-level access.

Step 3: Check sudo Permissions
Check if the user has sudo privileges, as this could allow you to elevate privileges to root. Run:
`sudo -l`
If the user has ALL permissions without requiring a password, you can escalate directly to root by running:
`sudo su`
If sudo permissions are restricted or require a password, proceed to the next step for privilege escalation techniques.

Step 4: Use **Linpeas** to Enumerate Privilege Escalation Paths
Linpeas is a script used to enumerate privilege escalation opportunities on Linux systems. Download and run Linpeas to identify possible weaknesses:
1. Download Linpeas on your local machine:
`wget https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh`

2. Upload Linpeas to the target machine (if you have local SSH access, you can use scp):
`scp linpeas.sh user@192.168.0.10:/tmp`

3. On the target machine, run Linpeas:
`chmod +x /tmp/linpeas.sh/tmp/linpeas.sh`

Review the Linpeas output for potential privilege escalation vectors, such as writable files, scheduled tasks, or vulnerable services running as root.

Step 5: Exploit Identified Privilege Escalation Paths
Based on Linpeas output, exploit any available methods. Here are some common methods:
Exploitable Sudo Permissions: If a binary with potential for privilege escalation (e.g., nano, vim, less, find) is executable with sudo, you can run it with elevated permissions to gain root access.
Writable Scripts or Cron Jobs: If any root-owned scripts are writable by your user, you can insert a command to spawn a root shell.

Example: If the user has sudo access to find, run:
`sudo find . -exec /bin/sh \;`

Step 6: Retrieve the root.txt File
Once you have root access, navigate to the /root directory:
`cd /root`
Use cat to read the contents of root.txt:
`cat root.txt`
Document the contents of root.txt as required.

---
Summary:
1. Nmap was used to identify the target Ubuntu machine.

2. SSH was used to log into the machine using credentials obtained via shoulder surfing.

3. sudo and Linpeas helped find potential privilege escalation paths.

4. Privilege escalation was achieved to gain root access.

5. The contents of root.txt were retrieved and documented.

Let me know if you’d like to dive deeper into any of these steps or need clarification on specific commands!

Another method 

In the CEH (Certified Ethical Hacker) exam and iLab environment, commonly used tools for privilege escalation are Linux commands, sudo checks, and Metasploit modules, rather than community scripts like Linpeas. Here’s an alternative approach focusing on these tools to escalate privileges on a Linux system.

---
Scenario: Privilege Escalation to Access root.txt Using CEH-Approved Methods
After obtaining the credentials for a standard user on a Linux machine (e.g., user:user_password), your task is to escalate privileges and retrieve the file root.txt located in the /root directory.

---
1. Assume the Environment Setup
Target Machine IP: 192.168.0.10 (based on previous reconnaissance)
User Credentials: user:user_password
Objective: Escalate privileges to access /root/root.txt
Tools: sudo, Nmap, Metasploit, Linux Commands

---
Step-by-Step Guide:
Step 1: Check User Privileges with sudo
Log into the target machine using the observed credentials:
`ssh user@192.168.0.10`
Once logged in, check the sudo privileges for the current user:
`sudo -l`
Analyze the output to see if the user can run any commands as root. Here are some common scenarios:
If the user has ALL privileges without a password, you can switch directly to root:
`sudo su`
If specific commands like vim, nano, find, or less are allowed, you might be able to exploit them for privilege escalation.

Step 2: Exploiting Allowed Sudo Commands for Privilege Escalation
If you have sudo access to a command like vim or nano, use it to escalate privileges:
Example with vim:
`sudo vim -c ':!/bin/bash'`
This command opens a root shell from within vim by executing the shell command :!/bin/bash.
Example with find:
`sudo find . -exec /bin/sh \; -quit`
This uses find to execute a shell with root privileges.

Step 3: Use Metasploit for Exploiting Kernel Vulnerabilities
If sudo permissions don’t offer privilege escalation, check the Linux kernel version to identify possible vulnerabilities:
`uname -a`
Open Metasploit on your local machine, search for exploits specific to the kernel version, and create a Meterpreter session:
1. Launch Metasploit:
`msfconsole`

2. Search for kernel-specific exploits:
`search linux/local`

3. Select an exploit, set options, and run it to gain root access on the machine.

Step 4: Access and Read root.txt
Once you have root privileges (via sudo, a root shell, or Metasploit), navigate to the /root directory:
`cd /root`
Use cat to read the contents of root.txt:
`cat root.txt`

---
Summary:
1. SSH login to the target machine using observed credentials.

2. sudo -l to check for available commands that could allow privilege escalation.

3. Use Metasploit for exploiting kernel vulnerabilities if sudo is limited.

4. After gaining root access, retrieve the root.txt contents.

This approach uses tools and commands typical for CEH labs and exams. Let me know if you’d like another example!