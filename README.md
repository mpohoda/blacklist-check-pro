# blacklist-check-unix-linux-utility
Blacklist check UNIX/Linux utility. I was just a bit tired of web interfaces.

###Introduction

Check blacklisting for domains and IP addresses in shell.

Works on UNIX/Linux systems with Bash.

Blacklists grabbed from http://multirbl.valli.org/ (all DNSBLs) and other.

![ScreenShot](http://aarvik.dk/content/images/2013/Dec/bl.png)

###Installation

    curl -O https://raw.githubusercontent.com/adionditsak/blacklist-check-unix-linux-utility/master/bl
    chmod +x ./bl
    mv ./bl /usr/bin

###Usage

    # Use with domains or IP addresses
    $ bl domain.tld
    $ bl 8.8.8.8 # IP
    
    # Pipe with other UNIX utils, eg. grep. Only blacklisted:
    $ bl domain.tld | grep "blacklisted"
    
    # or from SRV list
    $ dig txt +short qualityunit.com | tr " " "\n" | awk -F: '{if(NR>1)print $2}' | head -n -3 | xargs -L1 ./bl -q -a -d

###Sample output

    $ bl 8.8.8.8
    You entered an IP: 8.8.8.8
    8.8.8.8 name google-public-dns-a.google.com.
    15-02-17_Feb:02:1424185674_+0000 8.8.8.8.0spam.fusionzero.com.          [not listed]
    15-02-17_Feb:02:1424185674_+0000 8.8.8.8.0spam-killlist.fusionzero.com. [not listed]
    15-02-17_Feb:02:1424185674_+0000 8.8.8.8.rbl.abuse.ro.                  [not listed]
    15-02-17_Feb:02:1424185674_+0000 8.8.8.8.spam.dnsbl.anonmails.de.       [not listed]
    15-02-17_Feb:02:1424185674_+0000 8.8.8.8.dnsbl.anticaptcha.net.         [not listed]
    ...
