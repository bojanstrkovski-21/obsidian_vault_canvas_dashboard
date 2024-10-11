---
created: 2024-03-06T13:14:41 (UTC +01:00)
tags: []
source: https://medium.com/@Prinux/10-basic-linux-commands-that-you-need-to-know-50bdecf5a985
author: Prinux
---
![[image.jpeg]]
# 10 Basic Linux Commands That You Need To Know | Medium


## 1\. cd

The cd command is used for changing directories. cd stands for “change directory”. Use can to use to change from one folder to another.  
Changing Your Directory

-   You can use cd then, followed by the folder directory you want to change to.  
    for example:- `cd Downloads`
-   If you want to go through multiple directories at a time, instead of using `cd Downloads` and then `cd Wallpapers` you can use cd then followed by the directory name then the next directory name separated by a `/`  
    for example:- `cd Downloads/wallpapers`  
    `cd home/prinux/Desktop/Todolist`
-   if you want to change to the present directory to the previous one, you can use cd followed by two dots  
    for example:- `cd ..`  
    `pwd` (The `pwd` command is used to print the current working directory)  
    `/home/prinux/Desktop`
-   if you are present is the Documents directory of your system, you can use `/` in the beginning of the folder you wish to move  
    for example:- `cd /usr/share/applications`

## Creating Files & Folders

## 2\. touch

The touch command is used to make new files in the current working directory. With touch, you can create pretty much any file types.  
Example:- `touch hello.txt hello.csv hello.xcf`

## 3\. mkdir

The mkdir command is used to create folders in Linux.  
Example:- `mkdir foldername`

## 4\. chmod

The chmod command is used to make a script/file executable and non-executable. You can also set file permissions using chmod.  
Example:- `chmod +x filename`

## 5\. ls

the “ls” command shows the files present in the current working directory.  
You can use the `-al` flag to display all the hidden files also.

## 6\. rm

-   The `rm` command is used to remove files in your system.  
    Example:- `rm helloworld.py`
-   You can add the `-rf` flag along with rm to remove folders.

## Copying, Moving Your Files

## 7\. cp

-   The `cp` command is used for copying your files and folders. You must specify the file path to where the file must be copied to.  
    Example:- `cp hello.txt /home/prinux/Documents`
-   You can also use cp to copy the file contents of a file and save it by any other name. For that, you are not required to give the file path  
    example:- `cp hello.txt helloworld.txt`

## 8\. mv

-   The mv command is used to move your files and folders. As cp your are also required to give the file path to where the file is to be saved.  
    Example:- `mv hello.txt /home/prinux/Downloads`
-   The mv command can also be used to rename your files, as same as cp, you are not required to give the file path.  
    Example:- `mv hello.txt namaste.txt`

## Echoing Contents Into Your Terminal

## 9\. Cat

The `cat` command is used to print contents of a file into your terminal . This is suitable for small files as, after running it you will see the end of the file.  
example:- `cat helloworld.py`

## 10\. Less

The suitable for large files as it starts in the top part of the file and is required to scroll down for viewing the rest of the file.