# Vulnerability Report: Publicly Exposed Sensitive Directories & Backups

## Executive Summary
During an independent security assessment, a critical information disclosure vulnerability was identified on a Vodafone endpoint. Due to a server misconfiguration, sensitive directories containing database dumps, command histories, and backend source files were publicly accessible without authentication. 

* **Target URL:** `https://vfo11.vodafone.om`
* **Vulnerability Type:** Information Exposure Through Sent Data (CWE-200) / Server Misconfiguration
* **Platform:** HackerOne
* **Status:** Resolved / Confirmed & Patched by Vendor

---

## Technical Analysis & Steps to Reproduce

### 1. Discovery & Reconnaissance
An analysis of the target endpoint revealed an exposed backup descriptor mapping. Executing a standard terminal request targeted the following directory listing configuration:

```bash
curl [https://vfo11.vodafone.om/xml/backup_descriptor](https://vfo11.vodafone.om/xml/backup_descriptor)
