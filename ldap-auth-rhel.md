# Ldap RHEL 9

```
1. Installation der Pakete
dnf install -y
```
```
2. Configuration von /etc/sssd/conf.d/00-sssd.conf
[sssd]
config_file_version = 2
services = nss, pam, autofs
domains = default

[sssd]
domains = LOCAL,example.com

[domain/example.com]
enumerate = true
id_provider = ldap
autofs_provider = ldap
auth_provider = ldap
chpass_provider = ldap
ldap_uri = ldap://192.168.56.104/
ldap_search_base = dc=example,dc=com
ldap_id_use_start_tls = True
cache_credentials = True
ldap_tls_cacertdir = /etc/openldap/certs
ldap_tls_reqcert = allow

[nss]
homedir_substring = /home
```

```
chown -R sssd:sssd /etc/sssd/conf.d
systemctl restart sssd
# hier gibt es fehler 
```


```
# this configures pam 
authselect select sssd with-mkhomedir
Profile "sssd" was selected.
The following nsswitch maps are overwritten by the profile:
- passwd
- group
- netgroup
- automount
- services
```

```
# checks for user on ldap, if user does not exist /  sssd needs
getent passwd luser1
```
