# 1. Scan Targets get FQDN

To perform an extensive scan of the target network and identify the Fully Qualified Domain Name (FQDN) of the domain controller using **Nmap**,

---

### Step 1: **Determine the Network Range**

Assume the network range is `192.168.1.0/24` (replace with your actual target network). If the range is unknown, you can use `ipconfig` (Windows) or `ifconfig` (Linux) to find your IP and calculate the subnet range.

---

### Step 2: **Run an Extensive Nmap Scan**

Run an **Nmap script scan** with service detection and hostname enumeration enabled:

```bash
nmap -sC -sV --script "ldap*,smb*,dns*" -p 53,88,135,139,389,445,464,636,3268,3269,3389 192.168.1.0/24

```

**Explanation of Flags**:

- `sC`: Use default Nmap scripts.
- `sV`: Enable service version detection.
- `-script "ldap*,smb*,dns*"`: Use Nmap scripts for LDAP, SMB, and DNS protocols, common for domain controllers.
- `p`: Scan ports related to domain controllers (e.g., DNS, LDAP, SMB, RDP).
- `192.168.1.0/24`: Target subnet (adjust as needed).

---

### Step 3: **Analyze the Output**

- Look for systems with services indicating a domain controller:
    - **DNS** (`port 53`) resolving domain names.
    - **LDAP** (`port 389` or `636`) for directory services.
    - **Kerberos** (`port 88`).
    - **SMB** (`port 445`).
- Identify the hostname and domain in the `DNS` or `LDAP` output, which should include the FQDN.

Example Output Snippet:

```
Host: 192.168.1.10
PORT     STATE SERVICE VERSION
53/tcp   open  domain  Microsoft DNS
88/tcp   open  kerberos-sec Microsoft Windows Kerberos
389/tcp  open  ldap    Microsoft Windows Active Directory LDAP
445/tcp  open  microsoft-ds Microsoft Windows Server 2019
| smb-os-discovery:
|   OS: Windows Server 2019 Standard
|   Computer name: DC01
|   Domain: example.local
|   FQDN: dc01.example.local

```

From this, the **FQDN of the domain controller** is `dc01.example.local`.

---

### Step 4: **Validate the Domain Controller**

If the domain controller isn't immediately clear, narrow the search with additional Nmap scripts:

1. **Check SMB Enumeration**:
    
    ```bash
    nmap --script smb-enum-domains -p 445 192.168.1.10
    
    ```
    
    This script enumerates domains and domain controllers via SMB.
    
2. **Check LDAP Enumeration**:
    
    ```bash
    nmap --script ldap-search -p 389 192.168.1.10
    
    ```
    
    This script queries LDAP to confirm the domain and server role.
    
3. **Reverse Lookup**:
Use the `-dns-brute` script to enumerate DNS records:
    
    ```bash
    nmap --script dns-brute 192.168.1.0/24
    
    ```
    

---

### Step 5: **Final Confirmation**

After identifying the FQDN (e.g., `dc01.example.local`), confirm by querying the server with tools like `nslookup` or `dig`:

```bash
nslookup dc01.example.local

```

---

### Summary

1. Perform an Nmap scan targeting relevant ports and scripts for domain discovery.
2. Analyze the results to find the FQDN in the DNS, LDAP, or SMB information.
3. Confirm the domain controller’s role using additional enumeration scripts or tools.
