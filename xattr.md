# xattr - walkthrough 

## Generic 

  * save in the inode 

## Walkthrough 

```
# only possible as root 
touch foo-file
lsattr foo-file 
chattr +a foo-file

## then this works 
echo "test" >> foo-file 
## this not 
echo "test" > foo-file 

## + -> immutable 
chattr +i foo-file 
## does not work 
echo "no possibe" > foo-file 
echo "also not possible" >> foo-file
# and not deletable 
rm -f foo-file 
```


