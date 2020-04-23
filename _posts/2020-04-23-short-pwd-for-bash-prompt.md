---
layout: post
title: Short pwd for bash prompt
author: fnds
categories: tools
tags: bash
---

## tl;dr: Add this function to your .bashrc and use it to show only the current and the parent directory in the bash command prompt:

    function short_pwd {
        cdir=${PWD##*/}
        pdir=${PWD%/*}
        gdir=${pdir%/*}
        pdir=${pdir##*/}
        [[ $gdir == "" && $pdir == "" ]] && echo "/$cdir" && return
        [[ $gdir == "" && $pdir != "" ]] && echo "/$pdir/$cdir" && return
        echo "$pdir/$cdir"
    }

# Example

    $ export PS1="$(short_pwd) $ "
    ggggg/hhhhh $ pwd
    /tmp/aaaaa/bbbbb/ccccc/ddddd/eeeee/fffff/ggggg/hhhhh
    ggggg/hhhhh $ cd /usr/local/bin
    local/bin $

# Why is it better?

Bash PS1 prompt variable allows us to use \W or \w to show the current directory. 

\w could make the prompt become long and cumbersome when we are working with many directory levels. 

    $ export PS1='\w $ '
    /tmp/aaaaa/bbbbb/ccccc/ddddd/eeeee/fffff/ggggg/hhhhh $

\W might cause confusion for lack of context. 

    $ export PS1='\W $ '
    bin $ 
    
Where am I? /bin or /usr/bin? Neither!

    bin $ pwd
    /usr/local/bin
    
One solution for the dilema is to show both the parent and current dir in the prompt:

    $ export PS1='$(short_pwd) $ '
    /tmp $ cd /usr/local/bin
    local/bin $ cd /tmp/aaaaa/bbbbb/ccccc/ddddd/eeeee/fffff/ggggg/hhhhh
    ggggg/hhhhh $

***short_pwd*** is extremely fast because it uses bash builtin string manipulation which doesn't spawn any subprocesses.
It could use awk, sed, basename, dirname, etc., to the same effect, but it might cause some lag each time you display the prompt 
depending on how much stuff you have on your PS1. For instance, I have a function on PS1 to display the git branch.

This web page is an excellent reference on the subject: [https://www.tldp.org/LDP/abs/html/string-manipulation.html](https://www.tldp.org/LDP/abs/html/string-manipulation.html)

Thanks for reading. I hope this article helps someone.

-fnds
