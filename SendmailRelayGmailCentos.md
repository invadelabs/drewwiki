---
title: SendmailRelayGmailCentos
layout: default
---

### Setup certs

    # mkdir /etc/mail/certs
    # chmod 700 /etc/mail/certs
    # cp /etc/pki/tls/certs/ca-bundle.crt /etc/mail/certs
    # cd /etc/mail/certs
    # openssl req -new -x509 -keyout cakey.pem -out cacert.pem -days 3650
    # openssl req -nodes -new -x509 -keyout sendmail.pem -out sendmail.pem -days 3650
    # chmod 600 /etc/mail/certs/*

### Setup client info

    # mkdir /etc/mail/auth 
    # chmod 700 /etc/mail/auth
    # vi /etc/mail/auth/client-info

Add this to the file, changing username and password to gmail login
info.

    AuthInfo:smtp.gmail.com "U:root" "I:username" "P:password" "M:PLAIN"
    AuthInfo:smtp.gmail.com:587 "U:root" "I:username" "P:password" "M:PLAIN"

Make hash of client-info

    # makemap -r hash client-info.db < client-info
    # chmod 600 /etc/mail/auth/*

### /etc/mail/sendmail.mc

    divert(-1)dnl
    include(`/usr/share/sendmail-cf/m4/cf.m4')dnl
    VERSIONID(`setup for linux')dnl
    OSTYPE(`linux')dnl

    define(`confDEF_USER_ID', ``8:12'')dnl
    dnl define(`confAUTO_REBUILD')dnl
    define(`confTO_CONNECT', `1m')dnl
    define(`confTRY_NULL_MX_LIST', `True')dnl
    define(`confDONT_PROBE_INTERFACES', `True')dnl
    define(`PROCMAIL_MAILER_PATH', `/usr/bin/procmail')dnl
    define(`ALIAS_FILE', `/etc/aliases')dnl
    define(`STATUS_FILE', `/var/log/mail/statistics')dnl
    define(`UUCP_MAILER_MAX', `2000000')dnl
    define(`confUSERDB_SPEC', `/etc/mail/userdb.db')dnl
    define(`confPRIVACY_FLAGS', `authwarnings,novrfy,noexpn,restrictqrun')dnl
    define(`confAUTH_OPTIONS', `A')dnl

    dnl # cert stuff
    define(`CERT_DIR', `/etc/mail/certs')
    define(`confCACERT_PATH', `CERT_DIR')
    define(`confCACERT', `CERT_DIR/ca-bundle.crt')
    define(`confCRL', `CERT_DIR/ca-bundle.crt')
    define(`confSERVER_CERT', `CERT_DIR/sendmail.pem')
    define(`confSERVER_KEY', `CERT_DIR/sendmail.pem')
    define(`confCLIENT_CERT', `CERT_DIR/sendmail.pem')
    define(`confCLIENT_KEY', `CERT_DIR/sendmail.pem')

    define(`confTO_IDENT', `0')dnl

    FEATURE(`no_default_msa', `dnl')dnl
    FEATURE(`smrsh', `/usr/sbin/smrsh')dnl
    FEATURE(`mailertable', `hash -o /etc/mail/mailertable.db')dnl
    FEATURE(`virtusertable', `hash -o /etc/mail/virtusertable.db')dnl
    FEATURE(redirect)dnl
    FEATURE(always_add_domain)dnl
    FEATURE(use_cw_file)dnl
    FEATURE(use_ct_file)dnl

    dnl #
    dnl # The -t option will retry delivery if e.g. the user runs over his quota.
    dnl #
    FEATURE(local_procmail, `', `procmail -t -Y -a $h -d $u')dnl
    FEATURE(`access_db', `hash -T<TMPF> -o /etc/mail/access.db')dnl
    FEATURE(`blacklist_recipients')dnl
    EXPOSED_USER(`root')dnl

    dnl # The following causes sendmail to only listen on the IPv4 loopback address
    dnl # 127.0.0.1 and not on any other network devices. Remove the loopback
    dnl # address restriction to accept email from the internet or intranet.
    dnl #
    dnl DAEMON_OPTIONS(`Port=smtp,Addr=127.0.0.1, Name=MTA')dnl

    dnl # We strongly recommend not accepting unresolvable domains if you want to
    dnl # protect yourself from spam. However, the laptop and users on computers
    dnl # that do not have 24x7 DNS do need this.
    dnl #
    FEATURE(`accept_unresolvable_domains')dnl
    dnl #
    dnl FEATURE(`relay_based_on_MX')dnl
    dnl # 
    dnl # Also accept email sent to "localhost.localdomain" as local email.
    dnl # 
    LOCAL_DOMAIN(`localhost.localdomain')dnl
    dnl #
    dnl # The following example makes mail from this host and any additional
    dnl # specified domains appear to be sent from mydomain.com
    dnl #
    MASQUERADE_AS(`drewserv.drewrents.readytoinvade.com')dnl
    dnl #
    dnl # masquerade not just the headers, but the envelope as well
    dnl #
    dnl FEATURE(masquerade_envelope)dnl
    dnl #
    dnl # masquerade not just @mydomainalias.com, but @*.mydomainalias.com as well
    dnl #
    dnl FEATURE(masquerade_entire_domain)dnl
    dnl #
    dnl MASQUERADE_DOMAIN(localhost)dnl
    dnl MASQUERADE_DOMAIN(localhost.localdomain)dnl
    dnl MASQUERADE_DOMAIN(mydomainalias.com)dnl
    dnl MASQUERADE_DOMAIN(mydomain.lan)dnl

    FEATURE(masquerade_envelope) FEATURE(genericstable, `hash -o /etc/mail/genericstable')
    GENERICS_DOMAIN_FILE(`/etc/mail/genericsdomain') 

    define(`SMART_HOST',`smtp.gmail.com')dnl
    define(`RELAY_MAILER_ARGS', `TCP $h 587')dnl
    define(`ESMTP_MAILER_ARGS', `TCP $h 587')dnl
    define(`confAUTH_MECHANISMS', `EXTERNAL GSSAPI DIGEST-MD5 CRAM-MD5 LOGIN PLAIN')dnl
    FEATURE(`authinfo',`hash /etc/mail/auth/client-info')dnl

    MAILER(local)dnl
    MAILER(smtp)dnl
    #MAILER(procmail)dnl
    #MAILER(cyrusv2)dnl

### Build sendmail config

    # cd /etc/mail; make

### Restart sendmail

    # /etc/init.d/sendmail restart

### Send a test message

    echo "This is a test email..." | mail -s "Test Email" some-email@address.com

### Debug

    # tail -f /var/log/maillog
