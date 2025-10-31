# Splunk Basics – Zeek Connection Log Analysis  
* Day 22 of #30DaysOfSOC Challenge
---
##  📘 Overview

This project demonstrates how to ingest and analyze Zeek connection logs using **Splunk**.  
It focuses on identifying top clients, common services, and long-duration connections essential for understanding network behavior during SOC investigations.  

---

## 🎯 Objective  

In this lab, you will:  
- Learn how to upload and search Zeek connection logs in Splunk.  
- Find top clients, top servers, and most common services.  
- Identify large traffic and long connections.  

---

## 🖥️ Lab Setup  

- ✅ **Splunk**: Already installed and accessible.  
- ✅ **Data Source**: JSON-formatted Zeek-style connection logs.  
- 🌐 **Log File**: Download and upload to Splunk using the steps below.  

📥 **[Download zeek_conn_logs.json](./zeek_conn_logs.json)**  

---

## ⚙️ Steps to Upload Connection Log into Splunk  

1. Go to **Splunk Web → Settings > Add Data**.  
2. Choose **Upload** and select `zeek_conn_logs.json`.  
3. Set **Source type**: `_json` (Splunk default) or create a custom one `zeek:conn`.  
4. Choose **Index**: use `main` or create a new one `conn_lab`.  
5. Complete the upload and verify the data is searchable.  

---

## 🔍 Lab Tasks  

Use the following SPL queries to complete each task:

✅ Task 1: Find the Top 10 Client IPs (`id.orig_h`)

spl

index=conn_lab sourcetype="_json"
| stats count by id.orig_h
| sort -count
| head 10

---

✅ Task 2: List Most Common Services

spl

index=conn_lab sourcetype="_json"
| stats count by service
| sort -count

---

✅ Task 3: Find Connections with Duration > 1 Second

spl

index=conn_lab sourcetype="_json" duration>1
| table ts id.orig_h id.resp_h service duration
| sort -duration

---

✅ Task 4: Identify the Most Accessed Internal Servers

spl

index=conn_lab sourcetype="_json"
| stats count by "id.resp_h"
| sort -count
| head 10

---

🖼️ Project Screenshots

All screenshots from this analysis can be viewed here:

📸 **[View Screenshots Folder](./screenshots/)**


---

🧩 Project Files

| File                                           | Description                                                 |
| ---------------------------------------------- | ----------------------------------------------------------- |
| [`zeek_conn_logs.json`](./zeek_conn_logs.json) | Zeek connection log file used for analysis                  |
| [`screenshots/`](./screenshots/)               | Contains all screenshots of Splunk search results and setup |

---

Author: Godliveth Madu 
SOC Trainee 
LinkedIn: www.linkedin.com/in/godliveth-madu-1771b6251

