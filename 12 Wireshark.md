# 12. Wireshark
### Step-by-Step Guide to Analyze the File for the Source IP Address of a DDoS Attack  

Here’s a structured approach to identifying the source IP address of a DDoS attack, aligned with CEH practical exam standards.  

---

### **Task**: Investigate the DDoS Attack File for the Attacker's IP Address  
You’ve been provided with a file suspected to contain information about a DDoS attack. The objective is to analyze this file and identify the IP address of the attacking machine.  

---

### **Step-by-Step Solution**  

#### **Step 1: Open the File in a Safe Analysis Environment**  
- Use a secure, isolated environment such as REMnux or a Windows VM with analysis tools installed.  
- Ensure the file is opened in a sandboxed environment to mitigate any potential risks from malicious content.  

#### **Step 2: Examine the File Type**  
- Determine the file type to choose the appropriate tool for analysis.  
- **Text or Log Files**: Open directly using a text editor or command-line tools.  
- **Packet Capture (PCAP) Files**: Use tools like **Wireshark** or **Network Miner**, which are commonly used in CEH labs.  

#### **Step 3: Analyze the File with Wireshark (If It’s a PCAP File)**  
1. Open Wireshark and load the file:  
   - Navigate to `File > Open` and select the provided PCAP file.  
2. Apply specific filters to identify DDoS indicators, such as:  
   - **SYN Flood**: `tcp.flags.syn == 1 and tcp.flags.ack == 0`  
   - **ICMP Flood**: `icmp`  
   - **HTTP Flood**: `http.request`  
3. Identify high-volume IP addresses:  
   - Go to `Statistics > Conversations` to find the IP address with the most connections to the target machine.  
   - This IP address is likely the source of the DDoS attack.  

#### **Step 4: Verify the Attack Patterns**  
- Look for abnormal traffic patterns, such as:  
  - Repeated requests from the same IP within a short time frame.  
  - A large volume of SYN packets without corresponding ACKs.  
- Confirm the attacker’s IP address identified in the previous step by analyzing these patterns.  

#### **Step 5: Document the Attacker’s IP Address**  
- Record the IP address identified as the source of the DDoS attack.  
- Note the type of attack traffic (e.g., SYN flood, ICMP flood) associated with this IP for reporting purposes.  

---

### **Summary**  
1. Open the file in Wireshark (if in PCAP format).  
2. Apply filters, such as:  
   - `tcp.flags.syn == 1 and tcp.flags.ack == 0` for SYN floods.  
   - `icmp` for ICMP floods.  
3. Use `Statistics > Conversations` to identify the IP with the most connections or unusual traffic patterns.  
4. Document the attacker’s IP address and the associated attack type for further reporting.  

By following these steps, you can efficiently analyze and identify the source of a DDoS attack while adhering to best practices.
