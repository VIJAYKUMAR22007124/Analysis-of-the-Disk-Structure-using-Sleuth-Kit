# Analysis-of-the-Disk-Structure-using-Sleuth-Kit
## AIM:
To analyze the disk structure of a given disk image using Sleuth Kit tools in Kali Linux.

## DESIGN STEPS:
### Step 1:
Obtain or create a disk image file (e.g., disk.dd) to analyze. Open the terminal in Kali Linux.

### Step 2:
Use Sleuth Kit tools like mmls, fsstat, and fls to examine the partition layout, file system details, and file listing.

### Step 3:
Interpret the output of the tools to understand the disk structure, including partitions, sectors, and files.

## PROGRAM:
Sleuth Kit Disk Analysis Commands

## PRELIMINARY STEP:
### Step1:

  ●	Run command prompt as administrator
  ![image](https://github.com/user-attachments/assets/104e2b3f-74f0-4de5-b734-bf2df81e8bc2)

### Step2:

  ●	Verify Sleuthkit is installed.
  ![image](https://github.com/user-attachments/assets/c9c0a8be-0162-48e8-b215-c2b7e4c6ddcb)

### Step3:

  ●	Navigate to the binary file of Sleuthkit in command prompt: 
  ![image](https://github.com/user-attachments/assets/0b21d418-2da8-48cd-8a06-7796eeb478eb)

## PROCEDURE:
## ANALYSE THE FILE USING SLEUTHKIT TOOL:

### 1. View File Metadata
  ●	Use istat to view metadata of a file/directory using its inode number 0:

  ●	Command:  istat.exe -f filetype “file path” <inode number>
![image](https://github.com/user-attachments/assets/44a01388-eb16-40a6-961b-13bb2be7f8ed)

  #### OUTPUT SUMMARY:
  
  
  ●	Type: Directory

  ●	Permissions: dr-xr-xr-x (read + execute for all)

  ●	Created On: 2025-04-24 14:47:01 (India Standard Time)

  ●	Size: 2048 bytes, Sectors Used: 30


### 2. View Metadata of Inode 1

  ●	Use istat to view metadata of a file/directory using its inode number 1:

  ●	Command:  istat.exe -f filetype “file path” <inode number>

  ![image](https://github.com/user-attachments/assets/6f59244f-4bbb-41b6-bdb7-e4ff0775fd68)

  #### OUTPUT SUMMARY:

  ●	Name: Metasploitable2-Linux

  ●	Type: Directory 

  ●	Permissions: dr-xr-xr-x (read + execute for all)

  ●	Created On: 2025-04-24 14:45:47 (India Standard Time)

  ●	Size: 2048 bytes, Sectors Used: 31

### 3. View Metadata of Inode 6

  ●	Use istat to view metadata of a file/directory using its inode number 6:

  ●	Command:  istat.exe -f filetype “file path” <inode number>

  ![image](https://github.com/user-attachments/assets/d4196299-f348-4968-9a1d-8b9a6782a52c)

  #### OUTPUT SUMMARY:

  ●	Name: Metasploitable.vmxf

  ●	File Name: Metasploitable.vmx — This is a VMware configuration.

  ●	Type: File — It's a regular file, not a folder.

  ●	Permissions: -r-xr-xr-x — Read & execute allowed for everyone, no write access.

  ●	Created Time: 2025-04-24 14:39:31 (India Standard Time) — This is when the file was added to the ISO.

  ●	Sectors: 940295

### 4. Analysis of Inode 6 Metadata via icat Utility

  ●	Use icat to extract file content using its inode number 6:

  ●	Command:  icat.exe -f filetype “file path” <inode number>

  ![image](https://github.com/user-attachments/assets/5840bdcf-4831-4346-852b-36acec190725)

  #### OUTPUT SUMMARY:
  The command retrieves the contents of a VMware virtual machine configuration file (Metasploitable.vmx). This file defines how the virtual machine is set up, including:

  ●	Hardware settings like CPU (numvcpus = "1"), RAM (memsize = "512"), and SCSI controller.

  ●	Networking options, with both NAT (ethernet0) and Host-only (ethernet1) adapters configured.

  ●	Storage devices, such as virtual hard disk (Metasploitable.vmdk) and CD-ROM (auto detect).

  ●	Additional devices like USB, EHCI, and multiple PCI bridges.

  ●	VM metadata, including UUID, display name (Metasploitable2-Linux), OS type (ubuntu), and annotations.

  ●	Security note: The annotation warns that this VM is intentionally vulnerable and should not be exposed to untrusted networks.

### 5. View File System Details Using fsstat
  ●	Use fsstat to view file system metadata of the ISO image.

  ●	Command:  fsstat -f filetype “file path”
  ![image](https://github.com/user-attachments/assets/dfa47b09-0323-4047-82c3-1a97e9d36c25)

  #### OUTPUT SUMMARY:
  PRIMARY VOLUME DESCRIPTOR 1 File System Information:

  •	File System Type: ISO9660

  •	Volume Name:  24_04_2025

  •	Volume Set Size: 1

  •	Volume Set Sequence: 1

  •	Recording Application: AnyBurn

  Metadata Information:

  •	Path Table Location: 22–22

  •	Inode Range: 0 – 8

  •	Root Directory Block: 31390335418499100

  Content Information:

  •	Sector Size: 2048 bytes

  •	Block Size: 2048 bytes

  •	Total Sector Range: 0 - 940295

  •	Total Block Range: 0 - 940295

### 6.List Directory Structure

  ●	Use fls to view directory structure.

  ●	Command:  fls -f filetype -r  “file path”
  ![image](https://github.com/user-attachments/assets/b7c25dd1-4351-40d4-9ecb-ba780facea20)


  #### OUTPUT SUMMARY:

  •	Root Directory: metasploitable-linux-2.0.0 (Inode 1)

  •	Contained Files and Subdirectories:

  o	Metasploitable2-Linux/ — A directory (Inode 2)

  o	Metasploitable.nvram — NVRAM file storing BIOS settings (Inode 3)

  o	Metasploitable.vmdk — Virtual hard disk file (Inode 4)

  o	Metasploitable.vmsd — Snapshot metadata file (Inode 5)

  o	Metasploitable.vmx — Main configuration file (Inode 6)

  o	Metasploitable.vmxf — Extended configuration file (Inode 7)

### 7. Image File Information

  ●	Use img_stat – Sleuth Kit utility for viewing image file metadata.

  ●	Command:  img_stat  “file path”
  ![image](https://github.com/user-attachments/assets/e267fbf2-0f56-4007-aadf-cd2563c659a6)

  #### OUTPUT SUMMARY:
  •	Image Type: raw

  •	Size in Bytes: 1925726208 (approx. 1.79 GB)

  •	Sector Size: 512 bytes

  •	Confirms that the input image is a raw format disk image with standard sector configuration.
## RESULT:
The analysis was performed successfully using Sleuth Kit, and the disk structure was understood in detail.
