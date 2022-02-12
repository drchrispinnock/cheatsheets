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
## Navigating

To set the current address to a line number, specific the number. Ed will
print the line.

```
2
This is line 2
```

To print lines n -> m use the comma notation. If n is omitted, the beginning
of the file is assumed. If m is omitted, the end of the file is assumed.

```
2,3p
This is line 2
Welcome
,2p
This is a line
This is line 2
2,p
This is line 2
,p
This is a line
This is line 2
Welcome
```

So to append after line 2, nagivate there and use a.

```
2
This is line 2
a
put this between line 2 & 3
.
,p
This is a line
This is line 2
put this between line 2 & 3
Welcome
```

To insert before line 2, use i

```
2
This is line 2
i
put this before 2
.
,p
This is a line
put this before 2
This is line 2
put this between line 2 & 3
Welcome
```





## References

[Ed] Ed Mastery: The **Standard** Unix Text Editor, Michael W. Lucas, Tilted Windmill Press, 2018.
