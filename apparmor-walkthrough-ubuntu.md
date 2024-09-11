# apparmor - walkthrough (Ubuntu 20.04/22.04) 

## Step 0: set lang to english

```
sudo dpkg-reconfigure locales
-> en.US
-> Step 2 also

su - 
```


## Step 1: Create script and execute it without protection

```
cd /usr/local/bin
```

```
# vi example.sh 
# see next block for content
```

```
#!/bin/bash

echo "This is an apparmor example."

touch data/sample.txt
echo "File created"

rm data/sample.txt
echo "File deleted"
```

```
chmod u+x example.sh
mkdir data
example.sh
```

## Step 2: Protect it with apparmor 

```
Session 1: 
aa-genprof example.sh 



Session 2: (same server) 
cd /usr/local/bin 
example.sh 

Session 1:
# Press S for scan
# Now the logs will get scanned 
# Add each Entry with I (Inherit)  or A (Allow) 
# When ready F finish 
#### Let us enforce it (currently it is on complain) 
aa-enforce usr.local.bin.example.sh

Session 2:
# Does it still work 
example.sh 
# Now add new commands 
echo "echo somedata > righthere.txt" >> example.sh   
# Execute again 
example.sh 
# permission denied

Session 1:
# analyze log and add changed things
logprof 

Session 2:
# now try again.
example.sh

```

```
