# pam internals 

```
required
failure of such a PAM will ultimately lead to the PAM-API returning failure but only after the remaining stacked modules (for this service and type) have been invoked

requisite
like required, however, in the case that such a module returns a failure, control is directly returned to the application.

sufficient
success of such a module is enough to satisfy the authentication requirements of the stack of modules (if a prior required module has failed the success of this one is ignored). A failure of this module is not deemed as fatal to satisfying the application that this type has succeeded. If the module succeeds the PAM framework returns success to the application immediately without trying any other modules.
```

## Explanation

```
If an item marked sufficient succeeds, the PAM library stops processing that stack. This happens whether there were previous required items or not. At this point, PAM returns the current state: success if no previous required item failed, otherwise denied.

Similarly, if an item marked requisite fails, the PAM library stops processing and returns a failure. At that point, it's irrelevant whether a previous required item failed.

In other words, required doesn't necessarily cause the whole stack to be processed. It only means to keep going.
```

  * https://unix.stackexchange.com/questions/106131/pam-required-and-sufficient-control-flag
