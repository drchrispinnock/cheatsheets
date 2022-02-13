# ed cheatsheet

## Scope

This is a quick guide to *ed*, the original Unix line editor used by the folks to write Unix code and probably C. There were no monitors in those days! Please see [Ed] Ed Mastery for all the details in modern prose.

## Commands

```
# Writing the file to the stdout
,p		- output the file
,n		- output the file with line numbers
A,Bn 
A,Bp	- between lines A and B (0 beginning of file, $ end of file)
,pl		- for all above, l will add $ the end of line to see whitespace

# Editing, moving, deleting
a		- append at the current line
Aa		- append at line A
i		- insert before the current line
Ai		- insert before line A
c		- change the current line
Ac		- change line A
.		- exit editing mode

d   	- delete line
A   	- delete line A
A,Bd	- delete lines A to B

u		- undo previous (next undo is redo)

AmB		- move line A to after line B
AmB		

A,Bj	- join lines A to B to one line
AtB	    - copy line A to after line B
A,BtC	- copy lines A,B to after line B

# Files
Ar	file	- read file and append it after line A
W file    - "save as", save a copy of the file to file
A,BW file - save lines A to B to file

f file    - specify the filename for the current file
e file    - switch to editting file 
			  (complains if current buffer unsaved, second invocation overrides)
			
.= 	   - print number of lines in the file

# Bookmarks
kA		- bookmark the current line as A
'A		- go to the bookmark

# Escape to the shell

! cmd  - run command from inside ed
r ! cmd - insert the output of cmd to current line
Ar ! cmd - ... to after line A
w ! cmd - send the file to command
e ! cmd - start a new file with the output of command


```

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

To set the current line (also called the address) to a line number, specific the number. Ed will
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

Made a mistake at line 2? No problem - use c to change it. Without the number, change works on the current line.

```
2c
h
.
,n
1	This is a line
2	h
3	This is line 2
4	put this between line 2 & 3
5	Welcome
```

## More on addresses and bookmarks

Commands can be called with numbers to give them context. If A and B are
line numbers:

```
A,Bn  - writes the file between lines A and B with line numbers
A,Bp  - the same without line numbers
0,Bn  - from beginning to B
A,$n  - from A to the end
,n or ,p - prints the lot
```

Adding an l command (e.g. ,nl) will print a $ so that trailing space can be
seen.

To bookmark the current address with the letter a, use k:

```
ka
```

To go to the bookmark, use '

```
'a
```

Bookmarks move as the lines they mark move.

## Moving and deleting lines

To move lines around, use the m command. For example to move line 3 after line 1:

```
,n
1	This is a line
2	h
3	This is line 2
4	put this between line 2 & 3
5	Welcome
3m1
,n
1	This is a line
2	This is line 2
3	h
4	put this between line 2 & 3
5	Welcome
```

To delete lines, use d:

```
2,3d
,n
1	This is a line
2	put this between line 2 & 3
3	Welcome
```

## References

[Ed] Ed Mastery: The **Standard** Unix Text Editor, Michael W. Lucas, Tilted Windmill Press, 2018.
