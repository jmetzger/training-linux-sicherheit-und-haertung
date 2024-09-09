# Was nicht in sudo machen ?

```
# Achtung keine Negierung setzen
bill        ALL = ALL, !SU, !SHELLS
```

## Why not ? 

```
 It is generally not effective to "subtract" commands from ALL using the
   ’!’ operator.  A user can trivially circumvent this by copying the
   desired command to a different name and then executing that.  For
   example:

       bill        ALL = ALL, !SU, !SHELLS

   Doesn’t really prevent bill from running the commands listed in SU or
   SHELLS since he can simply copy those commands to a different name, or
   use a shell escape from an editor or other program.  Therefore, these
   kind of restrictions should be considered advisory at best (and
   reinforced by policy).
```
