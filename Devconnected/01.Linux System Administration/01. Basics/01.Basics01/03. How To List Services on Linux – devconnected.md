---
link: "https://devconnected.com/how-to-list-services-on-linux/"
title: "How To List Services on Linux – devconnected"
timestamp: "1/28/2023"
domain: "devconnected.com"
excerpt: "Learn how you can easily list your services on Linux, whether you are using systemd or Sysvinit. List services with options on Linux."
word_count: "6322"
status: "unread"
---
![[Pasted image 20230128080427.png]]

As a system administrator, you are probably dealing with a lot of **services** every day.

On Linux, **services** are used for many different purposes.

They may be used in order to start a SSH server on your machine or they can perform some operations on a specific hour or day.

Whether you are using a Debian based distribution or a RedHat one, querying services is very similar.

However, given the distribution you are using, and more specifically the initialization system (init or systemd), you may have to use different commands.

In this tutorial, you will learn how you can, given your system manager, **list all services on your Linux machine.**

-   [Determine the system manager used](#Determine_the_system_manager_used "Determine the system manager used")
-   [List Services using systemctl](#List_Services_using_systemctl "List Services using systemctl")
    -   [List All Services on Linux using list-units](#List_All_Services_on_Linux_using_list-units "List All Services on Linux using list-units")
    -   [List Services By State](#List_Services_By_State "List Services By State")
    -   [List All Service Files using list-unit-files](#List_All_Service_Files_using_list-unit-files "List All Service Files using list-unit-files")
-   [List Services using service](#List_Services_using_service "List Services using service")
    -   [List SysVinit Services in Folders](#List_SysVinit_Services_in_Folders "List  SysVinit Services in Folders")
-   [Conclusion](#Conclusion "Conclusion")

## Determine the system manager used

As you probably know, recent distributions use the [**Systemd system manager**](https://en.wikipedia.org/wiki/Systemd).

However, it has not always been the case : in the past, most distributions used the **SysVinit system manager.**

As a consequence, there are really two ways of managing your services on a Linux system.

Before learning the commands to list services, you have to know the system manager that you are currently using.

**To determine your current system manager, the easiest way is to use the “pstree” command and to check the first process ever run on your system.**

```
$ pstree | head -n 5
```

![pstree command on linux](https://devconnected.com/wp-content/uploads/2020/12/pstree.png)

If you see “**systemd**“, it obviously means that you are currently using systemd. However, if you see “**init**“, it means that you are using SysVinit.

On Ubuntu 14.04, that is still using the old init system, your “pstree” may look like this.

![pstree init system](https://devconnected.com/wp-content/uploads/2020/12/pstree-init.png)

## List Services using systemctl

**The easiest way to list services on Linux, when you are on a systemd system, is to use the “systemctl” command followed by “list-units”. You can specify the “–type=service” option in order to restrict the results to services only.**

```
$ systemctl list-units --type=service
```

![list active services on linux](https://devconnected.com/wp-content/uploads/2020/12/list-services-linux-systemd.png)

By default, this command will show you only the services that are active or the services that have failed on your system. In the screenshot above, most of the services are active but the logrotate one (highlighted in red) is marked as failed.

Awesome, you learnt how you can easily **list your services on a Linux server.**

However, as you may have noticed, you did not have access to all services : *what about inactive services? What about services that were not loaded by systemd on boot?*

### List All Services on Linux using list-units

**In order to list all services, meaning active and inactive, you have to use the “systemctl list-units” command followed by the “–all” option.**

Similarly, you can limit the results to services only by using the type filter.

```
$ systemctl list-units --type=service --all
```

![list inactive services linux](https://devconnected.com/wp-content/uploads/2020/12/list-inactive-services.png)

As you can see, inactives services also listed which might be convenient if you just wrote your service and looking after it in the list.

In this case, only loaded services are listed. On boot, systemd loads unit files and it may choose not to load a specific service if it finds that it won’t be used by the system.

As a consequence, there is a real difference between “**loaded**” and “**installed**” services. “**Installed” services mean that unit files can be found in the corresponding paths.**

![service path systemd](https://devconnected.com/wp-content/uploads/2020/12/installed-services.png)

### List Services By State

**In some cases, you may only be interested in services that have failed. For that, you can specify the state that you are looking for as an option of the systemctl command.**

```
$ systemctl list-units --state=<state>

$ systemctl list-units --state=<state1>,<state2>
```

Where “state” can be one of the following values : **active, inactive, activating, deactivating, failed, not-found or dead.**

For example, if we are only interested in “failed” services, we are going to run the following command

```
$ systemctl list-units --state=failed
```

![list failed services on ubuntu](https://devconnected.com/wp-content/uploads/2020/12/failed-service.png)

### List All Service Files using list-unit-files

Finally, if you are interested in “**loaded**“, “**installed**“, “**disabled**” as well as “**enabled**” service files, there is a another command that might be pretty handy.

**In order to list all service files available, you have to use the “systemctl” command followed by “list-unit-files”. Optionally, you can specify the type by using the “–type=service” option.**

```
$ systemctl list-unit-files --type=service
```

![list installed services](https://devconnected.com/wp-content/uploads/2020/12/list-installed-services.png)

Alternatively, you can use the [“grep” command](https://devconnected.com/find-text-in-files-on-linux-using-grep/) in order to search for specific paths on your system that may contain service files.

```
$ ls -l /etc/systemd/system /usr/lib/systemd/service | egrep .service$
```

![](https://devconnected.com/wp-content/uploads/2020/12/list-files-using-grep.png)

Congratulations, you learnt how you can list services if your system is using systemd!

## List Services using service

**The easiest way to list services on Linux, when you are on a SystemV init system, is to use the “service” command followed by “–status-all” option. This way, you will be presented with a complete list of services on your system.**

```
$ service --status-all
```

![listing services on init systems](https://devconnected.com/wp-content/uploads/2020/12/list-services-init-system.png)

As you can see, each service is listed preceded by symbols under brackets. Those symbols mean :

-   **+** : means that the service is **running**;
-   **–** : means that the service is **not running** at all;
-   **?** : means that Ubuntu **was not able to tell** if the service is running or not.

*So why are some services to tell if they are running or not, and some are not able to?*

It all comes down to the implementation of the init script. In some scripts, such as the [udev](https://opensource.com/article/18/11/udev) script for example, you are able to see that the “**status**” command is implemented.

![](https://devconnected.com/wp-content/uploads/2020/12/udev-status.png)

This is not the case for the “**dns-clean**” script for example which is the reason why you have a question mark when you query this service.

### List SysVinit Services in Folders

**Another way of listing the current list of services is to use the “ls” command on the folders containing all scripts on a Linux system, namely “/etc/init.d”.**

```
$ ls -l /etc/init.d/*
```

![listing init scripts](https://devconnected.com/wp-content/uploads/2020/12/initd-folder.png)

## Conclusion

In this tutorial, you learnt how you can **easily list services on a Linux system** whether you are using systemd or SysVinit ones.

If you are interested in creating your own services, we recommend that you have a look at the following resources. They might be really useful in order to correctly achieve that.

-   [Writing a startup script for init systems](https://unix.stackexchange.com/questions/47695/how-to-write-startup-script-for-systemd);
-   [Starting services at boot using systemd](https://www.linode.com/docs/guides/start-service-at-boot/);

If you are interested in **Linux System Administration**, we have a complete section on this subject on the website, so make sure to check it out.

[![](https://devconnected.com/wp-content/uploads/2019/09/100.png)](https://devconnected.com/category/linux-administration/)

Icons made by [Freepik](https://www.flaticon.com/authors/smashicons) from [FlatIcon](https://www.flaticon.com/)