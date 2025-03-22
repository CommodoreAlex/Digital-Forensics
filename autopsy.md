### Tutorial: Using Autopsy for Digital Forensics

Autopsy is a powerful open-source digital forensics tool that helps forensic investigators analyze hard drives, mobile devices, memory, and other types of digital evidence. It provides an easy-to-use graphical interface and is used in both criminal and corporate investigations to help find, recover, and analyze digital evidence.

This tutorial will guide you through the basic steps of using Autopsy for digital forensics, focusing on creating a case, adding data sources, and performing common forensic tasks like file analysis, keyword searching, and reporting.

---
## Video Demonstrations:
- [Computer Forensics: Using Autopsy To Investigate a Local Hard Drive](https://www.youtube.com/watch?v=uRK7xWsZ2TU)
- [Disk Analysis with Autopsy | HackerSploit Blue Team Training](https://www.youtube.com/watch?v=o6boK9dG-Lc)

---

### 1. Prerequisites

Before starting, ensure you have the following:
- **Linux or Windows system**: Autopsy works on both Linux and Windows.
- **Java Runtime Environment (JRE)**: Autopsy requires Java to run.
- **A sample disk image**: To analyze, you’ll need a disk image (e.g., `.dd`, `.e01`, `.img` files) from a device like a hard drive, USB drive, or other storage media.
### 2. Installing Autopsy

#### For Windows:
1. Download the installer from the Autopsy website.
2. Run the installer and follow the on-screen instructions.
3. Once installed, launch Autopsy from the Start menu.

#### For Linux (Debian/Ubuntu-based):

1. Open a terminal and install the necessary dependencies:
```bash
sudo apt-get update
sudo apt-get install sleuthkit autopsy
```

2. After installation, you can run Autopsy by typing:
```bash
autopsy
```

### 3. Creating a New Case

Once Autopsy is installed and launched, you’ll begin by creating a new case.

#### Step 1: Start a New Case

1. Open Autopsy and click **"Create New Case"**.
2. Enter a **Case Name** and **Case Number** (e.g., "Sample Investigation" and "1234").
3. Set the **Base Directory** where your case files and data will be stored.
4. Click **Next**.
#### Step 2: Set Up the Investigator's Information

- Enter your name and other details as the investigator.
- Click **Next** to proceed.

#### Step 3: Choose a Data Source Type

- Select the type of evidence you're analyzing. You can choose from various options like a **Disk Image**, **Local Disk**, or **Network Drive**.
- Click **Next** once you've chosen the source.

### 4. Adding Data Sources

Autopsy allows you to add various types of data sources, such as disk images, local disks, or directories.

#### Step 1: Add Disk Image

- Choose **Disk Image or VM File** if you’re analyzing a disk image.
- Click **Add** and navigate to the image file you want to analyze (e.g., `.dd`, `.e01`).

#### Step 2: Configure Image File Settings

- Choose the type of image file you are adding (e.g., raw, AFF, E01).
- If you’re adding multiple images, you can specify additional files here.
- Click **Finish** once you’ve added the necessary files.

Autopsy will now process the image and begin indexing the data.

### 5. Analyzing the Data

#### File Analysis

After adding the data source, you can start analyzing the files:

1. On the **Data Sources** tab, you’ll see your added data source.
2. Expand the data source to view the file system structure (directories, files, etc.).
3. You can **double-click** on any file to view its contents (e.g., text files, images, etc.).
4. You can also **right-click** a file or folder to view file details like metadata, hash values, and more.

#### Keyword Searching

To search for specific keywords within the data:

1. Go to the **Keyword Search** tab on the left sidebar.
2. Click on **New Search**.
3. Enter the keyword(s) you want to search for (e.g., "password", "invoice").
4. Click **Search**. Autopsy will scan through the data and provide a list of matches.
5. You can click on each result to view the context of the match in the file.

#### Viewing Deleted Files

Autopsy can help you recover and view deleted files:

1. Navigate to **File Analysis** in the left sidebar.
2. Expand the disk image data source and look for the **Deleted Files** section.
3. Click on **Deleted Files** to see files that have been deleted but are still recoverable.
4. You can **restore** deleted files by clicking on them and saving them to a different location.

#### Viewing File Metadata

Autopsy allows you to view the metadata of files, which can be valuable in forensics:

1. Select a file from the file list.

2. In the file details pane, scroll down to view the file’s metadata, including:
    - **File size**
    - **File type**
    - **Last accessed date**
    - **Last modified date**
    - **Owner/creator information**
    - **Hashes (MD5, SHA1, SHA256)**

### 6. Reporting

Autopsy has built-in reporting functionality to generate comprehensive reports of your findings.

#### Step 1: Generate a Report

1. Go to the **Reports** tab.
2. Click **Create Report**.
3. Select the type of report you want (e.g., **Full Report**, **Custom Report**).
4. Choose the format for the report (e.g., **HTML**, **CSV**, **PDF**).
5. Customize the report by selecting specific data to include.
6. Click **Finish** to generate the report.

#### Step 2: Save the Report

Once the report is generated, you can save it to your preferred location for sharing or documentation.

### 7. Additional Features and Tips

- **Timeline Analysis**: Autopsy allows you to analyze the timeline of file system events, such as file access and modification times. This can help identify patterns of activity over time.
- **Hash Analysis**: Autopsy can perform hash analysis to detect known files or artifacts that match hash values in forensic databases like the National Software Reference Library (NSRL).
- **File Carving**: Autopsy can recover fragmented or deleted files by looking for file signatures (carving).
- **Malware Detection**: Autopsy can detect malware artifacts, including executable files, suspicious processes, and other indicators of compromise (IoC).

### Conclusion

Autopsy is an incredibly useful tool for digital forensics investigations, offering powerful features for analyzing disk images, searching for keywords, recovering deleted files, and generating reports. By following this tutorial, you should be able to create a case, add data sources, analyze files, and generate reports for your forensic analysis.
