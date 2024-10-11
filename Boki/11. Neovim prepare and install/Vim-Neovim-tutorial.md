Vim-Neovim how to tuttorial
========================

# I. Basic Motion Keys

1. Vim motion keys in normal mode

h - move left
j - move down
k - move up
l - move right

2. Arrow keys 
left down up right

3. move trough the document
gg - go to the top start of the document
Shift+g (capital G) - go to the bottom start of the document
G+number (exemple 10G - go to line 10) - go to line number
number+k - move number of lines up
number+j - move number of lines down
number+l - move number of characters to the right
number+h - move number of characters to the left
0 (zero) - go to the begining of the line
$ (Shift+4) - go to the end of the line
^ (Shift+6) - go to the first nonblank character of the line
g_ - go to the last nonblank character of the line
} - go down to the next paragraph
{ - go up to the previous paragraph
Ctrl+d - move down by a half page
Ctrl+u - move up by a half page
w - move at start of the next word
b - move to the previous word
e - move to the the end of the next word
ge - move to the end of the previous word
W - go to the start of the next word and skip punctation marks (, . ; : ' ")
B - go to the start of previous word and skip punctation marks (, . ; : ' ")
E - move to the end of the next word and skip punctation marks (, . ; : ' ")
gE - move to the end of the previous word and skip punctation marks (, . ; : ' ")
% - move to the closing bracket and back to the opening bracket 


# II. Command Mode
: (colon) - which is command mode  

1. Basic commands in command mode
a. :q - quit/exit neovim
b. :w - write/save buffer/document
c. :wq - save and quit neovim
d. :colorscheme and press tab to see all the available colorschemes and select the one you want.

# III. Insert Mode

i - insert mode (before character)
a - insert mode (after character)
A (Shift+a) - go to insert mode on the end of the line
o - go to insert mode on the next line
O (Shift+o) - go to insert mode on the previous line
u - undo
Ctrl+r - redo

# IV. Visual Modes

## A. Visual Line Mode

Shift+v and move up or down to select lines of text

## B. Visual Block Mode

Ctrl+v and move up down left right to select the desired block (area) of text(code).

## C. Search mode
/ - type and press enter to search
n - to go to next result
N (Shift+n) - to go to previous result
? - type and press enter to search from the last result backwards
n - to go to previous result
N (Shift+n) - to go to next result

f+name of character(a 1 ...) - find the next same caracter in the line
t+name of the character character(a 1 ...) - find the character before the next same caracter in the line 
; - go to the next result from f+character(a 1 ...) and the same for t+character(a 1 ...)
, - go to the previous result from f+character(a 1 ...), when press after t+character(a 1 ...) it finds the character after the previous result 

# V. Delete copy paste

dd - delete the line 
p - paste on the next line
P (Shift+p) - paste to the previous line
yy - yank (copy) the line
dG - delete all document text from first to the last line (first type gg to go to the first line)
yG - copy all document text from first to the last line (first type gg to go to the first line)
:%y - yank the whole document
:%d - delete the whole document
x - delete thw character the cursor is on
r+name of character(a b , ; ...) - to replace a character the cursor is on
dw - delete the word the cursor is on
yw - yank the word the cursor is on
d% - delete from the word the cursor is on to the end of the line
d0(zero) - delete from the word the cursor is on to the begining of the line
y% - yank/copy from the word the cursor is on to the end of the line
y0(zero) - yank/copy from the word the cursor is on to the begining of the line
cw - delete and go to insert mode to insert the new word in its place
cc - delete and go to insert mode to insert the entire new line in its place
c% - to go to insert mode to type new text from the word the cursor is on to the end of the line
c0(zero) - to go to insert mode to type new text from the word the cursor is on to the begining of the line
diw - delete the inside of the word the cursor is in the middle of
yiw - yank/copy the inside of the word the cursor is in the middle of
yaw - yank/copy the around of the word the cursor is in the middle of
daw - delete the around of the word the cursor is in the middle of
di[ di{ di( di' di" - delete everything insoide the pair of brackets or quotes



