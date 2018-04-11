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

# Use cases

## Interactive shell

Let's say you have a backup script that deletes the old directory before backing up:
```
rm -rf $HOME/backups
```
If you run this script normally it will delete the directory without asking any question:
```
$ ./run-backup.sh
> backup start...
> done.
```
This is great for running the script as a `cron` job or any automated process. But when you run it manually you want to be warned.

You install [safe][1] and add an alias in your `.bashrc` to make `rm` safe:
```
$ alias rm='safe rm'
```
Now, you can run the script again but this time you will be warned first:
```
$ bash -i ./run-backup.sh
> backup start...
> Are you sure you want to 'rm -rf /home/alexar/backups'? [y/n]
```

# @TODO
- Write about usecases. (it does have very interesting and useful usecases)
- Write `unsafe`
- Allow for environmental variables.
- Make sure it does not go into infinite loop if is used as an alias.

[1]: https://github.com/pendashteh/safe

