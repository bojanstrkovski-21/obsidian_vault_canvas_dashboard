---
link: "https://devconnected.com/how-to-manage-root-account-on-ubuntu-20-04/"
title: "How To Manage Root Account on Ubuntu 20.04 – devconnected"
timestamp: "1/28/2023"
domain: "devconnected.com"
excerpt: "Learn how to manage the root account on Ubuntu 20.04 by checking the lock status, locking and unlocking it Manage root SSH account."
word_count: "4952"
status: "unread"
---
![[Pasted image 20230128104002.png]]

On Linux, the **root account** is probably one of the most powerful accounts that there is.

Considered **the most privileged account on a Unix system**, root can perform any tasks needed for system administration.

Navigating a specific folder, killing any process or deleting a directory, root is so powerful that it has to be managed properly.

In this tutorial, you will learn about the different facets of **the root account on Ubuntu 20.04**.

You will learn to lock and unlock it, to change its password as well as disabling it when trying to remotely access your machine.

Finally, you will know the difference between the root account and the sudo command that is used quite often.

-   [Prerequisites](#Prerequisites "Prerequisites")
-   [Check Lock Status of Root Account](#Check_Lock_Status_of_Root_Account "Check Lock Status of Root Account")
    -   [Inspecting the shadow file](#Inspecting_the_shadow_file "Inspecting the shadow file")
    -   [Using the passwd command](#Using_the_passwd_command "Using the passwd command")
-   [Locking & Unlocking Root Account](#Locking_Unlocking_Root_Account "Locking & Unlocking Root Account")
    -   [Changing the root password](#Changing_the_root_password "Changing the root password")
-   [Disabling Root Login over SSH](#Disabling_Root_Login_over_SSH "Disabling Root Login over SSH")
-   [Conclusion](#Conclusion "Conclusion")

## Prerequisites

For most of the commands used in this tutorial, you will need **sudo privileges.**

![using groups command on linux](https://devconnected.com/wp-content/uploads/2020/11/groups.png)

If the **sudo group** is part of your current groups, it means that you should be able to execute the commands listed below.

If not, make sure to check our guide on [**how to get sudo rights on Ubuntu 20.04**](https://devconnected.com/how-to-add-user-to-sudoers-on-ubuntu-20-04/)**.**

## Check Lock Status of Root Account

Given your distribution, the root account may or may not be locked by default.

By default, when [installing Ubuntu 20.04](https://devconnected.com/how-to-install-and-configure-ubuntu-20-04-with-gnome/), you created a user account that got the sudo privileges.

As you can see, by default, the “**devconnected**” user is in the “**sudo**” group, which allows it to have temporary root rights if needed.

*But what about the actual root account?*

**To know if your root account is locked or not, you can either check the “/etc/shadow” file or use the passwd command with the “-S” option.**

### Inspecting the shadow file

On Linux, the shadow file is a very sensitive file : it contains the encrypted passwords for all the users available on your machine.

As a consequence, its content should never be seen or modified by a regular user.

In our case, we are only going to pay attention to the information related to the root account.

**In order to know if the root account is locked or not, look for an exclamation mark in the field that should contain the encrypted password. If there is one, that means that the account is locked.**

```
$ sudo getent shadow root

$ sudo cat /etc/shadow | grep root
```

![root account locked](https://devconnected.com/wp-content/uploads/2020/11/root-locked.png)

If you are curious, this point is actually specified in the documentation when reading the page dedicated to “**shadow**“.

```
$ man shadow
```

![man shadow file](https://devconnected.com/wp-content/uploads/2020/11/encrypted-password.png)

### Using the passwd command

**Usually, the** [**passwd command**](https://man7.org/linux/man-pages/man1/passwd.1.html) **is used in order to change a user’s password on Linux.**

However, the “**\-S**” option can be used in order to display the account “**status**” information.

```
$ sudo passwd -S root
```

![](https://devconnected.com/wp-content/uploads/2020/11/passwd-command.png)

When using the “-S” option, you want to pay attention to the second column : it actually displays the status of the account (L for “**locked**” and P for “**usable password**“).

In this case, the **root account** is locked while the regular user account has a password.

## Locking & Unlocking Root Account

By default, it is recommended to lock the root account and to use dedicated privileged accounts in order to perform critical operations.

**In order to lock the root account, you have to use the “usermod” command with the “-L” option for “lock” and specify the root account.**

```
$ sudo usermod -L root
```

Make sure to verify that the account is correctly locked by using one of the commands we described in the previous section.

![lock root account](https://devconnected.com/wp-content/uploads/2020/11/lock-root-account-1.png)

**In order to unlock the root account, you have to use the “usermod” command with the “-U” and specify the root account.**

```
$ sudo usermod -U root
```

### Changing the root password

**In order to change the root password, you have to use the “passwd” and specify the root account.**

```
$ sudo passwd root
```

![changing root password](https://devconnected.com/wp-content/uploads/2020/11/changing-root-password.png)

After changing your password, the account will be automatically unlocked.

In order to switch to the root account, you can use the well-known [“su” command](https://devconnected.com/how-to-change-user-on-linux/) without any arguments (the default account is root).

```
$ su - 
```

![connect to root using su](https://devconnected.com/wp-content/uploads/2020/11/connect-to-root.png)

## Disabling Root Login over SSH

In some cases, you want to keep the **local root account accessible** for administration but disabled for remote access.

If you are [**accessing your machine over SSH**](https://devconnected.com/working-remotely-with-linux-systems/), you should disable root login whenever your server is active.

By default, on recent distributions, root login is set to “prohibit-password”, which means that you can still connect to it using SSH key authentication.

**In order to disable it completely, head over to your “/etc/ssh/sshd\_config” file and identify the line with “PermitRootLogin”.**

```
#PermitRootLogin

PermitRootLogin no
```

![disable root ssh password](https://devconnected.com/wp-content/uploads/2020/11/ssh-root-login.png)

Of course, make sure to restart your SSH server for the modifications to be taken into account.

```
$ sudo systemctl restart sshd
```

## Conclusion

In this tutorial, you learnt how **you can manage the root account on Linux easily**.

You learnt that there are many different ways of **checking for the lock status** **of the root account**, using the shadow file or the passwd command for example.

If you are interested in **Linux System Administration**, we have a complete section dedicated to it on the website, so make sure to check it out!

[![](https://devconnected.com/wp-content/uploads/2019/09/100-1024x341.png)](https://devconnected.com/category/linux-administration/)