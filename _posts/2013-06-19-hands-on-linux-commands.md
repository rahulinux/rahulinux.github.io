---
ID: 610
title: Useful Linux Commands
author: Rahul Patil
date: 2013-06-19 16:57:35
post_excerpt: ""
categories: [ "linux" ]
layout: post
published: true
---

In this post, I want to list some useful shell scripts/commands, keyboard shortcuts , some may be already known to you and some may not be, but nonetheless I feel its my duty to share some not so trivial things to search and find that easily sometimes, also I needed a quick reference of these which may be useful for Linux System Admin, coders including me in future, so here we go.

**1. Place the argument of the most recent command on the shell**

When typing out long arguments, such as

```shell
tail -f /var/log/messages
```

You can put that argument on your command line by holding down the <kbd>ALT</kbd> key and pressing the period <kbd>.</kbd> or by pressing <kbd>ESC</kbd> then the period <kbd>.</kbd>

For example: tail -f <kbd>ALT</kbd> + <kbd>.</kbd>

this would put '/var/log/messages' as my argument. Keeping pressing <kbd>ALT</kbd>+<kbd>.</kbd> to cycle through arguments of your commands starting from most recent to oldest. This can save a ton of typing.

In Mac you can use <kbd>ESC<kbd><kbd>.</kbd>

**2. Man Pages**

Command `man` is your friend, Before googling , you should check man pages to solve issue yourself. here is simple Example, if want to understand File System Hierarchy, then simply use :

```shell
man hier
``` 

**3. SSH**

If ServerB is Not accessible but you can access ServerA , and ServerA can access ServerB , then you can use .

```shell
ssh -t ServerA  ssh  ServerB
```

Directly ssh to ServerB that is only accessible through ServerA

**4. RPM, DPKG**

If you want to Check which file belongs to which package.

In RHEL/CentOS

```shell
rpm -qf   /path/of/file
```

In Ubuntu

```shell
dpkg -S  /path/of/file
```

Note that if package installed using source code, then it will never show , only apply for files those are installed through package manager.


**5. Get absolute Path of file**

This trick very useful in Shell Script.

if you want to check absolute path of file which is in your current directory :

```shell
readlink  -f  filename
```

If you want to get absolute path of script it self

```shell
This_Script=$(readlink -f $0 )
```

**6. Backup/Rename File**

If you want to Backup file with current date name.

```shell
cp  filename{,-bkp-$(date +%F)}
```

If you want to rename file 

```shell 
mv filename{,-old}
```

**7. Fast, built-in pipe-based data sink**

```shell
 Yourcommand   |:
```

This is shorter and actually much faster than >/dev/null (see sample output for timings)

**8. Save Command in History Without Executing it.**

Type your command and Simple Press <kbd>ALT</kbd>+<kbd>#</kbd>

**9. Search and Execute Recent commands from your history**

Simply Press <kbd>Ctrl</kbd>+<kbd>r</kbd> and type some word to search your Command, Simply do Next using <kbd>Ctrl</kbd>+<kbd>r</kbd>  to cycle through commands. 

**10. Fast Execute recent command.**

Suppose you have Open file using vim then you save file and run some other command, 
now just run 

```shell
!vim
```
this will execute last command start with vim from your history. 



If you want to share any command line tips & tricks, just post in comments.
