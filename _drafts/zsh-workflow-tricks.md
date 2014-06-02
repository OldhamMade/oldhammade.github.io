`!!` retrieves the last command.

`CRTL-r` allows you to search history and insert/execute at the prompt.

`ESC-.` inserts the last argument of the previous history line, repeat to go back in history.

`ESC-'` quotes the whole line. (Useful for su -c or ssh).

`ESC-RETURN` inserts a literal newline, so you can edit longer commands easily.

Moving around

`cd` alone will take you back to your home folder.

`cd -` will move back to the previous folder.

You can omit `cd` and just type `..` to jump up a directory. `...` will jump up 2 directories.

You can also change to a similar directory by using `cd {old} {new}`. For example, if you are in ~/dev/myproject1/src/lib/, and you want to cd to ~/dev/myproject2/src/lib/, all you need to do is: `cd 1 2`
