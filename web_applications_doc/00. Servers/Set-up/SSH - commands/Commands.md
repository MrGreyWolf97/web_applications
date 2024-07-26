[Add environments variables to profile](https://unix.stackexchange.com/questions/26047/how-to-correctly-add-a-path-to-path)
1. edit `~/.profile` file
2. Add the following to append the new PATH
```bash
PATH=$PATH:<directory-absolute-path>/bin
```
3. Log-in again

> [!warning] Didn't work to set visualvm as part of the $PATH variable

---
