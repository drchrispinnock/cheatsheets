# ed cheatsheet

## Starting ed

To start with an empty buffer, simply:

```
% ed
```

To edit a file, specify the filename. If the file doesn't exist, ed will
complain but will use the filename for subsequent writes unless told 
otherwise.

```
% ed haddock
haddock: No such file or directory
a
test
.
w
5
q
```

To change the prompt from being empty, use -p

```
% ed -p'% ' haddock
5
% p
test
% q
```

## Writing and exiting

w <file> - to write out to a file
w - will write to the file (provided the filename is previously specified)
q - quit (will not quit if the file is unwritten, q again to confirm)
Q - quit regardless
wq - write and quit

## Commands to input or append text

i - insert before the current line (does not work on an empty file)
a - append after the current line

For both, use a single full stop on its own on a line to finish. e.g.

```
a
This is the text segment.
.
```




## References

[Ed] Ed Mastery: The **Standard** Unix Text Editor, Michael W. Lucas, Tilted Windmill Press, 2018.
