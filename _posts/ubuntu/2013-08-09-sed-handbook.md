---
layout: post
title: "Sed Handbook"
description: "Sed Handbook"
category: ubuntu
tags: [sed, handbook, ubuntu, shell]
---
{% include JB/setup %}

## Introduction
sed is a stream editor. A stream editor is used to perform basic text transformations on an input stream (a file or input from a pipeline). While in some ways similar to an editor which permits scripted edits (such as ed), sed works by making only one pass over the input(s), and is consequently more efficient. But it is sed's ability to filter text in a pipeline which particularly distinguishes it from other types of editors.

## Invocation

    sed OPTIONS... [SCRIPT] [INPUTFILE...]
    sed OPTIONS... -f scriptfile [INPUTFILE...]

###options
    -e script, --expression=script
        add the script to the commands to be executed
    -f script-file, --file=script-file
        add the contents of script-file to the commands to be executed
    -h, --help
        display this help and exit
    -i[SUFFIX], --in-place[=SUFFIX]
        edit files in place (makes backup if extension supplied)
    -l N, --line-length=N
        specify the desired line-wrap length for the `l' command
    -n, --quiet, --silent
        suppress automatic printing of pattern space
    -r, --regexp-extended
        use extended regular expressions in the script.
    -V, --version
        output version information and exit

## sed programs

###How sed works
    sed maintains two data buffers: the active pattern space, and the auxiliary hold space. Both are initially empty.

    sed operates by performing the following cycle on each line of input: first, sed reads one line from the input stream, removes any trailing newline, and places it in the pattern space. Then commands are executed; each command can have an address associated to it: addresses are a kind of condition code, and a command is only executed if the condition is verified before the command is to be executed.

    When the end of the script is reached, unless the -n option is in use, the contents of pattern space are printed out to the output stream, adding back the trailing newline if it was removed.3 Then the next cycle starts for the next input line.

    Unless special commands (like ‘D’) are used, the pattern space is deleted between two cycles. The hold space, on the other hand, keeps its data between cycles (see commands ‘h’, ‘H’, ‘x’, ‘g’, ‘G’ to move data between both buffers). 

###Selecting lines with sed
Addresses in a sed script can be in any of the following forms:

    number
        Specifying a line number will match only that line in the input. (Note that sed counts lines continuously across all input files unless -i or -s options are specified.)
    $
        This address matches the last line of the last file of input, or the last line of each file when the -i or -s options are specified.
    /regexp/
        This will select any line which matches the regular expression regexp. If regexp itself includes any / characters, each must be escaped by a backslash (\).
        The empty regular expression ‘//’ repeats the last regular expression match (the same holds if the empty regular expression is passed to the s command). Note that modifiers to regular expressions are evaluated when the regular expression is compiled, thus it is invalid to specify them together with the empty regular expression. 

###Overview of regular expression syntax
    ^
        Matches the null string at beginning of the pattern space.
    $
        It is the same as ^, but refers to end of pattern space.
    .
        Matches any character, including newline. 
    *
        Matches a sequence of zero or more instances of matches for the preceding regular expression.
    []
        Matches any single character in list.
    [^]
        A leading ^ reverses the meaning of list, so that it matches any single character not in list.
    \(..\)
        Groups the inner regexp as a whole.
    &
        Keep the search characters, and replace others. For example, s/love/**&**/，love line became **love**
    \<
        Anchoring the beginning of the word. For instance, /\<love match lines which begin with love.
    \>
        Anchoring the end of the word. For example, /love\> match lines which end with love.
    x\{i\}
        Matches exactly i sequences. For example, /o\{5\} match lines which include 5 o.
    x\{i,\}
        Matches more than or equal to i sequences. For example, /o\{5,\} match lines which include more than or equal 5 o.
    x\{i,j\}
    Matches between i and j, inclusive, sequences. For example, /o{5,10\} match lines which include between 5 and 10 o.

####Examples
    ‘abcdef’
        Matches ‘abcdef’.
    ‘a*b’
        Matches zero or more ‘a’s followed by a single ‘b’. For example, ‘b’ or ‘aaaaab’.
    ‘a\?b’
        Matches ‘b’ or ‘ab’.
    ‘a\+b\+’
        Matches one or more ‘a’s followed by one or more ‘b’s: ‘ab’ is the shortest possible match, but other examples are ‘aaaab’ or ‘abbbbb’ or ‘aaaaaabbbbbbb’.
    ‘.*’
    ‘.\+’
        These two both match all the characters in a string; however, the first matches every string (including the empty string), while the second matches only strings containing at least one character.
    ‘^main.*(.*)’
        This matches a string starting with ‘main’, followed by an opening and closing parenthesis. The ‘n’, ‘(’ and ‘)’ need not be adjacent.
    ‘^#’
        This matches a string beginning with ‘#’.
    ‘\\$’
        This matches a string ending with a single backslash. The regexp contains two backslashes for escaping.
    ‘\$’
        Instead, this matches a string consisting of a single dollar sign, because it is escaped.
    ‘[a-zA-Z0-9]’
        In the C locale, this matches any ASCII letters or digits.
    ‘[^ tab]\+’
        (Here tab stands for a single tab character.) This matches a string of one or more characters, none of which is a space or a tab. Usually this means a word.
    ‘^\(.*\)\n\1$’
        This matches a string consisting of two equal substrings separated by a newline.
    ‘.\{9\}A$’
        This matches nine characters followed by an ‘A’.
    ‘^.\{15\}A’
        This matches the start of a string that contains 16 characters, the last of which is an ‘A’. 

###Often-used commands
    { commands }
        A group of commands may be enclosed between { and } characters.
    : label
        specify the location of label for branch commands.
    a\
        insert text after current line.
    b lable
        unconditionally branch to label.
    c\
        replace the current line with the text
    d
        Delete the pattern space; immediately start next cycle. 
    D
        delete text in the pattern space up to the first newline
    h
        Replace the contents of the hold space with the contents of the pattern space. 
    H
        Append a newline to the contents of the hold space, and then append the contents of the pattern space to that of the hold space. 
    g
        Replace the contents of the hold space with the contents of the pattern space. 
    G
        Append a newline to the contents of the pattern space, and then append the contents of the hold space to that of the pattern space. 
    l
        Print the pattern space in an unambiguous form.
    n
        read next line.
    N
        Add a newline to the pattern space, then append the next line of input to the pattern space.
    p
        Print out the pattern space. 
    P
        Print out the portion of the pattern space up to the first newline. 
    q
        Exit sed without processing any more commands or input.
    r filename
        Queue the contents of filename to be read and inserted into the output stream at the end of the current cycle, or when the next input line is read. 
    t lable
        Branch to label only if there has been successful substitution since the last input line was read or conditional branch was taken.
    w filename
        Write the pattern space to filename. 
    W filename
        Write to the given filename the portion of the pattern space up to the first newline. 
    !
        Indicates that the following command take effect on all rows are not selected.
    s/regexp/replacement/flags
        that portion of the pattern space which was matched is replaced with replacement. 
    =
        Print out the current input line number (with a trailing newline). 
    #
        The # character begins a comment; the comment continues until the next newline.
    *
    Matches a sequence of zero or more instances of matches for the preceding regular expression. 

## Examples

    # print line 3
    sed -n '3p' $FILE_NAME
    
    # print lines between 100 and 200
    sed -n '100,200p' $FILE_NAME
    
    # print lines which contain "my".
    sed -n '/my/p' $FILE_NAME
    
    # delete the last line, and print others
    sed '$d' $FILE_NAME
    
    # delete lines which contain "my"
    sed '/my/d' $FILE_NAME
    
    # delete lines between 2 and 5
    sed '2,5d' $FILE_NAME
    
    # delete lines from the line containing "My" to the line containing "You"
    sed '/My,/You/d' $FILE_NAME
    
    # delete lines from the line containing "My" to line 10.
    sed '/My,10d' $FILE_NAME
    
    #'s/regexp/replacement/flags'
    sed -i '{'s/9080/8080/g'}' pom.xml
    sed '{'s/3306/7077/g'; 's/root/cbay/g'; }' pom.xml
    sed '{'s/9080/8080/g'; 's/3306/7077/g'; 's/root/cbay/g'; }' pom.xml
    
    #All "My" will be replaced by "You".
    sed 's/^My/You/g' $FILE_NAME
    sed -n '1,20s/My$/You/gp' $FILE_NAME
    
    #the first character after s will be the delimiter.
    sed 's#My#You#g' $FILE_NAME
    
    # sed -e variables
    sed -e '1,10d' -e 's/My/You/g' $FILE_NAME
    sed -e $var1'i \'"$var2" $FILE_NAME
    
    sed -e ":begin; /<port>/,/<\/port>/ { /<\/port>/! { $! { N; b begin }; }; s/<port>.*<\/port>/<port>8080<\/port>/; };" pom.xml
    
    sed -e ":begin; /<connection.password/,/\/>/ { /\/>/! { $! { N; b begin }; }; s/<connection.password.*\/>/<connection.password>cbay<\/connection.password>/; };" pom.xml
    
    sed -e "{s/9080/8080/g; s/3306/7077/g; s/root/cbay/g; }; :begin; /<connection.password/,/\/>/ { /\/>/! { $! { N; b begin }; }; s/<connection.password.*\/>/<connection.password>cbay<\/connection.password>/; };" -i pom.xml
    
    sed '/My/r test.txt' $FILE_NAME
    sed -n '/My/w test.txt' $FILE_NAME
    
    sed '/My/a\
    Hello,\
    Johnny' $FILE_NAME
    
    # command n, read the next line, and deal with this line.
    sed '/My/{n;s/My/You/;}' $FILE_NAME
    
    # command q, exit sed
    sed '/My/{s/My/You/;q;}' $FILE_NAME

## REFERENCES
- [sed, a stream editor](http://www.gnu.org/software/sed/manual/sed.html)
- [linux sed命令详解](http://www.iteye.com/topic/587673)
- [SED(带-E参数)变量传递问题](http://bbs.chinaunix.net/thread-796205-1-1.html)
- [sed命令详解](http://www.cnblogs.com/edwardlost/archive/2010/09/17/1829145.html)


