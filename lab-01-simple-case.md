# Lab 01: File Path Traversal – Simple Case

**Platform:** PortSwigger Web Security Academy  
**Difficulty:** Apprentice  
**Date:** October 19, 2026  
**Tool:** Burp Suite Community Edition  
**Result:** Successfully retrieved `/etc/passwd`

## Objective

Identify and exploit a path traversal vulnerability in a product image endpoint to retrieve the contents of `/etc/passwd`.

## Steps Performed

1. Opened the PortSwigger Web Security Academy lab.
2. Launched the lab website in Burp Suite's built-in browser.
3. Navigated to Proxy → HTTP History.
4. Located an HTTP GET request containing the `filename` parameter.
5. Right-clicked the request and selected "Send to Repeater."
6. Opened Burp Repeater to modify the HTTP request.
7. Changed the filename parameter to `../../../etc/passwd`.
8. Clicked "Send" to submit the modified request.
9. Examined the server response and identified an entry beginning with `root:x:0:0`.

## Vulnerability Explanation

The application did not properly restrict user-controlled file paths.

The `../` sequence moves up one directory level. By using `../../../`, I was able to reference a file outside the intended image directory.

## Results

The server returned the contents of `/etc/passwd`, demonstrating that the application was vulnerable to path traversal.

## Security Impact

This vulnerability may allow attackers to read sensitive files, application configurations, or source code that the server has permission to access.

## Recommended Remediation

- Use an allowlist of permitted filenames.
- Restrict file access to approved directories.
- Validate resolved file paths.
- Apply least-privilege file permissions.

## Skills Learned

- Burp Suite Proxy and HTTP History
- Burp Suite Repeater
- HTTP request and response analysis
- Path traversal vulnerability testing
- Security findings documentation

## Reflection

This was my first hands-on PortSwigger lab. I learned how to identify an image request, modify its parameters using Burp Suite, and examine the server's response to determine whether a vulnerability exists.

## Disclaimer

All testing was performed in an authorized educational environment provided by PortSwigger Web Security Academy.
