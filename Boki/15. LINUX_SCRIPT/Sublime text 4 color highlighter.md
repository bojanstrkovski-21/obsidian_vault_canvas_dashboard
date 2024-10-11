# [How to get the Color Highlighter package to work](https://stackoverflow.com/questions/40914391/how-to-get-the-color-highlighter-package-to-work)

[Ask Question](https://stackoverflow.com/questions/ask)

Asked 6 years, 2 months ago

Modified [2 years, 1 month ago](https://stackoverflow.com/questions/40914391/how-to-get-the-color-highlighter-package-to-work?lastactivity "2020-12-22 08:04:36Z")

Viewed 8k times

3

[](https://stackoverflow.com/posts/40914391/timeline)

The sublime text package [Color Highlighter](https://packagecontrol.io/packages/Color%20Highlighter) looks quite useful. However, it doesn't seem to behave as described in the docs.

_**According the docs:**_

> **Usage :**
> 
> Just click or move the cursor (or multiple cursors) on the color code e.g. “#FFFFFF” or “rgba(255, 0, 0, 0.7)” or variable with color code value and it'll be highlighted with its real color. "

**Anomalous behaviors:**

-   Nothing happens when I click the color (the gifs in the documentation show highlighting on the fly, which simply isn't occurring).
    
-   I can manually from the dropdown menu get the colors to highlight, but I need to click on the menu again to get it to stop highlighting even if the text is changed.
    

[![enter image description here](https://i.stack.imgur.com/7uaXR.png)](https://i.stack.imgur.com/7uaXR.png)

-   It also appears that the selection of a given highlighting style isn't retained in the menu. Below is how the menu appears after selecting "Filled" previously (no checkmarks as usually appears with other menu items).

[![enter image description here](https://i.stack.imgur.com/yn5KN.png)](https://i.stack.imgur.com/yn5KN.png)

-   Gutter highlighting is also absent.

**Relevant Setup:**

-   imagemagick-6.9.6-5
-   OSX 10.11.6
-   Sublime text 3- Build 3126 (also tried with Build 2221, with same results)

> **NOTE:** Same behavior using Windows 7 with latest install of Sublime Text 3 and Color Highlighter

-   [colors](https://stackoverflow.com/questions/tagged/colors "show questions tagged 'colors'")
-   [package](https://stackoverflow.com/questions/tagged/package "show questions tagged 'package'")
-   [sublimetext2](https://stackoverflow.com/questions/tagged/sublimetext2 "show questions tagged 'sublimetext2'")
-   [sublimetext3](https://stackoverflow.com/questions/tagged/sublimetext3 "show questions tagged 'sublimetext3'")
-   [sublimetext](https://stackoverflow.com/questions/tagged/sublimetext "show questions tagged 'sublimetext'")

[Share](https://stackoverflow.com/q/40914391 "Short permalink to this question")

[Improve this question](https://stackoverflow.com/posts/40914391/edit)install

Follow

[edited Jun 20, 2020 at 9:12](https://stackoverflow.com/posts/40914391/revisions "show all edits to this post")

[

![Community's user avatar](https://www.gravatar.com/avatar/a007be5a61f6aa8f3e85ae2fc18dd66e?s=64&d=identicon&r=PG)

](https://stackoverflow.com/users/-1/community)

[Community](https://stackoverflow.com/users/-1/community)Bot

111 silver badge

asked Dec 1, 2016 at 15:24

[

![Minnow's user avatar](https://i.stack.imgur.com/x30jD.jpg?s=64&g=1)

](https://stackoverflow.com/users/2651663/minnow)

[Minnow](https://stackoverflow.com/users/2651663/minnow)

1,67522 gold badges2626 silver badges4949 bronze badges

[Add a comment](https://stackoverflow.com/questions/40914391/how-to-get-the-color-highlighter-package-to-work# "Use comments to ask for more information or suggest improvements. Avoid answering questions in comments.")

## 1 Answer

Sorted by:

                                              Highest score (default)                                                                   Trending (recent votes count more)                                                                   Date modified (newest first)                                                                   Date created (oldest first)                              

3

[](https://stackoverflow.com/posts/40940956/timeline)

You have not set up the Color Highlighter plugin correctly to find the full path to the `convert` utility from ImageMagick. In Sublime, select **`Preferences → Package Settings → Color Highlighter`** and select both the **`Settings-Default`** and **`Settings-User`** options. Read through the default settings to find all the ways you can customize the plugin. For this case, however, we are only interested in the `"convert_util_path"` option. Open Terminal and enter `which convert` and, if it's on your `$PATH` and has been installed correctly, it should print out its location (perhaps `/usr/local/bin/convert` or something similar. If you can't find it, try making a fresh install of ImageMagick using [the latest version for OS X](https://www.imagemagick.org/script/download.php#macosx). Once you've installed it in the directory of your choice, create a symlink to `convert` by running

```
ln -s /Users/Minnow/Utilities/ImageMagick-7.0.3/bin/convert /usr/local/bin/convert
```

You _may_ need to use `sudo` before that command, I'm not sure how 10.11 is set up. Also, you'll obviously need to replace the `/Users/Minnow/...` path with the real path to your installation directory.

Once you have completed either of the above steps, select the `Color Highlighter.sublime-settings` file in Sublime that was opened when you selected **`Settings-User`** (it may already have stuff in it). Add the following line:

```javascript
"convert_util_path": "/usr/local/bin/convert", // or whatever the path is
```

to the top, after the opening braces `{`. If `"convert_util_path"` is already there, just change its value to the correct path.

Now, save the file, restart Sublime, and you should be good to go. Here are the complete contents of my settings, along with an image of my [Neon Color Scheme](https://packagecontrol.io/packages/Neon%20Color%20Scheme)'s `Neon.tmTheme` file. All the colors have a box of that particular color around them, and when I put my cursor on one of the colors (here it's in `#FF0080` on line 21) a dot shows up in the gutter. (Just FYI, this screenshot was taken on Windows 10, OS X might work differently.)

```javascript
{
    "enabled": true,
    "style": "default",
    "icons": true,
    "ha_style": "filled",
    "icons_all": true,
    "default_keybindings": true,
    "convert_util_path" : "c:/users/mattdmo/bin/convert",
    "color_formats": [
        "white",
        "#FFF", "#FFFF", "#FFFFFF", "#FFFFFFFF",
        "rgb(255, 255, 255)",
        "rgba(255, 255, 255, 1.0)",
        "hsv(0, 0%, 100%)",
        "hsva(0, 0%, 100%, 1.0)",
        "hsl(0, 100%, 100%)",
        "hsla(0, 100%, 100%, 1.0)"
    ],
    "file_exts": [".css", ".sass", ".scss", ".less", ".styl", ".html", ".js", ".tmTheme", ".svg"]
}
```

[![Neon.tmTheme highlighted with Color Highlighter](https://i.stack.imgur.com/UJd0G.png)](https://i.stack.imgur.com/UJd0G.png)

[Share](https://stackoverflow.com/a/40940956 "Short permalink to this answer")

[Improve this answer](https://stackoverflow.com/posts/40940956/edit)

Follow

[edited Dec 22, 2020 at 8:04](https://stackoverflow.com/posts/40940956/revisions "show all edits to this post")

[

![Glorfindel's user avatar](https://i.stack.imgur.com/Haz6W.jpg?s=64&g=1)

](https://stackoverflow.com/users/4751173/glorfindel)

[Glorfindel](https://stackoverflow.com/users/4751173/glorfindel)

21.5k1313 gold badges7878 silver badges105105 bronze badges

answered Dec 2, 2016 at 21:16

[

![MattDMo's user avatar](https://i.stack.imgur.com/7eIWB.png?s=64&g=1)

](https://stackoverflow.com/users/1426065/mattdmo)

[MattDMo](https://stackoverflow.com/users/1426065/mattdmo)

99.4k2121 gold badges238238 silver badges229229 bronze badges

-   Thanks for the effort. The convert error is resolved. However, the main question remains unsolved as the plugin still doesn't recognize text without manually selecting it using the menu. I've made an edit to the last part, which you've fixed. 
    
    – [Minnow](https://stackoverflow.com/users/2651663/minnow "1,675 reputation")
    
     [Dec 3, 2016 at 3:19](https://stackoverflow.com/questions/40914391/how-to-get-the-color-highlighter-package-to-work#comment69098897_40940956)
    
-   This should really be in the package instructions, my installation also did not have this (macOS). Also, the preferences settings defaults did not even contain the `convert_util_path` listed. 
    
    – [Merlin](https://stackoverflow.com/users/2223505/merlin "1,643 reputation")
    
     [Sep 10, 2020 at 21:26](https://stackoverflow.com/questions/40914391/how-to-get-the-color-highlighter-package-to-work#comment112886410_40940956)
    
-   2
    
    @Merlin If you're having issues with `Color Highlighter`, I highly recommend giving [`ColorHelper`](https://packagecontrol.io/packages/ColorHelper) a try. I started using it fairly recently after seeing a comment on Sublime's Discord channel, and I love it. It's really easy to configure which file types you want highlighting for and which you don't, and best of all it doesn't rely on external dependencies like Image Magick. 
    
    – [MattDMo](https://stackoverflow.com/users/1426065/mattdmo "99,384 reputation")
    
     [Sep 13, 2020 at 14:44](https://stackoverflow.com/questions/40914391/how-to-get-the-color-highlighter-package-to-work#comment112946296_40940956)
    
-   1
    
    @MattDMo thank you i will try this and share a joke i heard. In every programmer are two wolves: One wants to get the highlight colors just right, and the other wants to finsh work by five. 
    
    – [Merlin](https://stackoverflow.com/users/2223505/merlin "1,643 reputation")
    
     [Sep 13, 2020 at 15:29](https://stackoverflow.com/questions/40914391/how-to-get-the-color-highlighter-package-to-work#comment112947018_40940956)