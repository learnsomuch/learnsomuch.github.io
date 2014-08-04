---
layout: post
title:  "Inner concept in Linux – Changing password of non-privileged users"
date:   2011-12-21 23:55:55
categories: linux
meta: Inner concept in linux
---


There could be multiple users/groups/others which is a non-privileged user to perform a system function that requires root privileges, such as changing a password in Linux.
One of the possible solution is to give the user root privileges;

But, This also gives the user complete control over the system, which is generally bad from a security perspective. Instead, the program is given the ability to run as if it were the root user, so that the system function can be carried out properly and the user isn’t actually given full system control. 

This type of permission is called the suid (set user ID) permission or bit. When a program with the suid permission is executed by any user, that user’s euid (effective user ID) is changed to the uid of the program’s owner, and the program is executed. After the program execution completes, the user’s euid is changed back to its original value. This bit is denoted by the s in bold in the following file listing. There is also a sgid (set group ID) permission, which does the same thing with the effective group ID.

```
-rwsr-xr-x 1 root san 6023 Dec 20 12:00 /usr/bin/passwd 
```

Here is the passwd path with file permissions as mentioned above.If a user wanted to change password, then we would needs to run /usr/bin/passwd, which is owned by root and has the suid bit on. The uid would then be changed to root’s uid (which is 0) for the execution of passwd, and it would be switched back after the execution completes. This is where binary (1 or 0) comes in typical core techincal computers concepts involves. Programs that have the suid permission turned on and that are owned by the root user are typically called suid root programs.

## Posibility of hacking - Appraoch

Changing the flow of program execution becomes very powerful. If the flow of a suid root program can be changed to execute an injected piece of arbitrary code, then the attacker could get the program to do anything as the root user. If the attacker decides to cause a suid root program to spawn a new user shell that he/she can access, the attacker will have root privileges at a user level. This is generally bad from a security perspective, as it gives the attacker full control of the system as the root user.

## Learning from he above scenario

Hacking to change the execution flow of a program still isn’t actually breaking any of the program or cracking passwords; Instead, hacker getting known with new ways/appraoches which never expected while developing. To do these methods of exploitation, and to write programs to prevent these types of exploits, requires a greater understanding of the lower-level Programming such as program memory.

Thanks for spending some time in reading this. Hope you enjoyed learning!
BR, Sankar