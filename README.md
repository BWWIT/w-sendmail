# w-sendmail

Python-script for relaying system-status-mails to administrator. 
This script work as a replacement for a classic MTA's.
Only require some standard Python libraries which are likely already installed.
To- and From-addresses specified by the daemons that automatic send mails are overruled by the addresses specified in the 
config-file to ensure system-status-mails will always be sent to the correct administrator, e.g. daemons might specify sender to "root", so it has to be set to the real admin email.

How to use:

    1: Download w-sendmail /usr/local/bin/
    
    2: Create a symbolic-link to sendmail
        ln -sf "/usr/local/bin/w-sendmail" "/usr/sbin/sendmail"

    3: Make w-sendmail executeable:
        chmod +x "/usr/local/bin/w-sendmail"

    4: Create configfile "/etc/w-sendmail.conf" with these properties:
        TOADDR = "xx"
        FROMADDR = "xx"
        SMTP_SERVER = "xx"
        SMTP_PORT = "587"
        USE_TLS = "True"
        SMTP_USER = "xx"
        SMTP_PASSWORD = "xx" 

    5: Make a test-mail:
        echo -e "Subject: Hello World\n\nThis is body of testmail" | sendmail

    6: Check the journal-log and your mailbox:
        journalctl -e
        or for real-time update:
        journalctl -f
