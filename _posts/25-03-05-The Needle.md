---
title: "The Needle Challenge"
date: 2025-03-05 00:00:00
categories: [Hardware]
tags: [Hardware,Challenges,HackTheBox]
---

# the needle

- challenge describtion

![image.png](images/HTB/Hardware/the_needle/image.png)

- it’s embedded image

![image.png](images/HTB/Hardware/the_needle/image%201.png)

- to extract the file system of the image `binwalk -e firmware.bin`
- let’s try to connect to the given address

![image.png](images/HTB/Hardware/the_needle/image%202.png)

- mmm login , let’s try to search for it in the files.
- i found that

![image.png](images/HTB/Hardware/the_needle/image%203.png)

- so the user is : `Device_Admin`
- let’s investigate more in the file

![image.png](images/HTB/Hardware/the_needle/image%204.png)

- let’s get the password

![image.png](images/HTB/Hardware/the_needle/image%205.png)

- `qS6-X/n]u>fVfAt!`
