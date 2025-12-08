# Author: Darkraicg492

# Description
Can you find the flag in this disk image?
Download the disk image [here](https://artifacts.picoctf.net/c/538/disko-1.dd.gz).

# Hints
1.  Maybe Strings could help? If only there was a way to do that?


# What is Disk Image
A Disk Image is an exact, bit-by-bit replica of a storage device (like a hard drive, USB stick, or SD card). Unlike a simple "copy-paste" of files, a disk image preserves the entire structure of the storage media, including:

Active files: The data currently visible to the user.

File system structures: The "map" that tells the computer where files live (e.g., the File Allocation Table).

Deleted data: Files that have been removed but not yet overwritten.

Unallocated space: "Empty" areas of the drive that may still contain fragments of old data.

In CTFs (like picoCTF), disk images are often provided as .dd or .img files. You analyze them using digital forensics tools (like Autopsy, The Sleuth Kit, or binwalk) rather than just opening them like a normal folder.

# What is disko-1.dd
The output of the file command in Linux. It analyzes the "magic bytes" (file headers) to identify what kind of file disko-1.dd is. Here is the breakdown for your writeup:

disko-1.dd: DOS/MBR boot sector, code offset 0x58+2, OEM-ID "mkfs.fat", Media descriptor 0xf8, sectors/track 32, heads 8, sectors 102400 (volumes > 32 MB), FAT (32 bit), sectors/FAT 788, serial number 0x241a4420, unlabeled

DOS/MBR boot sector: This tells you the file contains a Master Boot Record (MBR) partition table. It acts like a bootable disk (like a C: drive or a bootable USB).

OEM-ID "mkfs.fat": This is a major clue. It indicates the file system was created using the Linux tool mkfs.fat. This confirms the disk is formatted with the FAT (File Allocation Table) file system, which is compatible with almost all operating systems (Windows, Linux, macOS).

FAT (32 bit): This specifies the version is FAT32. Knowing this is crucial because it tells you which tools can read it (e.g., fsstat or fls from The Sleuth Kit would work perfectly here).

Media descriptor 0xf8: This hex code identifies the type of media. 0xf8 typically stands for a "Fixed Disk" (Hard Drive), as opposed to a removable floppy disk.

sectors 102400: This indicates the size of the volume. (102,400 sectors * 512 bytes/sector ≈ 50 MB).

# In summary for your writeup: "Running the file command revealed that disko-1.dd is a raw disk image containing a FAT32 file system. This means we can analyze it using standard forensic tools or even mount it to browse the files directly."

# Steps
1. Download the disk image with wget.
2. Got the "disko-1.dd.gz" gzip file. Unzip it with "gunzip disko-1.dd.gz" got disko-1.dd then use "file disko-1.dd" and "wc disko-1.dd" commands to see what kind of file it is and how big the file is.
3. Found that it's some kind of disk image "disko-1.dd: DOS/MBR boot sector, code offset 0x58+2, OEM-ID "mkfs.fat", Media descriptor 0xf8, sectors/track 32, heads 8, sectors 102400 (volumes > 32 MB), FAT (32 bit), sectors/FAT 788, serial number 0x241a4420, unlabeled" I don't really know what it's called exactly. and also found that it's quite a big file with 52428800 bytes in total.
4. First I used "less" command to see if there is any readable text in this binary file or not.
5. Found that there are quite some so I used " cat disko-1.dd | strings | grep "pico" "
6. And Voila! Found it.

Answer: picoCTF{1t5_ju5t_4_5tr1n9_e3408eef}
