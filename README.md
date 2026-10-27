### Android Forensics Investigation: Google Pixel 3

**International Cybersecurity and Digital Forensics Academy (ICDFA)**
School of Basic Vocational Training (SVT)

![Course](https://img.shields.io/badge/Course-SBT--DF205-blue)
![Case Study](https://img.shields.io/badge/Case%20Study-01%20Android%20Forensics-red)
![Tools](https://img.shields.io/badge/Tools-SQLite%20%7C%20ExifTool%20%7C%20Kali%20Linux-informational)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)

---

### Author Information

| Field | Details |
| :--- | :--- |
| **Student Name** | Ibrahim Diseh Garba |
| **Student ID** | 2025/FWSD/11521 |
| **Programme** | Fellowship in Web Application Security & Digital Forensics |
| **Course** | SBT-DF205 - Mobile and IoT Forensics Case Study |
| **Instructor** | Aminu Idris, AMCPN |
| **Date** | 24th October, 2026 |
| **Case Reference** | SBT-DF205-C1 |

---

### Executive Summary

This repository contains the forensic artefacts, SQL scripts, and final report for a logical extraction taken from a **Google Pixel 3 running Android 10**. The examination was carried out to determine whether a Harbour Operations Ltd employee engaged in unauthorised communication.

> **Primary Finding:** The device is associated with the user **"Josh Hickman"**. Communication and activity artefacts were successfully recovered from AOSP SMS, TextNow, Google Maps, and Google Photos. Records in the Google Messages database (`bugle_db`) reference the AOSP Telephony Provider, showing the app was in active use. 
> 
> **Confidence Level:** High for device identity and artefact recovery. Moderate for timeline correlation due to mixed timezone offsets. Technical evidence alone cannot attribute the communications to a specific person without HR context.

---

## 🔍 Key Findings & Artefacts

### 1. Device Identity & Profiles
*   **Build Properties:** Android 10 (`ro.build.version.release = 10`), Build ID `QQ1A.200105.003`.
*   **User Profiles:** User 0 (Owner) and User 11 (Work Profile) identified via `userlist.xml`.
*   **Account Associations:** Primary account `thisisdifir@gmail.com`, corroborated by WhatsApp and Twitter services.
*   **Security Posture:** `install_non_market_apps = 1` (Sideloading enabled). Wi-Fi configuration was empty.

### 2. Communications
*   **AOSP SMS (`mmssms.db`):** Recovered latest message sent to `919-579-0479` (Josh Hickman) containing the text: *"Wow, the messages sync over between accounts."*
*   **MMS Reconstruction:** Recovered an MMS notification and message part (`text/plain`) containing *"Here's Signal."*
*   **Calls (`calllog.db`):** Identified a 91-second incoming call from `9195790479`.
*   **Google Messages (`bugle_db`):** Proved to be the default SMS app via `sms_message_uri` links (e.g., `content://sms/24`).
*   **TextNow (`textnow_data.db`):** Recovered a conversation with `+1(984) 203-2223` starting with *"Hi there!"*
*   **WhatsApp (`msgstore.db`):** Local database contained only `status@broadcast` rows (no 1-to-1 chat history).

### 3. Location & Media
*   **Google Maps (`gmm_myplaces.db`):** Recovered E6 location data (`35734602, -78636654`), converting to `35.734602, -78.636654` (Raleigh, NC).
*   **Google Photos (`gphotos-1.db`):** Identified media file `IMG_20190917_082637.jpg`.
*   **EXIF GPS:** Extracted precise GPS coordinates (`35° 44' 8.33" N, 78° 38' 10.92" W`) from the photo, corroborating the Maps location.

---

## 🛠️ Methodology & Tools

### Evidence Integrity
The original archive (`Pixel 3.zip`, 5.25 GB) was hashed and verified, remaining untouched. All analysis was performed on a working copy.
*   **Original SHA-256:** `ca6918ef8b20486b6a5ded15609ac51318f377829480f93be3ba15364a8aa00a`

### Tools Used
| Tool | Purpose |
| :--- | :--- |
| **SQLite3** | Scripted SQL queries; reproducible outputs. |
| **grep** | System configuration extraction. |
| **ExifTool** | Photo metadata and GPS extraction. |
| **sha256sum** | Integrity verification. |
| **Kali Linux** | Analysis environment. |

### Android Epoch Timestamp Conversion
Most Android databases record time as milliseconds since the Unix epoch. Values were converted to UTC using:

---

### Challenges & Limitations
**Attribution:** The device has multiple profiles and may have been used by more than one person. Device activity does not equal human identity.

**Missing Data:** No one-to-one WhatsApp history, Wi-Fi configurations, or Calendar events were recovered.

**Timezone Offsets:** Sources used mixed timezone offsets, requiring careful normalization to UTC.

**Server-Side Logs:** Unavailable (e.g., Craigslist, Gmail), limiting external corroboration.

---

### Copyright & Usage

**© 2026 Ibrahim Diseh Garba. All Rights Reserved.**

This repository contains academic coursework and a forensic report submitted as part of the Fellowship in Web Application Security & Digital Forensics at the **International Cybersecurity and Digital Forensics Academy (ICDFA)**.
