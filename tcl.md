# TCL scripting

## List of Commands

- `info commands`: List of all commands interpreter knows

- `puts`: Output a string to standard output device
  - `puts "Hello world"`
  - `puts {Hello world}`

- `set`: Assignment command
  - `set my_var Mikkel`
  - `set my_var $Mikkel` 

- `expr`: Command for doing math type operations
  - Enclose expression in curly braces for correct evaluation and faster code
  - `eq, ne`: Ensures that values are regarded as strings as a pose to `==` or `!=`
  - `in, ni`: Is string in a list or not


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

- `if` statements
  - "no" and "yes" can also be used as the test expression
  - Expression can be enclosed in braces or quotes. Quotes do an extra round of substitution and should be avoided


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
