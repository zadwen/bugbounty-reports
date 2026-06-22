# Bug Bounty Reports
Collection of my bug bounty reports and security research evidence.

## Vodafone IoT - ID Enumeration
**Summary:** The API allowed unauthenticated ID enumeration, exposing user IDs without proper access control.  
**Steps to Reproduce:** Fuzzing the `id` parameter returned valid responses for existing IDs.  
**Evidence:** ![Vodafone IoT](vodafone_idor.png)  
**Impact:** Information disclosure, classified as Medium severity (CVSS 5.3).

## Vodafone - Exposed Sensitive Files
**Summary:** Misconfigured server exposed sensitive files publicly.  
**Steps to Reproduce:** Accessing `/xml/backup_descriptor` revealed a directory listing.  
**Evidence:** ![Vodafone Exposed Files](vodafone_exposed.png)  
**Impact:** Exposure of `.htaccess`, `private-key.pem`, and `backup.zip` could lead to deeper compromise.  
Severity was downgraded to Low by the program, but technically this can be High risk.
