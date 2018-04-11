# safe
It asks you again whatever it is in your mind, just in case. 

# Usage

```
$ safe [shell command and its arguments]
```

# Examples
```
$ safe rm /var/log/backup*
> Are you sure you want to 'rm backups backups_old'? [y/n]
```

Tip: notice that it replaces * with what SHELL interprets it as. In this case `backup* --> backups backups_old`

```
$ safe dd if=/path/to/old/image of=/dev/sda
> Are you sure you want to 'dd if=/path/to/old/image of=/dev/sda'? [y/n]
```

# @TODO
- Write about usecases. (it does have very interesting and useful usecases)
- Write `unsafe`
- Allow for environmental variables.
- Make sure it does not go into infinite loop if is used as an alias.

