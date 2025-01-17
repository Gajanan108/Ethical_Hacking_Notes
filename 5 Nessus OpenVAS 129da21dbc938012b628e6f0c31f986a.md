# 5.  Nessus/OpenVAS

To perform a vulnerability scan and assess the vulnerability score related to the "End of Life" (EOL) of a web development language platform, follow these detailed steps:

---

### Assumed Setup

- **Target IP**: `192.168.1.10` (replace with your actual target).
- **Vulnerability Scanning Tool**: **Nessus** or **OpenVAS**.
- **Objective**: Identify outdated software (e.g., PHP, Python, or Ruby) and assess the vulnerability score.

---

### Step-by-Step Guide

### **Step 1: Install and Set Up the Scanning Tool**

1. **Install Nessus**:
    - Download from [Tenable](https://www.tenable.com/products/nessus/nessus-professional).
    - Install and configure it on your machine.
    - Update the vulnerability database to ensure up-to-date scanning.
2. **Alternatively, Install OpenVAS**:
    - Use a Linux system (e.g., Kali Linux) to install OpenVAS:
        
        ```bash
        sudo apt update
        sudo apt install openvas
        
        ```
        
    - Run the setup command:
        
        ```bash
        sudo gvm-setup
        sudo gvm-check-setup
        
        ```
        

---

### **Step 2: Configure the Scan**

1. **Define the Target**:
    - Add the IP address `192.168.1.10` as the scan target in Nessus/OpenVAS.
2. **Enable Plugins**:
    - Ensure plugins for detecting "End of Life" vulnerabilities are enabled.
    - Nessus Plugins: Search for keywords like **"End of Life"** or **"EOL"** in the plugin library.
    - OpenVAS: Use the default or CVE-specific scan profile.
3. **Select Scanning Profile**:
    - For Nessus, select **Advanced Scan**.
    - For OpenVAS, use **Full and Fast Scan**.

---

### **Step 3: Run the Vulnerability Scan**

1. Start the scan targeting `192.168.1.10`.
2. Allow the scan to complete (this may take several minutes depending on the target's complexity).

---

### **Step 4: Analyze Results**

1. **Check for "End of Life" Alerts**:
    - Look for vulnerabilities labeled as **"End of Life"**, **EOL**, or **Outdated Software**.
    - Example: PHP 5.x detected with EOL status.
2. **Evaluate the CVSS Score**:
    - Locate the CVSS (Common Vulnerability Scoring System) score for each vulnerability.
    - Example Output:
        
        ```
        Plugin ID: 10000
        Name: PHP 5.x Reached End of Life
        Description: PHP 5.x is no longer supported. Consider upgrading to a supported version.
        CVSS Base Score: 7.5 (High)
        Solution: Upgrade to PHP 7.4 or later.
        
        ```
        

---

### **Step 5: Remediation Recommendations**

- If the EOL vulnerability is critical (e.g., CVSS score ≥7.0):
    - **Upgrade the Software**: Move to a supported version of the platform (e.g., PHP 7.4, Python 3.x).
    - **Apply Security Patches**: If upgrading is not immediately possible, ensure all security patches are applied.
    - **Monitor the System**: Use additional tools to check for exploitation.

---

### Sample Summary Report

| **Target IP** | **Vulnerability** | **CVSS Score** | **Description** | **Recommendation** |
| --- | --- | --- | --- | --- |
| 192.168.1.10 | PHP 5.x End of Life | 7.5 (High) | PHP 5.x is no longer supported by the vendor | Upgrade to PHP 7.4 or higher |
| 192.168.1.10 | Ruby 2.6 End of Life | 6.5 (Medium) | Ruby 2.6 has reached EOL | Upgrade to Ruby 2.7 or higher |

---

### Key Notes

- **EOL vulnerabilities** are high-risk because they lack vendor support and security patches.
- **Tools like Nessus or OpenVAS** automate detection and provide detailed remediation steps.
- Always verify detected vulnerabilities against official vendor documentation.