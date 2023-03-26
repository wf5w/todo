# todo
simple todo list  for command line, using ruby

# INSTALLATION:

the ruby language is required
no special gems are required, they should already be part of your default ruby

# SETUP:

todo will default to use ~/Documents/todos/todos.xit, but if you would like
a different directory, then provide the TODO_DIRECTORY environment variable
in your .bashrc file.

TODO_DIRECTORY="Documents/todos"

# SUMMARY:

This simple todo command, conforms to (roughly) the xit specification
found in github: https://github.com/jotaen/xit/blob/main/Specification.md 
 
todo command summary:
 
$ todo -h

All commands: will have an implied -f $TODO_DIRECOTORY/todos.xit UNLESS 
              otherwise specified with a -f filename.xit

add a todo list item: $ todo some new description text

print all todos (-f todos.xit is implied): $ todo 

print all todos .. searching for text: todo -p /some text

print all todos ... that are still open: todo -p open

print all todos ... that are closed: todo -p closed

mark an item done: $ todo -x ID

mark an item open (from previously done): $ todo -X ID

edit the todos via your editor: $ todo -e
(the environment variable EDITOR will be used, or nano)

# EXAMPLES:

$ todo -h
```
usage: todo [options] [arguments]

    todo with no options and arguments, prints entire list


    -x, --done ID                    mark item ID as done
    -X, --open ID                    mark item ID as open
    -f, --filename FILENAME          use filename instead of default todos.xit
    -e, --edit                       open todo list in editor
    -p, --print {[open|closed]}      todo print open or closed
    -h                               help
```

the following examples use this todos.xit file (~/Documents/todos/todos.xit):

```
[x] this is item 1
[ ] this is item 2
[x] this is a closed item 3
[ ] open item after a closed item
[ ] add this item at the end
[x] final thought
    an additional line for the final thought
    #todofinal -> 2023/04

ham radio todo items
[ ] do prep for nanoVNA
[ ] prepare for POTA
[x] put feet on icom 7300
```

$ todo
```
[x] this is item 1 (ID = 0)
[ ] this is item 2 (ID = 1)
[x] this is a closed item 3 (ID = 2)
[ ] open item after a closed item (ID = 3)
[ ] add this item at the end (ID = 4)
[x] final thought (ID = 5)
    an additional line for the final thought
    #todofinal -> 2023/04

ham radio todo items
[ ] do prep for nanoVNA (ID = 6)
[ ] prepare for POTA (ID = 7)
[x] put feet on icom 7300 (ID = 8)
```

mark ID 4 as closed

$ todo -x 4

mark ID 5 as open

$ todo -X 4

$ todo -p closed
```
[x] this is item 1 (ID = 0)
[x] this is a closed item 3 (ID = 2)
[x] final thought (ID = 5)
    an additional line for the final thought
    #todofinal -> 2023/04
[x] put feet on icom 7300 (ID = 8)
```

# TIPS:

If you want separate todo lists just supply the filename in the -f option

so, if you routinely, use separate todo lists, just add an alias for each one

$ alias hrtodo="todo -f hamradio.xit"

$ alias ptodo="todo -f personal.xit"

$ alias wtodo="todo -f work.xit"

$ alias p1todo="todo -f project1.work.xit"

## Use the same todos directory on multiple linux clients

let say you have a todos directory (in ~/Documents/todos) on your server machine
that you want to be able to access on your client.

here is how to do that:
* create a passwordless ssh from your client to your server, and test it
* install sshfs if it is not already installed
* edit /etc/fuse.conf and uncomment user_allow_other
* mount your server todos directory to your local client mount point

remote: ~/Documents/todos/ 

local: create a mount point (~/Documents/todos)

$ sshfs user@remote_machine:/home/user/Documents/todos/ ~/Documents/todos

once you have this working, then look at this to set it up on fstab:
see https://ubuntuforums.org/showthread.php?t=430312 for explanation

