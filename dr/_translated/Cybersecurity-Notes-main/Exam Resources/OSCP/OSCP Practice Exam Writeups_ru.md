Here is a summary and analysis of the practice exam writeup.

### Key Takeaways

**Strategic Shift**
The most significant change from Exam 1 to Exam 2 was in report structure. Instead of a single "Information Gathering" section, the report now includes **separate sections for each machine**, with `nmap` results integrated directly into their writeups.

**Efficiency & Time Management**
The author identified a specific time constraint: if you are short on points by end of day 1, sleep less and aim for 00:00–06:00. This is because the afternoon slump occurs due to fatigue, suggesting morning starts work better for alertness.

**Tool Usage**
The author adopted several new tools:
*   **wpscan:** For brute-force password cracking on services like `/wp-admin`.
*   **LinPEAS:** For quick file misconfiguration scanning.
*   **scans/[IP]/results:** A custom Bash script to view all Autorecon results at once.

**Report Writing**
The author reduced "fluff" in the report. Instead of documenting every step, they focused on **methodology lessons** and **proof**. They also structured the appendices to include meterpreter usage and file content evidence.

### Analysis of Exam 2 Success

The author successfully rooted Mercy and completed the exam. Key factors likely behind this were:
1.  **Reuse:** They realized password reuse was a common foothold on CTF machines.
2.  **Information Review:** They used `autorecon` to cross-reference service names with Hacktricks, which Autorecon prioritizes over manual enumeration.
3.  **SMB Scan Trick:** Using `nmap --script=banner` on SMB shares is a proven technique for bypassing `smbclient` detection.

### Suggested Next Steps

If you are preparing for the OSCP, the author’s strategy of "removing information" is highly effective for revision. To replicate this:
1.  **Standardize Scans:** Use the same `nmap` scripts across all machines to make analysis faster.
2.  **Template Usage:** Using existing report templates (as mentioned in the comments) reduces the time spent writing from ~9 hours to ~3 hours per machine.
