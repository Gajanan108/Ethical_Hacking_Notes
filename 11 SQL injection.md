# 11. SQL injection
### Performing an SQL Injection Attack on a Target Web Application  

Here’s a structured approach, similar to CEH practical labs, to perform an SQL injection attack on a vulnerable web application like **Damn Vulnerable Web Application (DVWA)**. This walkthrough demonstrates how to extract the password for a specific user, "Suresh."  

---

### **Task**: Extract the Password for User "Suresh" Using SQL Injection  

**Given**:  
- **Target Application**: DVWA or a similar vulnerable web application.  
- **Initial User Credentials**: `Joy / Joy@1234` (for logging in).  
- **Goal**: Extract the password for the user "Suresh" using SQL injection.  

---

### **Step-by-Step Solution**  

#### **Step 1: Log in to the Application with Valid Credentials**  
1. Log in to the web application using the provided credentials (`Joy / Joy@1234`).  
2. Navigate to a page where SQL injection might be possible, such as a **search**, **login**, or **user profile** form.  

#### **Step 2: Identify SQL Injection Vulnerability**  
1. Test input fields by entering simple SQL payloads to check for vulnerabilities. Example:  
   ```
   ' OR '1'='1
   ```  
2. Observe the behavior of the application:  
   - If unexpected data is displayed or errors occur, the field is likely vulnerable to SQL injection.  

#### **Step 3: Craft SQL Injection Payload to Extract User Data**  
1. Once a vulnerability is identified, create a **UNION-based SQL injection payload** to retrieve the password for "Suresh."  
2. Example payload:  
   ```sql
   ' UNION SELECT null, username, password FROM users WHERE username = 'Suresh' --
   ```  
3. **Payload Breakdown**:  
   - **`' UNION SELECT`**: Combines results from the vulnerable query with a new query.  
   - **`null, username, password`**: Ensures the column structure matches the original query.  
   - **`FROM users WHERE username = 'Suresh'`**: Filters results to return data only for "Suresh."  
   - **`--`**: Comments out the rest of the original query to avoid conflicts.  

#### **Step 4: Execute the Payload**  
1. Enter the crafted payload into the vulnerable input field and submit it.  
2. If successful, the application should display the data for "Suresh," including their password.  

#### **Step 5: Document the Extracted Password**  
1. Record the password obtained for "Suresh" and note the process used to retrieve it.  
2. Ensure all findings are documented for reporting purposes.  

---

### **Summary**  
1. Log in using the credentials `Joy / Joy@1234`.  
2. Test input fields for vulnerabilities using payloads like:  
   ```
   ' OR '1'='1
   ```  
3. Use a **UNION-based SQL injection** payload to extract data for the user "Suresh." Example:  
   ```sql
   ' UNION SELECT null, username, password FROM users WHERE username = 'Suresh' --
   ```  
4. Document the extracted password and any other relevant findings.  

This structured approach ensures a thorough and methodical process for identifying and exploiting SQL injection vulnerabilities in a controlled ethical hacking environment.
