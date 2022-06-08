# TCL scripting

## List of Commands

- `info commands`: List of all commands interpreter knows

- `puts`: Output a string to standard output device
  - `puts "Hello world"`
  - `puts {Hello world}`

- `set`: Assignment command
  - `set my_var Mikkel`
  - `set my_var $Mikkel` 



## MISC

- Backslash sequences:
  - `\a`: Audible Bell
    - `puts \a`
  - `\b`: Backspace
  - `\f`: Clear Screen
  - `\n`: New line
  - `\r`: Carridge Return
  - `\t`: Tab
  - `\v`: Vertical Tab
  - `\0`: Octal number
  - `\u`: Unicode value
  - `\x`: Hex value

- Commands with `""`
  - Contents are substituted before use

- Commands with `{}`
  - The contents are not substituted before use
  - `puts {$my_var}  ->  "$my_var"`

- Command within `[]`
  - Replaced with result of execution of that command

- Using the value of a variable
  - `$my_var`

- Comments:
  - `# Comment at beginning of line`
  - `puts "Hello World" ;# Comment at end of line needs ';'`

## Useful Resources

- TCL Tutorial: https://www.tcl.tk/man/tcl8.5/tutorial/Tcl0a.html 
