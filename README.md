# safe
It asks you again whatever it is in your mind, just in case. 

# Usage

```
$ safe [shell command and its arguments]
```

# Examples
```
$ safe rm /var/log/backup*
> rm backups backups_old
Are you sure? y|n
```

Tip: notice that it replaces * with what SHELL interprets it as. In this case `backup* --> backups backups_old`

```
$ safe dd if=/path/to/old/image of=/dev/sda
> dd if=/path/to/old/image of=/dev/sda
Are you sure? y|n
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
backup start...
done.
```
This is great for running the script as a `cron` job or any automated process. But when you run it manually you want to be warned.

You install [safe][1] and add an alias in your `.bashrc` to make `rm` safe:
```
$ alias rm='safe rm'
```
Now, you can run the script again but this time you will be warned first:
```
$ bash -i ./run-backup.sh
backup start...
> rm -rf /home/user/backups
Are you sure? y|n
```

## Parameter expansion
All parameters passed to `safe` are expanded. In other words, paths containing wildcards will be expanded to a list of correspanding files and directories. This is particularly helpfule when `safe` used with `rm`.
```
$ alias rm='safe rm'
```
When deleting the test images you may notice a test audio which was not intended to be deleted.
```
$ rm test*
> rm test test_000.png test_001.png test-0.png test-1.png testaudio.mp3
Are you sure? y|n n
Ok, moving on. They say, better to be safe than sorry.
$ rm test*png
> rm test test_000.png test_001.png test-0.png test-1.png
Are you sure? y|n y
Alright.
```

# @TODO
- Write about usecases. (it does have very interesting and useful usecases)
- Write `unsafe`
- Allow for environmental variables.
- Make sure it does not go into infinite loop if is used as an alias.

[1]: https://github.com/pendashteh/safe

