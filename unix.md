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
