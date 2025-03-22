# Guide to Using ExifTool for Metadata Collection on Linux

## Introduction

ExifTool is a powerful command-line utility for reading, writing, and modifying metadata in a variety of file formats, including images, videos, PDFs, and more. This guide will walk you through installing and using ExifTool on a Linux system to collect metadata from files.

---

## Video Demonstrations:
- [OSINT At Home #2 - Five ways to find EXIF/metadata in a photo or video](https://www.youtube.com/watch?v=d3NsT8lJRlE)
- [Extract iPhone and Android EXIF metadata from online photos using PYTHON // OSINT with Kali Linux](https://www.youtube.com/watch?v=A_itRNhbgZk)

---

## Installation

Most Linux distributions include ExifTool in their package repositories. Use one of the following commands based on your package manager:

### Debian/Ubuntu

```bash
sudo apt update && sudo apt install libimage-exiftool-perl -y
```

To verify installation, run:
```bash
exiftool -ver
```

This should return the installed version of ExifTool.

---

## Basic Metadata Extraction

To extract metadata from a file, use the following command:
```bash
exiftool filename
```

For example:
```bash
exiftool image.jpg
```

This will display all metadata associated with `image.jpg`:

---

## Extracting Specific Metadata Fields

You can filter the output to show only specific metadata fields. For example:
```bash
exiftool -Make -Model -DateTimeOriginal image.jpg
```

This command will display the camera make, model, and original date/time the image was taken.

---

## Extracting Metadata from Multiple Files

To extract metadata from all images in a directory:
```bash
exiftool *.jpg
```

Or recursively scan a directory:
```bash
exiftool -r /path/to/directory
```

---

## Exporting Metadata to a File

To save metadata output to a text file:
```bash
exiftool image.jpg > metadata.txt
```

For multiple files:
```bash
exiftool -r /path/to/directory > metadata.txt
```

---

## Removing Metadata

To strip all metadata from a file:
```bash
exiftool -all= -overwrite_original image.jpg
```

To remove only GPS data:
```bash
exiftool -gps:all= -overwrite_original image.jpg
```

---

## Modifying Metadata

To edit metadata fields, use:
```bash
exiftool -Artist="Your Name" image.jpg
```

To modify multiple fields at once:
```bash
exiftool -Artist="Your Name" -Copyright="Your Copyright" image.jpg
```

---

## Extracting Metadata in JSON Format

To output metadata in JSON format for further processing:
```bash
exiftool -json image.jpg
```

For multiple files:
```bash
exiftool -json *.jpg > metadata.json
```

---

## Conclusion

ExifTool is a versatile tool for analyzing and modifying metadata across various file types. Whether you're conducting digital forensics, verifying authenticity, or managing media files, ExifTool provides a comprehensive solution for metadata collection on Linux.

For further information, refer to the official documentation: [https://exiftool.org](https://exiftool.org/)
