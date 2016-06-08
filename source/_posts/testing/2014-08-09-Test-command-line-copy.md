---
layout: post
title: "[Testing] Test Command Line Copy"
comments: true
category: Testing

---

### Question 

[link](http://stackoverflow.com/questions/6591652/how-do-i-test-the-copy-command-in-the-windows-environment)

> testing the copy command in windows environment 

### Solution

[The most important point](http://stackoverflow.com/a/6591999) is to __come up with different domains of inputs and scenarios__. 

### Copying between:

1. network share
1. A really slow network share across the Internet
1. partitions
1. disks
1. disks of different types (flash, usb, external sata, SSD, etc...)
1. directories
1. within the same directory

### Naming

1. Normal file name
1. Filename that exceeds 8.3 (verylongfilename.whatever)
1. Copying a very long file name, but referencing it by it's 8.3 name (copy verylo~1.wha d:\)
1. A full directory path that exeeds MAX_PATH (260) characters (e.g. c:\a\very\long\directory\name\that\goes\on\forever\in\length......foo.txt)
1. By absolute addressing (\\?\\c:\foo\foo.txt)
1. wildcards (e.g. *.* *.txt foo?.txt )
1. A filename with unicode characters
1. A filename with illegal characters in it (there are creative ways to get these files on disk)

### Attributes

1. Testing with different file attributes (read-only, hidden, system, archive, etc...)
1. Validate timestamp is preserved across copies
1. Validate timestamp is preserved across network file share copies when the destination machine is in another timezone
1. NTFS ACLs are preserved

### Addressing types

1. reference by absolute path (e.g. copy c:\some\directory\foo.txt c:\other\place\foo.txt)
1. reference by relative path (e.g. copy ..\..\documents\whatever\foo.txt subdirectory/foo.txt)
1. By absolute drive letter into current working directoroy of destination (with no path (e.g. copy foo.txt d:)
1. Network share mounted to a drive letter

### Failure cases, edge cases, and hack attacks

1. Try to copy a file onto itself (e.g copy c:\foo.txt c:\foo.txt)
1. Copy when the network share is down.
1. Unplug the network cable in the middle of a network file copy
1. copy to a read only directory
1. copy when the source file is locked.
1. copy the when destination file exists but the destination file exists and is read only
1. Detach the external disk right before the file copy starts
1. disk is near full (But would be full before the entire copy finishes)
1. disk is full
1. Unplug the power cable in the middle of the copy!
1. During a very long copy, start another copy with the same source file, but to another destination
1. During a very long copy, start another copy with a different source file, but the the same destination
1. During a very long copy, start another copy with the same source and destination files!

### File types

1. ascii file
1. unicode file
1. binary file

### Environments

1. RAID configurations
1. FAT and NTFS
1. Windows XP, Vista, 7, Server 2003, etc... (you can quantify this by asking the requirement of "which OS" up front)
1. Virtual Machine (VMWare, virtual PC, hypervisor, etc...)
1. Intel and AMD
