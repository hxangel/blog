---
title: install mail server on centos 5.5
id: 566
categories:
  - Linux系统
date: 2013-07-21 00:24:19
tags:
---

<pre class="lang:sh decode:true ">yum remove sendmail yum install dovecot yum install postfix
yum install cyrus-sasl cyrus-sasl-devel cyrus-sasl-gssapi cyrus-sasl-md5 cyrus-sasl-plain</pre>
<pre class="lang:default decode:true ">#start dovecot config 
#file=/etc/dovecot.conf
protocols = imap imaps pop3 pop3s #line 20
default_mail_env = maildir:/home/vmail/%d/%n #line205

first_valid_uid = 89 #line 328 
ssl_cert_file = /etc/postfix/ssl/smtpd.crt #line 91
ssl_key_file = /etc/postfix/ssl/smtpd.key #line 92
ssl_ca_file = /etc/postfix/ssl/cacert.pem #line 105
mechanisms = plain login
   passdb sql {
   # Path for SQL configuration file, see doc/dovecot-sql-example.conf #line 869
    args = /etc/dovecot-mysql.conf
   }
    userdb sql {
        # Path for SQL configuration file, see doc/dovecot-sql-example.conf #line 931
        args = /etc/dovecot-mysql.conf
    }
    client {
      # The client socket is generally safe to export to everyone. Typical use
      # is to export it to your SMTP server so it can do SMTP AUTH lookups
      # using it.
      path = /var/spool/postfix/private/auth
      user = postfix
      group = postfix
      mode = 0660
    }
#end dovecot config</pre>
<pre class="lang:sh decode:true ">#create vmail
&gt; mkdir /home/vmail 
&gt; chmod 770 /home/vmail 
&gt; chown postfix:postfix /home/vmail</pre>
<pre class="lang:tsql decode:true ">#start dovecot-mysql config
#file=/etc/dovecot-mysql.conf
driver = mysql
connect = host=/var/lib/mysql/mysql.sock dbname=postfix user=postfix password=pwd4postfix
default_pass_scheme = MD5-CRYPT
user_query = SELECT '/home/vmail/%d/%n' as home, 'maildir:/home/vmail/%d/%n' as mail, 89 AS uid, 89 AS gid, concat('dirsize:storage=', quota) AS quota FROM mailbox WHERE username = '%u' AND active = '1'
password_query = SELECT username as user, password, 89 AS uid, 89 AS gid FROM mailbox WHERE username = '%u' AND active = '1'
#end dovecot-mysql.conf</pre>
<pre class="lang:default decode:true ">#start postfix config main.cf
#file = /etc/postfix/main.cf
mynetworks = 198.71.86.91/32, 127.0.0.0/8, 198.71.86.92/32, 192.80.146.47/32 #line 248
inet_interfaces = all #line 100
myhostname = mail.vkilo.com #line 70
mydomain =vkilo.com #line 71
#inet_interfaces = localhost #line 103

mydestination = $myhostname, localhost.$mydomain, localhost #line 148

#start virtual_mailbox config append
virtual_mailbox_base = /home/vmail
readme_directory = /usr/share/doc/postfix-2.3.3/README_FILES
virtual_alias_maps = mysql:/etc/postfix/mysql_virtual_alias_maps.cf, regexp:/etc/postfix/virtual_regexp
virtual_gid_maps = static:89
virtual_mailbox_domains = mysql:/etc/postfix/mysql_virtual_domains_maps.cf
virtual_mailbox_maps = mysql:/etc/postfix/mysql_virtual_mailbox_maps.cf
virtual_minimum_uid = 89
virtual_transport = virtual
virtual_uid_maps = static:89
dovecot_destination_recipient_limit = 1
smtpd_sasl_auth_enable = yes
smtpd_sasl_type = dovecot
smtpd_sasl_path=/var/spool/postfix/private/auth
smtpd_sasl_local_domain = $myhostname
smtpd_sasl_security_options = noanonymous
broken_sasl_auth_clients = yes
smtpd_sasl_authenticated_header = yes
smtpd_recipient_restrictions = permit_mynetworks, permit_sasl_authenticated, reject_unauth_destination, reject_non_fqdn_recipient, reject_unknown_recipient_domain
smtpd_sasl_security_restrictions = permit_sasl_authenticated, permit_mynetworks, reject_unauth_destination, reject_non_fqdn_recipient, reject_unknown_recipient_domain
#smtpd_sasl_security_restrictions = permit_mynetworks, permit_sasl_authenticated, reject_unauth_destination
smtpd_tls_security_level = may
smtpd_tls_loglevel = 1
smtpd_tls_auth_only =yes
smtp_use_tls = yes
smtpd_use_tls = yes
smtp_tls_note_starttls_offer = yes
smtpd_tls_key_file = /etc/postfix/ssl/smtpd.key
smtpd_tls_cert_file = /etc/postfix/ssl/smtpd.crt
#`smtpd_tls_CAfile = /etc/postfix/ssl/cacert.pem
smtpd_tls_received_header = yes
smtpd_tls_session_cache_timeout = 3600s
tls_random_source = dev:/dev/urandom
smtpd_helo_restrictions = permit_sasl_authenticated, permit_mynetworks, reject_non_fqdn_hostname
smtpd_sender_restrictions = reject_non_fqdn_sender, reject_unknown_sender_domain
smtpd_recipient_restrictions = permit_sasl_authenticated, permit_mynetworks, reject_unauth_destination, reject_non_fqdn_recipient, reject_unknown_recipient_domain
smtpd_helo_required = yes
unknown_local_recipient_reject_code = 550
disable_vrfy_command = yes
smtpd_data_restrictions = reject_unauth_pipelining
#end postfix config</pre>
<pre class="lang:default decode:true ">#Afterwards we create the certificates for TLS
mkdir /etc/postfix/ssl
cd /etc/postfix/ssl/
openssl genrsa -des3 -rand /etc/hosts -out smtpd.key 1024
chmod 600 smtpd.key
openssl req -new -key smtpd.key -out smtpd.csr
openssl x509 -req -days 3650 -in smtpd.csr -signkey smtpd.key -out smtpd.crt
openssl rsa -in smtpd.key -out smtpd.key.unencrypted
mv -f smtpd.key.unencrypted smtpd.key
openssl req -new -x509 -extensions v3_ca -keyout cakey.pem -out cacert.pem -days 3650
#end create certificates</pre>
<pre class="lang:default decode:true ">#start mysql_virtual_alias_maps.cf
#file=/etc/postfix/mysql_virtual_alias_maps.cf
user = postfix
password = postfixuser
hosts = localhost
dbname = postfix
table = alias
select_field = goto
where_field = address
#end mysql_virtual_alias_maps.cf</pre>
<pre class="lang:default decode:true ">#start /etc/postfix/mysql_virtual_domains_maps.cf
#file=/etc/postfix/mysql_virtual_domains_maps.cf
user = postfix
password = postfixuser
hosts = localhost
dbname = postfix
table = domain
select_field = domain
where_field = domain
additional_conditions = and backupmx = '0' and active = '1'
#end</pre>
<pre class="lang:default decode:true ">#vim /etc/postfix/mysql_virtual_mailbox_maps.cf
hosts = localhost
user = postfix
password = postfixuser
dbname = postfix
table = mailbox
select_field = maildir
where_field = username
#end</pre> 
<pre class="lang:default decode:true " >#vim /usr/lib64/sasl2/smtpd.conf
#for i586 /usr/lib/sasl2/smtpd.conf
pwcheck_method: auxprop
mech_list: PLAIN LOGIN
auxprop_plugin: sql
sql_verbose: yes
sql_engine: mysqli
sql_hostnames: localhost
sql_user: postfix
sql_passwd: postfixuser
sql_database: postfix
sql_select: select password from mailbox where username = '%u@%r'
log_level: 3
#end</pre> 

<pre class="lang:default decode:true " >service postfix start
service saslauthd start
chkconfig --level 235 postfix on
chkconfig --level 235 saslauthd on
postconf -e virtual_mailbox_maps=mysql:/etc/postfix/mysql-virtual-mailbox-maps.cf
postmap -q john@example.com mysql:/etc/postfix/mysql-virtual-mailbox-maps.cf</pre> 