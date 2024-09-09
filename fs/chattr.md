# See files to immutable or appendable (examples for chattr) 

## Appenable 

```
touch topsecret
echo "test" >> topsecret
cat topsecret
```

```
# now only appenable 
chattr +a topsecret
# not working
echo "test neu" > topsecret
# works 
echo "test neu" >> topsecret
# works 
cat topsecret
```

```
lsattr topsecret
```

```
# set immutable 
chattr +i topsecret
lsattr topsecret
# not appendable 
echo "test neu" >> topsecret
# not writable 
echo "test neu" > topsecret
# not removable 
rm topsecret
# not renameable 
mv topsecret topsecretneu
```
