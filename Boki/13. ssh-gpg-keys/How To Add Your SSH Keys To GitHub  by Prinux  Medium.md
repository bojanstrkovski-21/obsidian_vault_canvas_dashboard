---
created: 2024-03-06T11:31:27 (UTC +01:00)
tags: []
source: https://medium.com/@Prinux/how-to-add-your-ssh-keys-to-github-3a63df43c7ce
author: Prinux
---

# How To Add Your SSH Keys To GitHub | by Prinux | Medium

![[1Jy6R0-K80tuVLNwtCiwtqw.png]]
Here’s a guide on how to set SSH keys, for your Windows, Linux and Mac Machines. SSH stands for Secure Shell Protocol, when you connect via SSH, you authenticate using a private key file on your local machine.

## For Windows, Linux and MacOS

For creating new ssh keys, run this command on your terminal

```
<span id="7cdf" data-selectable-paragraph="">ssh-keygen -t ed25519 -C <span>"your_email@example.com"</span></span>
```

Note: If you are using a legacy system that doesn’t support the Ed25519 algorithm, use:

```
<span id="20eb" data-selectable-paragraph="">$ ssh-keygen -t rsa -b <span>4096</span> -C <span>"your_email@example.com"</span></span>
```

When you run this, a prompt will ask you for the file location. Just hit enter as the default option it best one.

After that you are prompted for a passphrase, this is because even if your computer is compromised or your ssh keys have been copied the “bad actor” cannot use them until and unless they know your passphrase, I suggest you to use a good randomly generated password. In case in you don’t want to have a passphrase just hit enter, this will create the keys with a passphrase.

```
<span id="c3b8" data-selectable-paragraph="">&gt; Enter passphrase <span>(</span>empty for no passphrase<span>)</span><span>:</span> <span>[</span><span>Type</span> a passphrase<span>]</span><br>&gt; Enter same passphrase <span>again</span><span>:</span> <span>[</span><span>Type</span> passphrase again<span>]</span></span>
```

For starting the ssh-agent in the background.

```
<span id="c7c8" data-selectable-paragraph=""><span>$ </span>eval "$(ssh-agent -s)"<br><span>&gt; </span>Agent pid 59566</span>
```

Adding your SSH private key to the ssh-agent.

```
<span id="52dd" data-selectable-paragraph="">$ ssh-add ~<span>/.ssh/i</span>d_ed25519</span>
```

This all you need to do for Windows and Linux Operating Systems.

## More Information For macOS Sierra 10.12.2 or later

![](How%20To%20Add%20Your%20SSH%20Keys%20To%20GitHub%20%20by%20Prinux%20%20Medium/0NKUEeMXH8qg62iY0.jpeg)

Photo by [James McKinven](https://unsplash.com/@jmckinven?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

you will need to modify your `~/.ssh/config` file to automatically load keys into the ssh-agent and store passphrases in your keychain.

-   First, check to see if your `~/.ssh/config` file exists in the default location.
-   `$ open ~/.ssh/config > The file /Users/YOU/.ssh/config does not exist.`
-   If the file doesn’t exist, create the file.
-   `$ touch ~/.ssh/config`
-   Open your `~/.ssh/config` file, then modify the file to contain the following lines. If your SSH key file has a different name or path than the example code, modify the filename or path to match your current setup.

```
<span id="a993" data-selectable-paragraph="">Host *.github.com<br>  AddKeysToAgent <span>yes</span><br>  UseKeychain <span>yes</span><br>  IdentityFile ~/.ssh/id_ed25519</span>
```

Add your SSH private key to the ssh-agent and store your passphrase in the keychain.

```
<span id="e5e6" data-selectable-paragraph="">$ ssh-add --apple-use-keychain ~<span>/.ssh/i</span>d_ed25519</span>
```

## Adding Your Keys To GitHub

Now if you open your default location where your ssh keys are saved, you will find two files id\_ed25519, id\_ed25519.pub. You need to copy the contents of the file ending “”.pub.” .

Open your web browser and go to the settings of the GitHub page and click on ssh and GPG keys. Then click on new ssh keys and paste your file contents.

    ![[1_HAAISMyZ-_dAU57u9Pak7w (1).png]] 

The last Step Add SSH keys. Now you have added your ssh keys and are good to go.