# Priority string equivalent

```console
debug               Debugging statements
info                Miscellaneous statements
notice              Important statements, but not necessarily bad news
warning             Potentially dangerous situation
warn                Same as warning, but not to be used
err                 An error condition
error               Same as err, but not to be used
crit                Critical situation
alert               A message indicating an important occurence
emerg               An emergency situation
```

# rsyslog Message Property Names

```console
msg                 The actual log of message
rawmsg              The message as is received from socket
HOSTNAME            Hostname from the message
FROMHOST            Hostname of the system the message came from
syslogtag           TAG from the message
PRI-text            The PRI part of message in textual form
syslogfacility-text The facility from the message in text form
syslogseverity-text Severity from the message in text form
timereported        Timestamp from the message
MSGID               The content of MSGID field
```
