# One Time Password (otp) 

## Installation on Centos 8 

```

dnf install -y oathtool pam_oath

```

## Configuation 

```
# Settings in oath 
# create hexstring for pass 
echo "itsme" | od -x
0000000 7469 6d73 0a65
0000006
# use without 0 and blanks 
#
echo "kurs - 74696d730a65" > /etc/oath/oath.users 
chmod 000 /etc/oath/oath.users 
chown root /etc/oath/oath.users 

# Setup pam
# vi /etc/pam.d/su 
# add after root-entry 
auth            sufficient      pam_rootok.so
auth            requisite pam_oath.so usersfile=/etc/oath/users.oath window=5
```

## Create list 

```
authtool -w 5 74696d730a65
```

## Test it 

```
# starting from root the first time works without pw
su - kurs

# now you need to enter one otp from list
# and after that your normal pw 
su - kurs
exit

# try again and try to use same otp 
su - kurs 

```
