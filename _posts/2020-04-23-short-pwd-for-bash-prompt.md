---
layout: post
title: Short pwd for bash prompt
author: fnds
categories: tools
tags: bash
---

This solution is based on [code found on stackexchange.com](https://unix.stackexchange.com/questions/216953/show-only-current-and-parent-directory-in-bash-prompt). I tweaked it to my needs and created a function to make it easier to use.

## tl;dr: Add this function to your .bashrc and use it to show only the current and parent directory in the bash prompt:

    function short_pwd { [[ $PWD =~ /.*/.*/.* ]] && echo "${PWD#"${PWD%/*/*}/"}" || echo "$PWD" ; }

# Example

    $ PS1="$(short_pwd) $ "
    ggggg/hhhhh $ pwd
    /tmp/aaaaa/bbbbb/ccccc/ddddd/eeeee/fffff/ggggg/hhhhh
    ggggg/hhhhh $ 
    ggggg/hhhhh $ cd /usr/local/bin
    local/bin $

# Why is it "better"?

Bash PS1 variable allows us to configure the prompt using \W or \w to show the current directory. 

\w shows the full path but can cause the prompt to become long and cumbersome when we are working with many directory levels. 

    $ PS1='\w $ '
    /tmp/aaaaa/bbbbb/ccccc/ddddd/eeeee/fffff/ggggg/hhhhh $

\W shows only the lowest directory level, which might cause confusion for lack of context. 

    $ PS1='\W $ '
    bin $ 
    
Where am I? /bin or /usr/bin? Neither!

    bin $ pwd
    /usr/local/bin
    
One solution for the dilema is to show both the parent and current dir in the prompt:

    $ PS1='$(short_pwd) $ '
    /tmp $ cd /usr/local/bin
    local/bin $ 
    local/bin $ cd /tmp/aaaaa/bbbbb/ccccc/ddddd/eeeee/fffff/ggggg/hhhhh
    ggggg/hhhhh $

Another downside of \W and \w to me is displaying "```~```" for the $HOME directory. This solution does not convert $HOME to "```~```".

    $ PS1="\W $ "
    / $ cd
    ~ $
    ~ $ PS1="$(short_pwd) $ "
    /home/fnds $

If you want to preserve the "```~```" behavior, just use the [original code on stackexchange.com](https://unix.stackexchange.com/questions/216953/show-only-current-and-parent-directory-in-bash-prompt). 

Check this web page for an excellent reference on bash builtin string manipulation: [https://www.tldp.org/LDP/abs/html/string-manipulation.html](https://www.tldp.org/LDP/abs/html/string-manipulation.html)

Thanks for reading. I hope this article helps someone.

-fnds
