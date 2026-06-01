# w-sendmail

Python-script for sending (relaying) system-status-mails to administrator through an external SMTP server.

This script work as a replacement for classic MTA's (`DragonFly Mail Agent`, `exim4`, `postfix` or `msmtp`), this are overly complicated if you just want to sendt system-mails on a server. But in all fairness mails are not queued in current version in case of e.g. network/SMTP failures.

Only require some standard Python libraries which likely already are installed on your box.

To- and From-addresses specified by the daemons that automatic send mails are overruled by the addresses specified in the 
config-file to ensure system-status-mails will always be sent to the correct administrator, e.g. daemons might specify sender to "root".

How to use:

1: Download w-sendmail to `/usr/local/bin/`
    
2: Create a symbolic-link to sendmail: `ln -sf "/usr/local/bin/w-sendmail" "/usr/sbin/sendmail"`

3: Make w-sendmail executeable: `chmod +x "/usr/local/bin/w-sendmail"`

4: Create configfile `/etc/w-sendmail.conf` with these properties:
```
TOADDR = "xx"
FROMADDR = "xx"
SMTP_SERVER = "xx"
SMTP_PORT = "587"
USE_TLS = "True"
SMTP_USER = "xx"
SMTP_PASSWORD = "xx"
```

5: Make a test-mail: `echo -e "Subject: Hello World\n\nThis is body of testmail" | sendmail`

6: Check the journal-log and your mailbox:
```
journalctl -e
#For real-time update:
journalctl -f
````

Will work find with MUA (Mail-User-Agents) like `bsd-mailx` if you already has a work-flow which use the `mail` command, example: `echo "Hello World" | mail -s "Test mail" root`

But again, the specified to-address (in this example "root") is on purpose overruled by the address specified in the config-file.
