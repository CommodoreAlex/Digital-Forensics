# Recovering Graphic Files on Linux

## Introduction

Recovering deleted or lost graphic files on Linux can be accomplished using powerful open-source tools such as `photorec`, `foremost`, and `scalpel`. These tools scan storage devices for file signatures and recover images even if the file system metadata has been deleted.

---

## Prerequisites

Ensure you have the following installed:
```bash
sudo apt update && sudo apt install testdisk foremost scalpel
```

---

## Method 1: Recovering Images Using PhotoRec

PhotoRec is part of the TestDisk suite and is designed for recovering various file types, including images.
### Steps:

1. **Launch PhotoRec:**
```bash
sudo photorec
```

2. **Select the disk:** Choose the storage device where the deleted images were stored.

3. **Choose partition type:** Select the correct file system type (e.g., ext4, FAT32, NTFS).

4. **Select file types:** Navigate to `File Options` and select only graphic file types such as `jpg`, `png`, `gif`, etc.

5. **Choose recovery directory:** Specify a different drive or folder to store recovered files.

6. **Start the recovery process:** PhotoRec will scan and restore images to the specified directory.

---

## Method 2: Recovering Images Using Foremost

Foremost is a forensic tool used to recover files based on predefined headers, footers, and data structures.

### Steps:

1. **Run foremost on the target drive or image file:**
```bash
sudo foremost -t jpg,png,gif -i /dev/sdX -o ~/recovered_images/
```

- `-t` specifies file types.
- `-i` is the input drive or image file.
- `-o` is the output directory where recovered files will be stored.

2. **Review the recovered files:** Navigate to the output directory to check recovered images.
```bash
ls ~/recovered_images/
```

---

## Method 3: Recovering Images Using Scalpel

Scalpel is another signature-based file recovery tool that allows fine-tuned control over recovery parameters.

### Steps:

1. **Edit Scalpel configuration file:**
```bash
sudo nano /etc/scalpel/scalpel.conf
```

Uncomment the file types you want to recover (e.g., `jpg`, `png`).

2. **Run Scalpel on a disk or image file:**
```bash
sudo scalpel /dev/sdX -o ~/scalpel_recovered/
```

3. **Check the output directory for recovered images:**
```bash
ls ~/scalpel_recovered/
```

---

## Conclusion

Using `photorec`, `foremost`, and `scalpel`, you can effectively recover deleted graphic files on Linux. Each tool has its strengths, and the best choice depends on the scenario and desired level of customization. Always recover files to a separate disk to prevent overwriting existing data.
