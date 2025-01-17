# 7. Image investigation

For a Certified Ethical Hacker (CEH) practical environment or iLab scenario, let's revise the solution using tools commonly suggested in CEH training. Here’s how you would analyze an image file suspected of hiding sensitive data using CEH-recommended tools.

---
Task: Extract Sensitive Data from an Image File Using CEH Tools
In this scenario, a security investigator suspects that an image file (suspicious_image.png) contains hidden sensitive information, potentially an 8-digit alphanumeric code. We’ll analyze this image file using CEH tools and retrieve any hidden sensitive information.

---
1. Assumed Information
File Name: suspicious_image.png
Sensitive Data Format: An 8-digit alphanumeric code (e.g., AB12CD34).
Tools Required: QuickStego, StegSpy, and Hex Editors (commonly used in CEH labs).
Objective: Extract hidden data embedded within the image file, which may contain a sensitive code.

---
Step-by-Step Guide:
Step 1: Inspect the Image File with StegSpy
StegSpy is a tool used to detect if steganography was used in an image.
Run StegSpy on suspicious_image.png to check if the file contains hidden data:
1. Open StegSpy.

2. Load the image file suspicious_image.png.

3. Analyze the image to determine if any steganographic data is detected.

If StegSpy identifies hidden data, it confirms that further analysis is warranted.

Step 2: Extract Data Using QuickStego
QuickStego is a tool that can retrieve hidden text from images if certain steganographic methods were used.
To attempt extraction with QuickStego:
1. Open QuickStego.

2. Load suspicious_image.png.

3. Select "Reveal" or "Extract" to retrieve hidden data.

If hidden text is extracted, look for any 8-character alphanumeric strings resembling sensitive data.

Step 3: Hex Editor Analysis with HxD
If StegSpy or QuickStego doesn’t yield results, analyze the file’s binary data using HxD (a hex editor commonly used in CEH labs).
Open the image file with HxD and search for readable ASCII strings that may be embedded within the binary data:
1. Load suspicious_image.png into HxD.

2. Use Search -> Find and search for common patterns, such as an 8-character alphanumeric code.

3. Look for ASCII strings that match the format (e.g., AB12CD34).

A hidden code may be embedded directly in the image’s binary data as ASCII text.

Step 4: Use OpenStego for Extraction
If the prior steps did not reveal any hidden data, try OpenStego (another CEH-recommended steganography tool).
To use OpenStego for extraction:
1. Open OpenStego and select "Extract Data."

2. Load suspicious_image.png as the file to analyze.

3. Attempt to extract any embedded information.

If OpenStego finds hidden data, it will reveal the content or provide an extracted file.

Step 5: Review Extracted Data
After retrieving any hidden text or data from the image file using the above tools, check the content for any 8-character alphanumeric strings that resemble the sensitive code.
If extracted data is in text format, use cat in the command line or any text editor to review it.

---
Summary:
1. StegSpy was used to detect steganographic content.

2. QuickStego helped extract hidden text from the image file.

3. HxD provided a way to view ASCII strings directly within the binary data.

4. OpenStego offered another method to extract hidden data.

Once the 8-digit alphanumeric code is identified, record it as the sensitive data, fulfilling the investigation’s requirements. Let me know if you'd like more guidance on any of these tools!