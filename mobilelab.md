### **Autopsy Lab/Tutorial for Mobile Device Forensics**

**Objective:**  
The objective of this tutorial is to guide you through the process of using **Autopsy** (a powerful open-source digital forensics platform) to analyze mobile device data. This lab will focus on data extraction from mobile device backups, such as those from **iTunes** or **Android**, and guide you through analyzing the data for relevant evidence.

---

## Video Demonstrations

I understand there is a lot of content here, view what is interesting to you, there is a lot that goes into IoS/Android forensics.

SANS Digital Forensics and Incident Response Lecture:
- [iOS of Sauron: How iOS Tracks Everything You Do- SANS DFIR Summit 2016](https://www.youtube.com/watch?v=D6cSiHpvboI)

Mobile Device Acquisiton and Forensics Examiner Demonstration (quick):
- [DFS101: 11.2 Mobile Device Acquisition](https://www.youtube.com/watch?v=K_RE3wEZwPc)
- [Watch as forensic technicians break into an iPhone (quick but interesting)](https://www.youtube.com/watch?v=WYxV9PtkwbU)

Law Enforcement and Cellebrite:
- [How Law Enforcement Breaks into iPhones](https://www.youtube.com/watch?v=F7xawqxI260)
- [Mobile Forensics For Litigation using Cellebrite](https://www.youtube.com/watch?v=MQGSuHkfsdc)

TryHackMe:
- [Taking over Absolutely Everything On an iPhone ! iOS Digital Forensics Challenge (TryHackMe-Easy)](https://www.youtube.com/watch?v=12pmtwCDOEw)

Snapchat (Common App Concerns):
- [Snapchat Analysis to Discover Digital Forensic Artifacts on Android Phone](https://www.youtube.com/watch?v=BCMdJDggPos)

Android and IoS Data Storage and File System Structure:
- [The iOS File System Structure](https://www.youtube.com/watch?v=47IRNLQYqB4)
- [ANDROID FORENSIC ACQUISITION](https://www.youtube.com/watch?v=MA0Pud6hAyI)

Android Acquisition using ADB, root, ncat, and DD:
- [Windows Android Acquisition using mentioned tools](https://www.youtube.com/watch?v=KKkvkCgMeMA)

Mobile Device analysis with iLEAPP:
- [Fast iPhone forensic analysis with iLEAPP](https://www.youtube.com/watch?v=Cp9QMauTRaM)
- [Fast Android forensic triage with ALEAPP](https://www.youtube.com/watch?v=_cm1n0stVrA)

Mobile Device Forensics with OSForensics:
- [How to Obtain Data from an Android Device with OSForensics](https://www.youtube.com/watch?v=p4mXFJgtszY)
- [Expanding on Deleted File Search with OSForensics](https://www.youtube.com/watch?v=BWLxRHlKYsM)

---

### **Lab Setup and Requirements**

#### **Software Required:**

1. **Autopsy**: Install the latest version of Autopsy from Autopsy's website.
2. **Mobile Device Data**: For the tutorial, we will use a **mobile backup** (e.g., iTunes or Android). You can either create a backup of your own device or use sample forensic images available online.
    - For **Android**: Use tools like **ADB** to extract a backup or use **Oxygen Forensics** to create a mobile device backup.
    - For **iOS**: Extract an iTunes backup from an iOS device or use a sample backup.
3. **FTK Imager** (optional): To generate disk images, in case you want to start from raw device images.

---

### **Step 1: Install and Set Up Autopsy**

1. **Download Autopsy**:
    
    - Go to Autopsy's Download Page and follow the installation instructions for your operating system.
2. **Launch Autopsy**:
    
    - Open the Autopsy application. You will be greeted with the main interface. Select "Create New Case" to begin a new investigation.
3. **Create a New Case**:
    
    - **Case Name**: "Mobile Device Forensics Lab"
    - **Case Number**: A unique identifier for your case (e.g., "2023-001")
    - **Description**: Brief description of the case (e.g., "Analysis of iTunes backup for mobile device forensic investigation")
    - **Path**: Choose the directory where the case files will be saved.
4. **Add a Data Source**:
    
    - After creating the case, click on the **Add Data Source** button to load your mobile device backup.
    - Select the appropriate data source type:
        - For an **iTunes Backup**: Choose **"Logical File"**.
        - For an **Android backup**: Choose **"Disk Image"** or **"File System"**, depending on how the data was extracted.
5. **Select the Data Source File**:
    
    - Select the **mobile backup** or **disk image** you wish to analyze (e.g., `backup.ipa`, `backup.img`, etc.).
    - Click **Next**.

---

### **Step 2: Initial Processing of Mobile Backup**

1. **Select Ingestion Modules**:
    
    - Autopsy will prompt you to select **Ingestion Modules**. Ingestion modules are plugins used to extract and analyze different types of data from the image.
    - **Recommended Ingestion Modules** for mobile forensics:
        - **File Type Identification**: Identifies the file types in the backup.
        - **Hash Lookup**: Helps to identify known files (e.g., using hash databases like NSRL).
        - **Data Carving**: Recovers deleted files or fragments of files that might be present in the unallocated space.
        - **SMS**: This module helps extract SMS messages from mobile backups.
        - **Contacts**: Extracts contact information from the backup.
        - **Media Files**: Extracts photos, videos, and other media from the mobile device.
2. **Start the Ingestion Process**:
    
    - Click **Finish** to begin the analysis. Autopsy will start processing the mobile backup, extracting relevant data such as SMS, call logs, contacts, media files, and other app data.

---

### **Step 3: Analyze Mobile Data**

Once the processing is complete, the following types of data will be available for review in the **Autopsy** interface:

#### **3.1 File System View**

- In the **File Analysis** tab, you can explore the file system extracted from the backup. This includes directories for **System Files**, **App Data**, and **User Data**.
- You will also see directories for individual apps (e.g., WhatsApp, iMessage, etc.), and you can explore the files and metadata within them.

#### **3.2 SMS Messages**

- If your backup includes SMS or MMS data, Autopsy will list them under the **"Messages"** section.
- Browse through the conversation threads, view timestamps, and analyze any multimedia messages (e.g., images or voice memos) attached to the messages.

#### **3.3 Contacts**

- Contacts from the mobile device are listed under the **"Contacts"** section.
- Autopsy will extract names, phone numbers, email addresses, and other relevant details.

#### **3.4 Photos and Videos**

- Under the **"Media"** tab, Autopsy will list photos, videos, and audio files found in the backup.
- Autopsy identifies images and videos by file type (e.g., JPEG, PNG, MP4) and provides metadata about each file, such as creation date and file size.

#### **3.5 Call Logs**

- If the backup contains call logs, you can find them under the **"Call Logs"** section.
- The call logs will include details like call duration, timestamp, and contact information.

#### **3.6 App Data**

- For iOS and Android apps, Autopsy can extract data from apps such as WhatsApp, Facebook Messenger, or Instagram (depending on the backup type and tools used to extract the data).
- For example, **WhatsApp messages** or **location data** can be extracted from their respective folders.

#### **3.7 Geolocation Data**

- Some mobile apps, like **Google Maps**, store geolocation data. Autopsy can display GPS coordinates and other location-related data.
- You can visualize the locations on a map or analyze the timestamps associated with the locations.

---

### **Step 4: Data Carving (Recover Deleted Files)**

1. **Start Data Carving**:
    
    - If you suspect that deleted data may be present in the unallocated space, you can run **Data Carving** during the ingestion phase or manually initiate it afterward.
    - Autopsy will search for file fragments (e.g., deleted photos or documents) and try to reconstruct them.
2. **Analyze Recovered Data**:
    
    - The carved data will be listed in the **"Carved Data"** tab, where you can view and inspect the files recovered from unallocated space.
    - This can include deleted images, documents, or app-related data that may be crucial for the investigation.

---

### **Step 5: Reporting**

After completing the analysis, you can generate a report of your findings:

1. **Generate a Forensic Report**:
    
    - Click on **"Generate Report"** to produce a detailed forensic report. You can select the format (e.g., HTML, PDF) and specify which data to include.
    - Autopsy will generate the report, summarizing the findings, including extracted data like SMS, contacts, media files, and any carved or deleted files.
2. **Customize the Report**:
    
    - You can add notes or annotations to specific files or artifacts within the report.
    - The report will include file hash information, timestamps, and other metadata to help verify the integrity of the evidence.

---

### **Step 6: Conclusion**

You have successfully used **Autopsy** to conduct a mobile device forensic investigation. This tutorial covered the following key steps:

- Setting up Autopsy for mobile device analysis.
- Acquiring and processing mobile backup data.
- Analyzing key mobile data like SMS, contacts, media files, and app data.
- Recovering deleted files using data carving.
- Generating a comprehensive forensic report.

Remember to always preserve the integrity of the evidence and document each step to ensure that your findings can be used in legal proceedings. Mobile forensics is a powerful tool for uncovering digital evidence, and Autopsy makes it easier to navigate complex mobile data.
