---
layout: post
title: SSH Agent Auto Startup on Cygwin
author: fnds
categories: tools
tags: bash
---

Create script $HOME/bin/ssh-agent-start.sh:

    ### ssh-agent startup

    environ="$HOME/.ssh/agent.env"

    # start ssh-agent if not running
    AGENT_PID=$(pgrep ssh-agent)
    if [ $? -ne 0 ]; then
        (umask 077; ssh-agent > "$environ")
        #ssh-add
        echo "-- SSH Agent started (PID: $SSH_AGENT_PID)"
    else
        echo "-- SSH Agent already running (PID: $AGENT_PID)"
    fi

    # set environment
    if [ -f "$environ" ]; then
        . "$environ" >/dev/null
        echo "-- SSH Agent environment set"
    fi

Add this line at the end on $HOME/.bashrc:

    . $HOME/bin/ssh-agent-start.sh

Add this line to $HOME/.ssh/config

    echo "AddKeysToAgent yes" >> $HOME/.ssh/config
    
Open a new window on Cygwin. It will automatically start the ssh-agent. The keys will be cached when ssh is run for the first time.

Thanks for reading.

-fnds

# References

- https://superuser.com/questions/1125803/whats-the-best-way-to-start-ssh-agent-with-cygwin
- https://superuser.com/questions/1173569/ssh-agent-setup-on-windows-with-cygwin
