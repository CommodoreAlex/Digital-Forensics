# Disk Imaging & File System Analysis Guide

Disk imaging and file system analysis are essential steps in digital forensics for creating a copy of the digital evidence (e.g., hard drives, USB drives, network shares) and analyzing its contents. This guide will walk you through the steps of creating disk images, analyzing the file system, and performing basic file system analysis using popular forensic tools.

---

## 1. Introduction to Disk Imaging

Disk imaging is the process of creating a bit-by-bit copy of a storage device, such as a hard drive, USB drive, or network share. The image file, often in formats like `.dd`, `.img`, or `.e01`, captures the entire content of the device, including all sectors, partitions, and free space.

**Why use Disk Imaging?**

- **Preservation of Evidence**: The original device is not altered during analysis.
- **Repeatability**: Analysts can recreate the same environment without touching the original device.
- **Recovery of Deleted Files**: Disk images contain information about deleted files and file fragments.

---

## 2. Creating a Disk Image

### Using `dd` for Disk Imaging

`dd` is a powerful Linux command used to create a raw bit-by-bit image of a storage device. This is one of the most commonly used tools in digital forensics.

#### Steps:

1. **Identify the Source Device**
    - Run `lsblk` or `fdisk -l` to identify the device you wish to image (e.g., `/dev/sda` for a hard drive).

2. **Create the Disk Image**

Use the following `dd` command to create an image:
```bash
sudo dd if=/dev/sda of=/path/to/output.img bs=4M status=progress
```

- `if=/dev/sda`: Input file (source device).
- `of=/path/to/output.img`: Output file (disk image).
- `bs=4M`: Block size (optional, you can adjust for performance).
- `status=progress`: Show progress of the operation.


3. **Verify the Image**

After creating the image, it’s important to verify that the image matches the original device:
```bash
sha256sum /dev/sda
sha256sum /path/to/output.img
```

Compare the SHA256 hashes to ensure the image is an exact replica of the source.


---

### Using FTK Imager

FTK Imager is a popular forensic tool with a graphical interface, commonly used in forensic investigations to create disk images and analyze files.

#### Steps:

1. **Launch FTK Imager**
    - Open FTK Imager and click **Create Disk Image**.
2. **Select the Source**
    - Choose the source you want to image, whether it's a physical drive, a local file, or a network share.
3. **Choose the Image Format**
    - Choose a format for the image file (e.g., raw, E01, or AFF).
4. **Select Destination Folder**
    - Specify the destination folder where the disk image will be saved.
5. **Verify Image**
    - FTK Imager will calculate the hash values (MD5, SHA1) of the disk image during the creation process. You can use these hashes to verify the integrity of the image after the process is complete.

---

## 3. Mounting and Analyzing Disk Images

Once the disk image has been created, it needs to be mounted and analyzed.

### Mounting an Image on Linux

To mount a disk image for analysis on a Linux system, follow these steps:

1. **Create a Mount Point**
```bash
sudo mkdir /mnt/image
```

2. **Mount the Image**
```bash
sudo mount -o loop /path/to/image.img /mnt/image
```

- The `-o loop` option allows you to mount the image file as if it were a physical device.

3. **Access the Mounted Image**
- Now you can access the mounted image through `/mnt/image` to explore its file system.

4. **Unmount the Image**
```bash
sudo umount /mnt/image
```

---

### File System Analysis with Autopsy

Autopsy is a digital forensics tool that allows you to analyze file systems and recover deleted files, search for keywords, and examine artifacts in disk images.

#### Steps:

1. **Create a New Case in Autopsy**
- Launch Autopsy and create a new case by clicking **Create New Case**.
- Provide the case name, case number, and other relevant details.

2. **Add a Data Source**
- Choose **Disk Image or VM File** to add the disk image you created earlier.

3. **Analyze the Disk Image**
- Autopsy will parse the image and display the file system structure.
- You can browse through directories, view file metadata, and explore file contents.

4. **Run a Keyword Search**
- Use Autopsy’s keyword search feature to search for specific terms, such as filenames, user activity, or other relevant keywords.


---

## 4. File System Analysis Techniques

### Navigating the File System

In a typical forensic analysis, the first task is to navigate the file system to locate evidence of interest. Common things to look for include:
- User activity (e.g., documents, images).
- System logs (e.g., event logs, registry).
- Suspicious files (e.g., executables, scripts).

### Recovering Deleted Files

Even after a file is deleted, remnants of the file often remain on the disk, including its metadata and some data blocks. Forensics tools like **Autopsy** and **Sleuth Kit** can help you recover these deleted files.

- Use **Autopsy** to look at the **Deleted Files** section under the data source.
- You can attempt to recover files and inspect their metadata, even if the user has deleted them.

### Keyword Search

Keyword searches are an essential part of forensic analysis. They help find relevant artifacts quickly, such as:

- User credentials
- Command history
- File names or paths
- Keywords related to criminal activity (e.g., "hacking", "password", etc.)

Tools like **Autopsy** or **grep** (in Linux) can help with this type of search.

---

## 5. Reporting and Documentation

Once the analysis is complete, documenting your findings is crucial for presenting evidence in a forensic investigation.

### Generating Reports in Autopsy

Autopsy allows you to generate a comprehensive report for your case. Reports can be generated in various formats like **PDF**, **HTML**, or **CSV**.

1. Go to the **Reports** tab.
2. Select **Create Report**.
3. Choose the report format and customize it according to your needs.
4. Generate the report and save it for further analysis or presentation.

---

## Conclusion

Disk imaging and file system analysis are critical steps in digital forensics, providing investigators with the ability to preserve and examine digital evidence. This guide covered the process of creating disk images using `dd` and FTK Imager, mounting and analyzing disk images, performing file system analysis, and generating reports. By mastering these techniques, you'll be able to effectively investigate digital evidence and recover valuable data in forensic cases.
