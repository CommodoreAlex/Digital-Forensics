# FTK Imager Tutorial: Basic Usage

## Introduction

FTK Imager is a forensic imaging tool used to create copies of digital evidence without modifying the original data. This guide covers the basic usage of FTK Imager for forensic imaging.

---

## Digital Forensics with FTK Imager (TryHackMe Advent of Cyber Day 8):
- [John Hammond Demonstraton](https://www.youtube.com/watch?v=7wB0HNf1qh4)

---

## Installing FTK Imager

1. Download FTK Imager from the [Exterro website](https://accessdata.com/product-download/ftk-imager).
2. Install the software by following the on-screen instructions.
3. Launch FTK Imager after installation.

---

## Creating a Forensic Image

1. **Open FTK Imager**
    - Run FTK Imager as an administrator.
2. **Add Evidence Item**
    - Click on `File` > `Add Evidence Item`.
    - Select the type of evidence source (Physical Drive, Logical Drive, Image File, or Folder Contents).
    - Click `Next` and select the appropriate drive or file.
3. **Create a Disk Image**
    - Click on `File` > `Create Disk Image`.
    - Choose the source (Physical or Logical Drive).
    - Click `Next` and select the drive to be imaged.
4. **Select Image Type**
    - Choose the desired format:
        - `Raw (DD)`
        - `E01 (EWF)`
        - `AFF (Advanced Forensic Format)`
    - Click `Next`.
5. **Configure Destination**
    - Click `Add` to select the destination folder.
    - Enter a case number, evidence number, and examiner information if required.
    - Ensure `Verify images after they are created` is checked.
    - Click `Start` to begin imaging.
6. **Verify Image Integrity**
    - Once completed, verify the MD5/SHA1 hash matches the original file to ensure forensic integrity.

---

## Viewing Acquired Images

1. Click `File` > `Add Evidence Item`.
2. Select `Image File` and browse for the created forensic image.
3. Load the image and use FTK Imager’s built-in file viewer to inspect contents.

---

## Exporting Files from an Image

1. Load the forensic image in FTK Imager.
2. Navigate to the file or folder you want to export.
3. Right-click and choose `Export`.
4. Select the destination folder and save the exported files.

---

## Conclusion

FTK Imager is a powerful and user-friendly tool for digital forensic investigations. By following this guide, you can create, verify, and analyze forensic images while maintaining the integrity of the evidence.
