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

### References

- [vi command] (http://pic.dhe.ibm.com/infocenter/powersys/v3r1m5/index.jsp?topic=/iphcg/vi.htm)

- [Basic vi Commands] (http://www.cs.colostate.edu/helpdocs/vi.html)

- [Text editor] (http://en.wikipedia.org/wiki/Text_editor)

- [vi] (http://en.wikipedia.org/wiki/Vi)

##SciTE

    $ sudo apt-get install scite
    $ wget http://scite-files.googlecode.com/svn-history/trunk/translations/locale.zh_cn.properties

SciTE User Options File: ~/.SciTEUser.properties

    # 修改所有的字体为微软雅黑，如果希望修改为其它字体，只需要修改default.font.name即可    
    default.font.name=font:!Microsoft YaHei
    font.base=$(default.font.name),size:11
    font.small=$(default.font.name),size:10
    font.comment=$(default.font.name),size:11
    font.code.comment.box=$(font.comment)
    font.code.comment.line=$(font.comment)
    font.code.comment.doc=$(font.comment)
    font.code.comment.nested=$(font.comment)
    font.text=$(default.font.name),size:10
    font.text.comment=$(default.font.name),size:9
    font.embedded.base=$(default.font.name),size:9
    font.embedded.comment=$(default.font.name),size:9
    font.monospace=$(default.font.name),size:11
    font.vbs=$(default.font.name),size:9    

    # 修改打开文件窗口的文件过滤器为“全部文件”
    if PLAT_WIN
        all.files=All Files (*.*)|*.*|
        top.filters=$(all.files)|All Source
    if PLAT_GTK
        all.files=All Files (*)|*|Hidden Files (.*)|.*|
        top.filters=$(all.files)|All Source
    if PLAT_MAC
        all.files=All Files (*.*)|*.*|
        top.filters=$(all.files)All Source

    # 打开SciTE时默认全屏
    position.maximize=0

    # 默认显示工具条
    toolbar.visible=1

    # 让scite工具条使用gnome当前主题提供的图标
    toolbar.usestockicons=1

    # 默认显示状态栏
    statusbar.visible=1

    #在窗口标题栏显示当前文件的全路径文件名称
    title.full.path=1

    # 默认显示行号
    line.margin.visible=1
    # 行号至少占用的宽度
    line.margin.width=2+

    # 高亮当前选中的单词
    highlight.current.word=1
    # 设置高亮单词的颜色
    highlight.current.word.colour=#FF0000

    # 当前文件被外部程序修改时自动载入
    load.on.activate=1
    # 自动重新载入前询问
    are.you.sure.on.reload=1

    # 在已运行的SciTE中打开新文件
    check.if.already.open=1

    # 保存最近打开的文件列表
    save.recent=1

    # 打开SciTE时自动打开上次退出时没有关闭的所有文件
    save.session=1

    # 设置tab size 为 4个空格的大小
    tabsize=4
    # 设置缩进的大小为4个空格的大小，可以和tabsize不同
    indent.size=4
    #缩进时使用空格代替tab，如果设置为1则是空格和tab混合。
    use.tabs=0

    # 打开编辑窗格自动换行
    wrap=1
    # 按字进行换行（更适合亚洲语言）。如果设置为1则是按单词进行换行。
    wrap.style=2
    # 打开输出窗格自动换行
    output.wrap=1

    # 开启单词自动补全
    autocompleteword.automatic=1

    # 打开文件时自动检测编码
    command.discover.properties=python ~/.SciTEFileDetect.py "$(FilePath)"
        
    # xml、html自动闭合括号
    xml.auto.close.tags=1

Use .SciTEFileDetect.py to detect automatically file encoding.

    # Detect file encoding
    # Simple method that just chacks that first 1000 lines are valid in each encoding
    # and chooses first from set that is valid for all lines checked.
    # A better version would allow for a small proportion of failures and rank encodings
    # depending on how well they match the input.
    import sys
    import os

    encodings = [
        ['utf-8', 65001, 0],
        ['cp932', 932, 128],
        ['cp936', 936, 134],
        ['cp949', 949, 129],
        ['cp950', 950, 136],
    ]

    codings = [e[0] for e in encodings]

    def EncodingWorks(encoding, text):
        try:
            text.decode(encoding)
            return True
        except UnicodeDecodeError:
            return False
        
    # Read up to first 1000 lines of file
    if len(sys.argv) > 1 and os.path.isfile(sys.argv[1]):
        with open(sys.argv[1], "rb") as f:
            lineNumber = 1
            for line in f.readlines():
                # Filter out any encodings that fail
                codings = [c for c in codings if EncodingWorks(c, line)]
                lineNumber += 1
                if lineNumber > 1000:
                    break

    comment = ''
    for c in codings:
        for e in encodings:
            if e[0] == c:
                codePage, characterSet = e[1:]
                if codePage:
                    print('%scode.page=%s' % (comment, codePage))
                if characterSet:
                    print('%scharacter.set=%s' % (comment, characterSet))
                # Display other matches as comments so can check results
                comment = '#'

    # Change the caret colour so we can see that something happened
    print('caret.fore=#4499FF')

(Read more: <http://www.cnblogs.com/meetrice/archive/2013/02/15/2912790.html>)
