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

given the following in your ~/Documents/todos/todos.xit:

 
