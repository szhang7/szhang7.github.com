---
layout: post
title: "ubuntu text editors"
description: "Introduce some text editors used in ubuntu, for example vi and nano editor."
category: ubuntu
tags: [ubuntu, text editor, vi, nano]
---
{% include JB/setup %}

A text editor is a type of program used for editing plain text files.

Here focuses on vi and nano editors.

## vi

vi is a modal editor: it operates in either insert mode or normal mode.

**insert mode**: typed text becomes part of the document.
**normal mode**: keystrokes are interpreted as commands that control the edit session.

### Start vi

    vi filename     # edit filename
    vi -r filename  # recover filename that was being edited when system crashed.

### vi Subcommands

    i   - insert text before cursor, until Esc hit
    a   - append text after cursor, until Esc hit

    r   - replace single character under cursor(no Esc needed)
    R   - replace characters, starting with current cursor position, until Esc hit

    d   - delete single character
    dd  - delete current line

    Ctrl-U 	Scrolls up one-half screen.
    Ctrl-D 	Scrolls down one-half screen.
    Ctrl-F 	Scrolls forward one screen.
    Ctrl-B 	Scrolls backward one screen.

###last-line mode

Subcommands with the prefix:(colon),/(slash),?(question mark),!(exclamation point),or !!(two exclamation points) read input on a line displayed at the bottom of the screen.

Pressing the `Esc (escape key)` switches the editor to `normal mode`.

    :x  - quit vi, writing out modified file.
    :wq - quit vi, writing out modified file.
    :q  - quit vi
    :q! - quit vi even though latest changes have not been saved.

    :r filename - read file and insert after current line
    :w          - write current contents to file
    :w newfile  - write current contents to a new file

## References

- [vi command] (http://pic.dhe.ibm.com/infocenter/powersys/v3r1m5/index.jsp?topic=/iphcg/vi.htm)

- [Basic vi Commands] (http://www.cs.colostate.edu/helpdocs/vi.html)

- [Text editor] (http://en.wikipedia.org/wiki/Text_editor)

- [vi] (http://en.wikipedia.org/wiki/Vi)


