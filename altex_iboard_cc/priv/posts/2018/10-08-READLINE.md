%{
  title: "Command Line Pro Tip",
  date: "Mon Oct  8 18:58:44 CEST 2018",
  tags: ["andi", "2018", "util", "dev"]
}
---
Did you know that almost any shell uses the READLINE library?
If using the command-line is part of your daily work you really should read 
[Gnu Software Manual - Readline](https://www.gnu.org/software/bash/manual/html_node/Readline-Interaction.html#Readline-Interaction) and get comfortable with it's keys ;-)

Even setting an editor (`export EDITOR=vim` for example) is possible. Set that you can use Alt-E to edit the current input line of your terminal within your editor.

## Most important keys

### Movement

    C-a
    Move to the start of the line.

    C-e
    Move to the end of the line.

    M-f
    Move forward a word, where a word is composed of letters and digits.

    M-b
    Move backward a word.

    C-l
    Clear the screen, reprinting the current line at the top.

### Editing

    C-k
    Kill the text from the current cursor position to the end of the line.

    M-d
    Kill from the cursor to the end of the current word, or, if between words, to the end of the next word. Word boundaries are the same as those used by M-f.

    M-DEL
    Kill from the cursor the start of the current word, or, if between words, to the start of the previous word. Word boundaries are the same as those used by M-b.

    C-w
    Kill from the cursor to the previous whitespace. This is different than M-DEL because the word boundaries differ.

    Here is how to yank the text back into the line. Yanking means to copy the most-recently-killed text from the kill buffer.

    C-y
    Yank the most recently killed text back into the buffer at the cursor.

    M-y
    Rotate the kill-ring, and yank the new top. You can only do this if the prior command is C-y or M-y.


## BASH Cheat Sheet

2021-12-23, As suggested by Marc Wilson, take a look at the 
[BASH Cheat Sheet](https://www.pcwdld.com/bash-cheat-sheet)
