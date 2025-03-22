# Using a Write Blocker with FTK Imager to Create a Forensic Copy

## Overview

A write blocker is a crucial tool in digital forensics that prevents any modifications to the original evidence while allowing read-only access for analysis. This guide covers how to use a hardware write blocker with FTK Imager on a Windows system to create a forensic copy of a drive.

## Prerequisites

- A **hardware write blocker** (e.g., Tableau, CRU WiebeTech, or Kanguru)
- A **target storage device** (external hard drive or USB with sufficient space)
- **FTK Imager** installed on your computer (available from Exterro's website)
- The **source drive** (HDD, SSD, or USB) to be imaged

## Steps to Create a Forensic Copy

### 1. Connect the Write Blocker

1. Power off the source drive.
2. Connect the source drive to the write blocker using the appropriate interface (SATA, IDE, USB, etc.).
3. Connect the write blocker to your forensic workstation via USB or another supported connection.
4. Power on the write blocker (if applicable) and verify that it is functioning correctly.

### 2. Verify the Write Blocker Functionality

1. Open **Disk Management** (Windows) or use `lsblk` (Linux) to check if the source drive is detected.
2. Ensure the drive is set to **read-only** and that no unintended writes occur.

### 3. Launch FTK Imager

1. Open **FTK Imager** on your forensic workstation.
2. Click **File > Create Disk Image**.
3. Select **Physical Drive** or **Logical Drive** depending on your needs.
4. Choose the source drive connected via the write blocker and click **Next**.

### 4. Select Image Type

1. Choose an appropriate forensic image format:
    - **E01 (EnCase)** – Supports compression and hashing.
    - **RAW (DD)** – Uncompressed bit-by-bit copy.
    - **AFF (Advanced Forensic Format)** – Supports metadata storage.
2. Click **Next**.

### 5. Configure Image Destination

1. Click **Add** to set the destination for the forensic image.
2. Choose a destination folder on your external storage.
3. Set a **case number**, **evidence number**, and other relevant details.
4. Enable **MD5 or SHA-1 hashing** for verification.
5. Click **Finish** to confirm.

### 6. Start the Imaging Process

1. Click **Start** to begin the imaging process.
2. Monitor the progress to ensure no errors occur.
3. Once complete, verify the hash values to confirm integrity.

### 7. Verify the Image Integrity

1. Compare the generated **MD5 or SHA-1 hash** against the original.
2. Use FTK Imager’s built-in verification or run:

```bash
md5sum image.E01
sha1sum image.E01
```

in a Linux terminal to cross-check.

3. If the hash values match, the forensic copy is verified.

## Conclusion

Using a write blocker with FTK Imager ensures a proper forensic workflow by preventing accidental modifications to the original evidence. Always verify hash values to maintain data integrity. This process is a fundamental practice in digital forensics investigations.
