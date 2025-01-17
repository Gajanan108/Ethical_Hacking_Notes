# 3. SMB solutions

### Step-by-Step Solution Using Enum4Linux tryhackme

In this scenario, we will use **Enum4Linux** to identify a machine with the SMB service enabled in the `192.168.0.0/24` subnet, find the SMB credentials for a user named "john," and obtain a file named `ctf.txt` that contains a secret. Finally, we will use John's password to decrypt the file. Here’s how to do it step by step:

### Step 1: Identify Machines with SMB Service

1. **Scan the Subnet**: First, we need to identify machines in the subnet. You can use `nmap` to find live hosts:
    
    ```
    nmap -sn 192.168.0.0/24
    
    ```
    
    This command will ping all the devices in the subnet and list the active ones.
    
2. **Run Enum4Linux**: Once you have the IP addresses of the active machines, use Enum4Linux to gather information about SMB shares and users. Replace `<IP_ADDRESS>` with the actual IP address of the target machine:
    
    ```
    enum4linux -a <IP_ADDRESS>
    
    ```
    
    This command will provide detailed information about the SMB service, including user accounts, shares, and more.
    

### Step 2: Find SMB Credentials for User "john"

1. **Look for User Information**: In the output from Enum4Linux, look for the section that lists users. If "john" is listed, take note of any additional information that might help in guessing or cracking his password.
2. **Check for Shares**: Enum4Linux will also list available shares. Look for any shares that might be accessible to "john."
3. **Brute Force (if necessary)**: If you do not have the password for "john," you can use a tool like `hydra` to perform a brute-force attack on the SMB service:
    
    ```
    hydra -l john -P /path/to/password_list.txt smb://<IP_ADDRESS>
    
    ```
    
    This command attempts to log in as user "john" using passwords from the specified list.
    

### Step 3: Obtain the `ctf.txt` File

1. **Access the Share**: Once you have the correct credentials for "john," use `smbclient` to access the share where `ctf.txt` is located. For example:
    
    ```
    smbclient //<IP_ADDRESS>/share_name -U john
    
    ```
    
    Replace `share_name` with the actual name of the share you found earlier.
    
2. **Download the File**: After connecting to the share, you can download the `ctf.txt` file using the following command within the `smbclient` prompt:
    
    ```
    get ctf.txt
    
    ```
    

### Step 4: Decrypt the `ctf.txt` File

1. **Check the File Type**: First, check if `ctf.txt` is encrypted. You can use the `file` command to see what type of file it is:
    
    ```
    file ctf.txt
    
    ```
    
2. **Decrypt the File**: If the file is encrypted (for example, using AES), you will need to use the appropriate decryption tool. If you know the encryption method, you can use a command like:
    
    ```
    openssl enc -d -aes-256-cbc -in ctf.txt -out decrypted.txt -k <john's_password>
    
    ```
    
    Replace `<john's_password>` with the password you obtained for user "john."
    
3. **View the Decrypted File**: After decryption, you can open the `decrypted.txt` file to view the secret it contains:
    
    ```
    cat decrypted.txt
    
    ```
    

### Summary

By following these steps using Enum4Linux, you can successfully identify a machine with SMB enabled, find the credentials for user "john," obtain the `ctf.txt` file, and decrypt it using John's password. Always remember to conduct such activities ethically and with permission!

### Step-by-Step Solution to the Scenario

In this scenario, we need to identify a machine with the SMB service enabled in the `192.168.0.0/24` subnet, find the SMB credentials for a user named "john," and obtain a file named `ctf.txt` that contains a secret. Finally, we will use John's password to decrypt the file. Here’s how to do it step by step:

### Step 1: Identify Machines with SMB Service

1. **Scan the Subnet**: Use a tool like `nmap` to scan the subnet for machines with the SMB service enabled. Open your terminal and run the following command:
    
    ```
    nmap -p 445 --open 192.168.0.0/24
    
    ```
    
    This command scans for open port 445, which is used by SMB.
    
2. **Review the Results**: Look for IP addresses in the output that indicate an SMB service is running. Note down the IP address(es) of the machines found.

### Step 2: Find SMB Credentials for User "john"

1. **Attempt to Access SMB Shares**: Use the `smbclient` command to list the shares on the identified machine. Replace `<IP_ADDRESS>` with the actual IP address you found:
    
    ```
    smbclient -L //<IP_ADDRESS> -U john
    
    ```
    
    You may need to try common passwords or use a password list if you don't have the password for "john."
    
2. **Brute Force (if necessary)**: If you don’t have the password, you can use a tool like `hydra` to perform a brute-force attack on the SMB service:
    
    ```
    hydra -l john -P /path/to/password_list.txt smb://<IP_ADDRESS>
    
    ```
    
    This command attempts to log in as user "john" using passwords from the specified list.
    

### Step 3: Obtain the `ctf.txt` File

1. **Access the Share**: Once you have the correct credentials for "john," use `smbclient` to access the share where `ctf.txt` is located. For example:
    
    ```
    smbclient //<IP_ADDRESS>/share_name -U john
    
    ```
    
    Replace `share_name` with the actual name of the share you found earlier.
    
2. **Download the File**: After connecting to the share, you can download the `ctf.txt` file using the following command within the `smbclient` prompt:
    
    ```
    get ctf.txt
    
    ```
    

### Step 4: Decrypt the `ctf.txt` File

1. **Check the File Type**: First, check if `ctf.txt` is encrypted. You can use the `file` command to see what type of file it is:
    
    ```
    file ctf.txt
    
    ```
    
2. **Decrypt the File**: If the file is encrypted (for example, using AES), you will need to use the appropriate decryption tool. If you know the encryption method, you can use a command like:
    
    ```
    openssl enc -d -aes-256-cbc -in ctf.txt -out decrypted.txt -k <john's_password>
    
    ```
    
    Replace `<john's_password>` with the password you obtained for user "john."
    
3. **View the Decrypted File**: After decryption, you can open the `decrypted.txt` file to view the secret it contains:
    
    ```
    cat decrypted.txt
    
    ```
    

### Summary

By following these steps, you can successfully identify a machine with SMB enabled, find the credentials for user "john," obtain the `ctf.txt` file, and decrypt it using John's password. Always remember to conduct such activities ethically and with permission!