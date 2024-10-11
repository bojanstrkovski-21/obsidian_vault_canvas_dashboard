# How to Use the rsync Command to Transfer Files (Linux Crash Course Series)

2023-07-06

The rsync command is kind of like a “swiss army knife” of file transfer utilities. With a wealth of options available, it’s easily one of the best methods of moving files around. In this video, Jay goes over the finer points of the rsync command, with an emphasis on the most important options you should know for day-to-day usage.

![YouTube player](https://i.ytimg.com/vi/KG78O53u8rY/maxresdefault.jpg)

Thanks to Akamai for sponsoring today’s video! Check out their [connected cloud](https://learnlinux.link/akamai) platform for your own awesome Linux server!

In this video/article, it’s time for `rsync` to have its turn in the spotlight. This is definitely a fantastic utility that every Linux admin should know! Another episode in this series went over [`scp`](https://www.learnlinux.tv/transferring-files-with-the-scp-command-linux-crash-course-series/), which is another utility you can use to transfer files between servers. And `scp` is great for one-off file transfers. But for anything more advanced than that, `rsync` is the way to go for sure!

## Basic usage

First things first, in order to use `rsync`, we’ll need to make sure that it’s installed:

```
command -v rsync
```

If you receive no output here, then that means you don’t have it installed, but installing it is very straight forward. Just install the `rsync` package with your distribution’s package manager, and that’s it.

## The rsync Command Has Lots of Options

First things first – `rsync` is a utility that has a ridiculous number of options. For that reason, it’s sometimes a bit overwhelming for some people, especially those starting out. But the thing is, you don’t have to learn and memorize every option (in fact, no one ever does). Just focus on the options that pertain to your particular use-case. To make it easier, the most common options will be covered here.

The basic idea behind `rsync` is that you use it to transfer files from one place to another. And it doesn’t really matter what you transfer or even where you transfer it to, so long as you have access to it. You can sync data between local folders on the same system, between remote servers, a local server and a remote server, basically you can sync whatever data you want with whatever target you want, but again, assuming you have permission.

By default, `rsync` uses `ssh` to facilitate file transfers. And this isn’t unlike `scp`, which also uses SSH to facilitate file transfers. But where rsync outshines `scp` is its wealth of options that enable you to scrutinize your file transfers down to the very last detail.

As we start out, let’s see a very simple example of `rsync`:

```
rsync dir1 dir2
```

This is just a pseudo-example, we’ll get to the real stuff shortly. With this hypothetical example, we’re syncing files that exist in the first directory, to the second. These directories can exist on the same server, or perhaps one of the directories is attached to an NFS or Samba file share. It doesn’t really matter so much for `rsync`, you tell it to sync folders and it will.

## Does rsync give you a full sync?

Something important to understand about `rsync` is that it’s not really a sync utility in the way we think of them nowadays. Yes, you can use `rsync` to sync files in both directions to make folders exactly the same, but most examples of `rsync` are going to be syncing in one direction. Today, when we think of a sync utility, we think of something that’s bidirectional. It’s not that you can’t end up with a file sync on both sides, the difference is that `rsync` is primarily used to sync one direction at a time. Full synchronization solutions, such as [Syncthing](https://www.learnlinux.tv/syncing-your-files-across-all-your-computers-via-syncthing/), are better choices for bi-directional syncs.

In the above example, if there’s files inside directory 2 that are not inside of directory 1, those files will remain, and the files in directory 1 will be copied into directory 2. So basically, directory 2 will have all of its own contents, along with a copy of the data in directory 1 after `rsync` runs.

But of course, there’s ways to tweak this to make `rsync` do different things, which we’ll see shortly. For now, let’s start with an actual example of using `rsync` to sync data.

## First, Verify Permissions/Access

Since `rsync` uses OpenSSH by default to transfer files, you should verify you have access to the target server and that you have read/write access to the target directory. The `rsync` command is only as capable as your user’s permissions, so one way you can test this is to simply log in to the target server and attempt to write some sort of information to the directory that you want to sync to. That will help you rule out permissions as a potential barricade.

## Always use the “Dry Run” Option First - simulate a transfer to see if it will work

Here’s the first (usable) example of `rsync` in action. Just like before, we call `rsync` and then give it one or more options. Here, we’re adding `--dry-run` which triggers a “demo mode” that simulates a transfer, but doesn’t actually perform one:

```
rsync --dry-run notes jay@backup-server:/home/jay/backups
```

The reason why I’m explaining this option first is because it’s a very important option to know. You should never run `rsync` without testing the command first. I’ve been using Linux for decades and even I still make mistakes. We all do. With the `--dry-run` option, we can make sure that `rsync` is going to do what we think it will. If we don’t use `--dry-run` first, we might overwrite or purge something we didn’t intend to.

After using the `--dry-run` option, and verifying from its output that it’s going to do what you think it will, we can remove the option to have `rsync` run for real:

```
rsync notes jay@backup-server:/home/jay/backups
```

And now, all of the notes I have in the source directory are copied over to the target. This also works in reverse as well. For example:

```
rsync jay@backup-server:/home/jay/backups notes
```

And with that command, I’m able to use `rsync` in the opposite direction!

## The rsync Command Doesn’t Sync Deletes by Default

One potential “gotcha” around `rsync` is that if you delete a file in the source directory and then sync, the fact that the file is missing will not be synchronized to the target. If you do want to remove files from the target that you’ve deleted at the source, add the `--delete` option:

```
rsync --delete notes jay@backup-server:/home/jay/backups
```

With this command, files that are not found here locally will be removed from the target, to try and make the contents the same on both sides. This is basically the closest thing to a true sync in `rsync` that we’ll have without doing something more advanced. If I saved a brand new file on the target, that file will not be synced – literally anything present in the target not present at the source will be removed with this option. Again, it’s a one way sync.

Before running this though, be sure to try with `--dry-run first` – since we’re adding the `--delete` option, this is potentially dangerous as a typo may cause us to remove something we didn’t intend to.

## Archive Mode is a Great Option to Remember

Archive mode is activated by adding the `-a` option to `rsync`:

```
rsync -a --delete notes jay@backup-server:/home/jay/backups
```

What archive mode will do, is sync file metadata in addition to the files themselves. For example, modification date, permissions, owner, things like that. This option makes the data even more of a match than before.

In addition to that, I’ll add a few more options as well:

```
rsync -avz --delete notes jay@backup-server:/home/jay/backups
```

In addition to `-a` for archive mode, I added options `-v` and `-z` as well, and I combined them all together under one hyphen.

The `-v` option is verbose, it will list the files that `rsync` is copying as it copies them.

The `-z` option on the other hand is something you may or may not want to include, depending on the situation. What this option does is compress data during transfer. This is useful if you’re syncing data over a slow connection. By compressing data first, there’s less data to send over the wire, so that can definitely help in that situation. However, if you have a fast or at least reasonable connection between the source and target, it’s probably better to leave that option out since you’d be compressing data for no real gain.

## Moving Files (instead of Syncing) with rsync

So what if you wanted to perform a one off file transfer, and also remove the source files? You can do that with `rsync`, and this variation makes the transaction more of a “move” instead of a sync:

```
rsync --remove-source-files notes jay@backup-server:/home/jay/backups
```

Now be very careful with this command, because it will absolutely remove data from the source at least. Again, the dry run option is your friend here as that can help you simulate file transfers before running them.

Anyway, with this option, we’re telling `rsync` to delete files at the source after they’ve been copied over to the target. So again, this is more of a “move” than a sync.

And that’s about it for this introduction on `rsync`! There’s definitely more to come so bookmark this site and stay tuned for more Linux-related goodness!