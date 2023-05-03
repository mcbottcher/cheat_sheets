# UNIX

## List of Commands

- `cd` : Change Directory
  - `cd` itself will default to the home DIR
  - `cd -` takes you back to the previous directory you were at

- `pwd` : print the directory you are in

- `whoami` : prints current user

- `wc`: get file size info
  - `wc -c unix.md` : Get number of bytes of file
  - `wc -l unix.md` : Get number of lines of file

- `diff`: Compares two files
  - `diff -y <file1> <file2>`: Outputs diff of file1 and file2 side-by-side

- `find`: Find a file
  - `find . -name "*.py"`: Finds all .py files from current directory and down

- `tree`: Shows files in tree display

- `printenv`: Print environment variables

- `curl`: cURL lets us query URLs from the command line
  - `curl www.google.com`: Returns HTML/Scripts of google.com
  - option `-i` gives information header
  - option `-d or --data` can be used to post data to a url
    - `curl -d "first=Bob&last=Ross" http://<url>`
  - pass in username and password: `curl -u <username>:<password> <url>`
  - Download response e.g. picture: `curl -o test.jpg <url>` -> outputs response to test.jpg

- `grep`: Search for word or expression in a file
  - `grep "expression" <file>`
  - Use `-i` to search for expression without being case sensitive
  - Can use it with pipe: `cat my_file.txt | grep "hello world"`
  - Use with extended regualar expressions: `grep -E 'pattern1|pattern2' fileName`
    - Or regular grep:
      - `grep 'pattern1\|pattern2' fileName`
      - `grep -e 'pattern1' -e 'pattern2' fileName`
  - Use `-c` to get a count of number of grep matches
  - Can also search multiple files: `grep -c 'warning\|error' /var/log/*log` -> Searches all log files...
    - Use the -R flag to recursivly search subdirectories too

- `uname`: prints system info
