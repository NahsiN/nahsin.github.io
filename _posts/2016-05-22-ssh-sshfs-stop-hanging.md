---
layout: post
title: Stop ssh/sshfs from hanging up your applications
---

For my work, I need to keep multiple ssh and sshfs tunnels open. After an
upgrade to Ubuntu 16.04, my ssh tunnels started to hang after some period
of inactivity. Now if a ssh tunnel hangs, all one has to do is close the
terminal. So inconvenient but managable. But if a sshfs tunnel hangs, then a
simple _ls_ command can hang
the terminal. Or if you are using Nautilus (file manager), simply trying
to browse to the mounted folder will cause a hang making you force quit
the application. Lastly, desperation kicks in and you now try to force a
_umount_, but OS will complain saying some resource is busy.
To summarize, I am forced to restart every time a sshfs tunnel hangs which
is really annoying.

To resolve this issue for ssh, we use the option ServerAliveInterval. Quoting
from the man page of ssh_config,
> ServerAliveInterval  
> Sets a timeout interval in seconds after which if no data has
been received from the server, ssh(1) will send a message through
the encrypted channel to request a response from the server. The
default is 0, indicating that these messages will not be sent to
the server, or 300 if the BatchMode option is set.
ProtocolKeepAlives and SetupTimeOut are Debian-specific compati-
bility aliases for this option.

Therefore, either modify your ssh_config file or use the following command

```
ssh -o ServerAliveInterval=300 user@machine-name
```

So far, 300 = 5 minutes has served me well. Experiment with the value to find
one that works for you.

For sshfs, use the following command

```
sshfs user@machine-name -o ServerAliveInterval=300 mount-path
```
