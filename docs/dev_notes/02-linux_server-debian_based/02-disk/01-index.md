---
title: Disk
permalink: /docs/dev_notes/linux_server-debian_based/disk/
---

When systems work, they usually have different kinds of data management, such as more reading, more writing, temporary data, permanent storage, and more. Every kind of disk is oriented for different purposes, like better for writing, for reading, or for long duration (storage case). With that in mind, here are the different storage sections for a Linux system:

* Boot (/boot): This section contains the boot loader and kernel files. It’s usually around 1GB in size.
* Home (/home): This section stores user data and personal files. It’s beneficial to have a separate /home section to keep user data separate from system files.
* Var (/var): This section is used for variable data files like logs, databases, and email spools. It’s useful to have a separate /var section to prevent these files from filling up the root filesystem.
* Tmp (/tmp): This section is used for temporary files. Having a separate /tmp section can help manage temporary data more effectively.
* Swap: This is used for swap space, which acts as an overflow for your system’s RAM. The size of the swap section can vary, but it’s often recommended to be equal to the amount of RAM or slightly more.
* EFI System (/efi): If your system uses UEFI, this section is necessary for booting. It’s typically around 100MB.
* Root (/): This is the main section where the operating system files are stored. It usually requires at least 20GB, but more space might be needed depending on your use case.

It is a good practice to separate different kinds of data into different sections by category or purpose. In some cases, certain types of data require specific file systems. Fortunately, a single device can have different sections, each with different file systems. The stored data in a system are separated by:

* Disk: physical device that contains data.
* Partition: Virtual section of the disk used to save data. It divides the disk into separate areas that can be managed independently. Each partition can function like a separate disk.
* Volume Partition: logical section within a partition. It acts as a "sub-partition", allowing further division of a partition for more granular data management.

These sections and other possibilities depend on your infrastructure. For detailed information about how to set up and manage the disk, check the left sidebar.
