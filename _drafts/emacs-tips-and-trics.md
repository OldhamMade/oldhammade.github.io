## Search/Replace across files/buffers

Firstly, open all the files you want to search/replace across. Then, issue the following:

`M-x ibuffer RET t U`

This will select all open buffers. You can use `u`/`m` to (un)mark buffers as you see fit, then hit `U` to perform a regexp replace across the marked buffers.

`C-h m` will provide help for ibuffer, if you want to see what other options are available.
