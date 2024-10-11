# Vim cheatsheet

A useful collection of [Vim](http://www.vim.org/) 8.2 quick reference cheat sheets to help you learn vim editor faster.

## [#](https://quickref.me/vim.html#getting-started)Getting Started

### Motion Diagrams

```bash
▼/▶ Cursor   ▽/▷ Target
```

#### Left-right motions

```bash
┌───────────── |      
├───────────── 0      $ ──────────────┐ 
│  ┌────────── ^      fe ────────┐    │
│  │  ┌─────── Fo     te ───────┐│    │
│  │  │┌────── To     30| ───┐  ││    │
│  │  ││ ┌──── ge     w ───┐ │  ││    │
│  │  ││ │ ┌── b      e ─┐ │ │  ││    │
│  │  ││ │ │  ┌h      l┐ │ │ │  ││    │
▽  ▽  ▽▽ ▽ ▽  ▽▼      ▼▽ ▽ ▽ ▽  ▽▽    ▽
   echo "A cheatsheet from quickref.me"
```

#### Up-down motions

```bash
                 - SCREEN 1 START
   ┌─┬─────────▷ #!/usr/bin/python
   │ │     ┌───▷     
   │ │     │     print("Hello")
   │ │     { } ▶ print("Vim")
   │ │       │   print("!")
   │ │       └─▷    
   │ │ ┌───┬───▷ print("Welcome")
G gg H M L k j ▶ print("to")
│        │   └─▷ print("quickref.me")
│        │       print("/vim")
│        │     
│        └─────▷ 
│                - SCREEN 1 END
└──────────────▷ print("SCREEN 2")
```

### Motions

|   |   |
|---|---|
|`h` _\|_ `j` _\|_ `k` _\|_ `l`|Arrow keys|
|`<C-u>` _/_ `<C-d>`|Half-page up/down|
|`<C-b>` _/_ `<C-f>`|Page up/down|

#### Words

|   |   |
|---|---|
|`b` _/_ `w`|Previous/Next word|
|`ge` _/_ `e`|Previous/Next end of word|

#### Line

|   |   |
|---|---|
|`0` _(zero)_ _/_ `$`|Start/End of line|
|`^`|Start of line _(non-blank)_|

#### Character

|   |   |
|---|---|
|`Fe` _/_ `fe`|Move to previous/next `e`|
|`To` _/_ `to`|Move before/after previous/next `o`|
|`\|` _/_ `n\|`|Go to first/`n`th column|

#### Document

|   |   |
|---|---|
|`gg` _/_ `G`|First/Last line|
|`:n` _\|_ `nG`|Go to line `n`|
|`}` _/_ `{`|Next/Previous empty line|

#### Window

|   |   |
|---|---|
|`H` _/_ `M` _/_ `L`|Top/Middle/Bottom screen|
|`zt` _/_ `zz` _/_ `zb`|Top/Center/Bottom this line|

### Insert Mode

|   |   |
|---|---|
|`i` _/_ `a`|Insert before/after cursor|
|`I` _/_ `A`|Insert start/end of line|
|`o` _/_ `O` _(letter)_|Insert new line below/above|
|`s` _/_ `S`|Delete char/line and insert|
|`C` _/_ `cc`|Change to end of/current line|
|`gi`|Insert at last insert point|
|`Esc` _\|_ `<C-[>`|Exit insert mode|

### Saving and Exiting

|   |   |
|---|---|
|`:w`|Save|
|`:q`|Close file|
|`:wq` _\|_ `:x` _\|_ `ZZ`|Save and quit|
|`:wqa`|Save and quit all files|
|`:q!` _\|_ `ZQ`|Force quit|
|`:qa`|Close all files|
|`:qa!`|Force quit all files|
|`:w` now.txt|Write to `now.txt`|
|`:sav` new.txt|Save and edit `new.txt`|
|`:w` !sudo tee %|Write to readonly file|

### Normal Mode

|   |   |
|---|---|
|`r`|Replace one character|
|`R`|Enter Replace mode|
|`u` _/_ `3u`|Undo changes `1` / `3` times|
|`U`|Undo changes on one line|
|`J`|Join with next line|
|`<C-r>` _/_ 5 `<C-r>`|Redo changes `1` / `5` times|

### Cut and paste

|   |   |
|---|---|
|`x`|Delete character _(Cut)_|
|`p` _/_ `P`|Paste after/before|
|`xp`|Swap two characters|
|`D`|Delete to end of line _(Cut)_|
|`dw`|Delete word _(Cut)_|
|`dd`|Delete line _(Cut)_|
|`ddp`|Swap two lines|
|`yy`|Yank line _(Copy)_|
|`"*p` _\|_ `"+p`|Paste from system clipboard|
|`"*y` _\|_ `"+y`|Paste to system clipboard|

#### In visual mode

|   |   |
|---|---|
|`d` _\|_ `x`|Delete selection _(Cut)_|
|`s`|Replace selection|
|`y`|Yank selection _(Copy)_|

### Repeating

|   |   |
|---|---|
|`.`|Repeat last command|
|`;`|Repeat latest `f`, `t`, `F` or `T`|
|`,`|Repeat latest `f`, `t`, `F` or `T` reversed|
|`&`|Repeat last `:s`|
|`@:`|Repeat a command-line command|

### Visual mode

|   |   |
|---|---|
|`v`|Enter visual mode|
|`V`|Enter visual line mode|
|`<C-v>`|Enter visual block mode|
|`ggVG`|Select all text|
|`>` _/_ `<`|Shift text right/left|

### Macros

|   |   |
|---|---|
|`qi`|Record macro `i`|
|`q`|Stop recording macro|
|`@i`|Run macro `i`|
|`7@i`|Run macro `i` 7 times|
|`@@`|Repeat last macro|

You can save macro for any letters not just `i`

## [#](https://quickref.me/vim.html#vim-operators)Vim Operators

### Usage

|   |   |
|---|---|
|`d`|w|
|Operator|Motion|

Combine [operators](https://quickref.me/vim.html#available-operators) with [motions](https://quickref.me/vim.html#motions) to use them

### Available Operators

|   |   |
|---|---|
|`d`|Delete|
|`y`|Yank _(copy)_|
|`c`|Change _(delete then insert)_|
|`p`|Paste|
|`=`|Formats code|
|`g~`|Toggle case|
|`gU`|Uppercase|
|`gu`|Lowercase|
|`>`|Indent right|
|`<`|Indent left|
|`!`|Filter through external program|

### Examples

|Combination|Description|
|---|---|
|`d`d|Delete current line|
|`d`j|Delete two lines|
|`d`w|Delete to next word|
|`d`b|Delete to beginning of word|
|`d`fa|Delete until `a` char|
|`d`/hello|Delete until `hello`|
|`c`c|Change current line, synonym with `S`|
|`y`y|Copy current line|
|`>`j|Indent 2 lines|
|gg`d`G|Delete a complete document|
|gg`=`G|Indent a complete document|
|gg`y`G|Copy a whole document|

### Counts

```
[count] <operator> <motion>
<operator> [count] <motion>
```

---

|   |   |
|---|---|
|2`d`d|Delete `2` lines|
|6`y`y|Copy `6` lines|
|`d`3w|Delete `3` words|
|`d`5j|Delete `5` lines downwards|
|`>`4k|Indent `4` lines upwards|

## [#](https://quickref.me/vim.html#vim-text-objects)Vim Text objects

### Usage

|   |   |   |
|---|---|---|
|`v`|i _/_ a|p|
|Operator|inner _/_ around|Text object|

Operate with an [operator](https://quickref.me/vim.html#available-operators) inner or around text blocks

### Text objects

|   |   |
|---|---|
|p|Paragraph|
|w|Word|
|W|WORD  <br>_(surrounded by whitespace)_|
|s|Sentence|
|[ ( { <|A [], (), or {} block|
|] ) } >|A [], (), or {} block|
|' " `|A quoted string|
|b|A block [(|
|B|A block in [{|
|t|A HTML tag block|

See `:help text-objects`

### Delete

|   |   |
|---|---|
|`d`iw|Delete inner word|
|`d`is|Delete inner sentence|
|`d`i"|Delete in quotes|
|`d`a"|Delete in quotes _(including quotes)_|
|`d`ip|Delete a paragraph|

### Selections

|   |   |
|---|---|
|`v`i"|Select inner quotes "`...`"|
|`v`a"|Select quotes `"..."`|
|`v`i[|Select inner brackets [`...`]|
|`v`a[|Select brackets `[...]`|
|`v`iw|Select inner word|
|`v`ip|Select inner paragraph|
|`v`ipip|Select more paragraph|

### Misc

|   |   |
|---|---|
|`c`iw|Change inner word|
|`c`i"|Change inner quotes|
|`c`it|Change inner tags (HTML)|
|`c`ip|Change inner paragraph|
|`y`ip|Yank inner paragraph|
|`y`ap|Yank paragraph _(including newline)_|

## [#](https://quickref.me/vim.html#vim-multiple-files)Vim Multiple files

### Buffers

|   |   |
|---|---|
|`:e file`|Edit a file in a new buffer|
|`:bn`|Go to the next buffer|
|`:bp`|Go to the previous buffer|
|`:bd`|Remove file from buffer list|
|`:b 5`|Open buffer #5|
|`:b file`|Go to a buffer by file|
|`:ls`|List all open buffers|
|`:sp file`|Open and split window|
|`:vs file`|Open and vertically split window|
|`:hid`|Hide this buffer|
|`:wn`|Write file and move to next|
|`:tab ba`|Edit all buffers as tabs|

### Windows

|   |   |
|---|---|
|`<C-w>` `s`|Split window|
|`<C-w>` `v`|Split window vertically|
|`<C-w>` `w`|Switch windows|
|`<C-w>` `q`|Quit a window|
|`<C-w>` `T`|Break out into a new tab|
|`<C-w>` `x`|Swap current with next|
|`<C-w>` `-` _/_ `+`|Decrease/Increase height|
|`<C-w>` `<` _/_ `>`|Decrease/Increase width|
|`<C-w>` `\|`|Max out the width|
|`<C-w>` `=`|Equally high and wide|
|`<C-w>` `h` _/_ `l`|Go to the left/right window|
|`<C-w>` `j` _/_ `k`|Go to the up/down window|

### Tabs

|   |   |
|---|---|
|`:tabe [file]`|Edit file in a new tab|
|`:tabf [file]`|Open if exists in new tab|
|`:tabc`|Close current tab|
|`:tabo`|Close other tabs|
|`:tabs`|List all tabs|
|`:tabr`|Go to first tab|
|`:tabl`|Go to last tab|
|`:tabm 0`|Move to position `0`|
|`:tabn`|Go to next tab|
|`:tabp`|Go to previous tab|

#### Normal mode

|   |   |
|---|---|
|`gt`|Go to next tab|
|`gT`|Go to previous tab|
|`2gt`|Go to tab number `2`|

## [#](https://quickref.me/vim.html#vim-search-and-replace)Vim Search and Replace

### Search

|   |   |
|---|---|
|`/foo`|Search forward|
|`/foo\c`|Search forward _(case insensitive)_|
|`?foo`|Search backward|
|`/\v\d+`|Search with [regex](https://quickref.me/regex)|
|`n`|Next matching search pattern|
|`N`|Previous match|
|`*`|Search for current word forward|
|`#`|Search for current word backward|

### Replace LINE

```vim
:[range]s/{pattern}/{str}/[flags]
```

---

|   |   |
|---|---|
|`:s/old/new`|Replace first|
|`:s/old/new/g`|Replace all|
|`:s/\vold/new/g`|Replace all with [regex](https://quickref.me/regex)|
|`:s/old/new/gc`|replace all _(Confirm)_|
|`:s/old/new/i`|Ignore case replace first|
|`:2,6s/old/new/g`|Replace between lines `2`-`6`|

### Replace FILE

```vim
:%s/{pattern}/{str}/[flags]
```

---

|   |   |
|---|---|
|`:%s/old/new`|Replace first|
|`:%s/old/new/g`|Replace all|
|`:%s/old/new/gc`|Replace all _(Confirm)_|
|`:%s/old/new/gi`|Replace all _(ignore case)_|
|`:%s/\vold/new/g`|Replace all with [regex](https://quickref.me/regex)|

### Ranges

|   |   |
|---|---|
|`%`|Entire file|
|`’<,’>`|Current selection|
|`5`|Line `5`|
|`5,10`|Lines `5` to `10`|
|`$`|Last line|
|`2,$`|Lines `2` to Last|
|`.`|Current line|
|`,3`|Next `3` lines|
|`-3,`|Forward `3` lines|

### Global command

```vim
:[range]g/{pattern}/[command]
```

---

|   |   |
|---|---|
|`:g/foo/d`|Delete lines containing `foo`|
|`:g!/foo/d`|Delete lines not containing `foo`|
|`:g/^\s*$/d`|Delete all blank lines|
|`:g/foo/t$`|Copy lines containing `foo` to EOF|
|`:g/foo/m$`|Move lines containing `foo` to EOF|
|`:g/^/m0`|Reverse a file|
|`:g/^/t.`|Duplicate every line|

### Inverse :g

```vim
:[range]v/{pattern}/[command]
```

---

|   |   |
|---|---|
|`:v/foo/d`|Delete lines not containing `foo`  <br>_(also `:g!/foo/d`)_|

### Flags

|   |   |
|---|---|
|`g`|Replace all occurrences|
|`i`|Ignore case|
|`I`|Don't ignore case|
|`c`|Confirm each substitution|

### Substitute expression (magic)

|   |   |
|---|---|
|`&` _\|_ `\0`|Replace with the whole matched|
|`\1`...`\9`|Replace with the group 0-9|
|`\u`|Uppercase next letter|
|`\U`|Uppercase following characters|
|`\l`|Lowercase next letter|
|`\L`|Lowercase following characters|
|`\e`|End of `\u`, `\U`, `\l` and `\L`|
|`\E`|End of `\u`, `\U`, `\l` and `\L`|

### Examples

```c
:s/a\|b/xxx\0xxx/g		         # Modifies "a b"      to "xxxaxxx xxxbxxx"
:s/test/\U& file/                # Modifies "test"     to "TEST FILE"
:s/\(test\)/\U\1\e file/         # Modifies "test"     to "TEST file"
:s/\v([abc])([efg])/\2\1/g	     # Modifies "af fa bg" to "fa fa gb"
:s/\v\w+/\u\0/g		             # Modifies "bla bla"  to "Bla Bla"
:s/\v([ab])|([cd])/\1x/g         # Modifies "a b c d"  to "ax bx x x"
:%s/.*/\L&/                      # Modifies "HTML"     to "html"
:s/\v<(.)(\w*)/\u\1\L\2/g        # Make every first letter of a word uppercase
:%s/^\(.*\)\n\1/\1/              # Remove duplicate lines
:%s/<\/\=\(\w\+\)\>/\U&/g        # Convert HTML-Tags to uppercase
:g/^pattern/s/$/mytext           # Find and append text to the end
:g/pattern/norm! @i              # Run a macro on matching lines
/^\(.*\)\(\r\?\n\1\)\+$          # View the duplicates lines
/\v^(.*)(\r?\n\1)+$              # View the duplicates lines (very magic)
:v/./,/./-j                      # Compress blank lines into a blank line
:g/<p1>/,/<p2>/d                 # Delete inclusively from <p1> to <p2>
```

## [#](https://quickref.me/vim.html#vimdiff)Vimdiff

### Usage

```shell

$ vimdiff file1 file2 [file3]
$ vim -d file1 file2 [file3]
```

### Editing

```
:[range]diffget [bufspec]
:[range]diffput [bufspec]
```

---

|   |   |
|---|---|
|`do` _/_ `:diffget`|Obtain (get) difference|
|`dp` _/_ `:diffput`|Put difference|
|`:dif`|Re-scan differences|
|`:diffo`|Switch off diff mode|
|`:1,$+1diffget`|Get all differences|
|`ZQ`|Quit without changes|

See: [Ranges](https://quickref.me/vim.html#ranges)

### Folds

|   |   |
|---|---|
|`zo` _/_ `zO`|Open|
|`zc` _/_ `zC`|Close|
|`za` _/_ `zA`|Toggle|
|`zv`|Open folds for this line|
|`zM`|Close all|
|`zR`|Open all|
|`zm`|Fold more _(foldlevel += 1)_|
|`zr`|Fold less _(foldlevel -= 1)_|
|`zx`|Update folds|

### Jumping

  

|   |   |
|---|---|
|`]c`|Next difference|
|`[c`|Previous difference|

## [#](https://quickref.me/vim.html#miscellaneous)Miscellaneous

### Case

|   |   |
|---|---|
|`vU`|_Uppercase_ character|
|`vu`|_Lowercase_ character|
|`~`|_Toggle case_ character|
|`viw` `U`|_Uppercase_ word|
|`viw` `u`|_Lowercase_ word|
|`viw` `~`|_Toggle case_ word|
|`VU` _/_ `gUU`|_Uppercase_ line|
|`Vu` _/_ `guu`|_Lowercase_ line|
|`V~` _/_ `g~~`|_Toggle case_ line|
|`gggUG`|_Uppercase_ all text|
|`ggguG`|_Lowercase_ all text|
|`ggg~G`|_Toggle case_ all text|

### Jumping

|   |   |
|---|---|
|`<C-o>`|Go back to previous|
|`<C-i>`|Go forward|
|`gf`|Go to file in cursor|
|`ga`|Display hex, ascii value|

### Misc command-lines

|   |   |
|---|---|
|`:h`|Help open help view|
|`:edit!`|Reload current file|
|`:2,8m0`|Move lines `2`-`8` to `0`|
|`:noh`|Clear search highlights|
|`:sort`|Sort lines|
|`:ter`|Open a terminal window|
|`:set paste`|Enable Insert Paste sub-mode|
|`:set nopaste`|disable Insert Paste sub-mode|
|`:cq`|Exiting with an error  <br>_(aborting Git)_|

### Navigating

|   |   |
|---|---|
|`%`|Nearest/matching `{[()]}`|
|`[(` _\|_ `[{`|Previous `(` or `{`|
|`])` _\|_ `]{`|Next `)` or `}`|
|`[m`|Previous method start|
|`[M`|Previous method end|

### Counters

|   |   |
|---|---|
|`<C-a>`|Increase number|
|`<C-x>`|Decrease number|

### Tags

|   |   |
|---|---|
|`:tag Classname`|Jump to first definition of Classname|
|`<C-]>`|Jump to definition|
|`g]`|See all definitions|
|`<C-t>`|Go back to last tag|
|`<C-o> <C-i>`|Back/forward|
|`:tselect Classname`|Find definitions of Classname|
|`:tjump Classname`|Find definitions of Classname (auto-select 1st)|

### Formatting

|   |   |
|---|---|
|`:ce 8`|Center lines between `8` columns|
|`:ri 4`|Right-align lines at `4` columns|
|`:le`|Left-align lines|

See `:help formatting`

### Marks

|   |   |
|---|---|
|`` `^ ``|Last position of cursor in insert mode|
|`` `. ``|Last change in current buffer|
|`` `" ``|Last exited current buffer|
|`` `0 ``|In last file edited|
|`''`|Back to line in current buffer where jumped from|
|` `` `|Back to position in current buffer where jumped from|
|`` `[ ``|To beginning of previously changed or yanked text|
|`` `] ``|To end of previously changed or yanked text|
|`` `< ``|To beginning of last visual selection|
|`` `> ``|To end of last visual selection|
|`ma`|Mark this cursor position as `a`|
|`` `a ``|Jump to the cursor position `a`|
|`'a`|Jump to the beginning of the line with position `a`|
|`d'a`|Delete from current line to line of mark `a`|
|``d`a``|Delete from current position to position of mark `a`|
|`c'a`|Change text from current line to line of `a`|
|``y`a``|Yank text from current position to position of `a`|
|`:marks`|List all current marks|
|`:delm a`|Delete mark `a`|
|`:delm a-d`|Delete marks `a`, `b`, `c`, `d`|
|`:delm abc`|Delete marks `a`, `b`, `c`|

### Calculator

|   |   |
|---|---|
|`<C-r>` `=` 7*7|Shows the result|
|`<C-r>` `=` 10/2|Shows the result|

Do this in INSERT mode

### Shell

|   |   |
|---|---|
|`:!<shell>`|Interpret Shell Command|
|`:r!<shell>`|Read in output of shell|
|`:r!date`|Insert date|
|`:!!date`|Replace current line with date|

### Command line

|   |   |
|---|---|
|`<C-r><C-w>`|Insert current word into the command line|
|`<C-r>"`|Paste from " register|
|`<C-x><C-f>`|Auto-completion of path in insert mode|

### Tricks

Remove duplicate lines

```shell
:sort | %!uniq -u
```

To number the lines in the file

```shell
:%!cat -n
```

Copy whole doc to clipboard

```shell
:%w !pbcopy            # Mac OS X
:%w !xclip -i -sel c   # GNU/Linux
:%w !xsel -i -b        # GNU/Linux
```

