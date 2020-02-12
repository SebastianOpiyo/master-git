# GIT PLUBMING & PORCELAIN

What is Git in real sense? 
- It is a Content-addressable file system with a VCS user interface on top of it.
- the more user friendly commands are called `porcelain commands` whereas the low-level commands designed to be chained together in UNIX-style or called from scripts are called `plumbing commands`. 

# Plumbing Commands
- Give you access to the inner workings of git, and help demo why and how git does what it does.
- Most of these commands are meant to be used as building blocks for new tools and custom scripts.

# HERE WE GO ----> .git 
- this folder is the heart of git.
- to initialize it we `[git init]`
- cd .git
- ls -F1

ls
cd > The content you expect to see include the following from a fresh .git repo
	. config
	. description
	. HEAD
	. hooks/
	. info/
	. objects
	. refs/
> Note: depending on the version of git you might see additional content.

1. DESCRIPTIONS
- Used by GitWeb program - a web client of git showing git repos.

2. CONFIG - Contains your project specific configurations

3. INFO - keeps a global exclude file for ignored patterns that you don't want to track in `.gitignore` file. 

4. HOOKS - contains your client or server-side hooks scripts. look at git hooks

- The remaining form the core parts of git i.e the index, HEAD, Objects and refs. 

* Objects - stores all the contents of your db
* Refs - stores pointers into commit objects in the data (branches, tags, remotes etc.)
* HEAD - points to the branch you currently have checked out
* index - where git stores your staging area information

# GIT INTERNALS
[ Git Objects ]
- Git is a content addressable filesystem --> at the core of git is the a simple key-value data store.

* Commands
> git hash-object
$ git init test && cd test
$ find .git/objects
$ find .git/objects -type f
> we can use the `git hash-object` to create a new data object and manually store it in a Git db.
$echo 'test content' | git hash-object -w stdin
- this string of commands returns a SHA-1 hash value.
- to see how git has stored your data:
$find .git/objects -type f

- To see the content of the file
$ git cat-file -p <hash>

- git doesn't store your files, only the content in form of `blob` objects
- thaso find out the type of object from a hash value run:
$git cat-file -t <hash>


# Tree Object 
- Content is store in UNIX like file structure but much simpler
- content is stored in tree and blob objects
$ git cat-file -p branch-name^{tree}

> Note: Trees are created by staging some files.

- you can manually create a tree using the plumbing command `git update-index` 
- `--add` --> to set up a staging area and include the file.
- `cacheinfo` because the file is not in the directory but in the db
- meaning of mode numbers:
> 100644 normal file
> 100755 executable file
> 120000 specifies a symbolic link

$ echo 'new file' > new.txt
$ git update-index --add --cacheinfo 100644 \
  1f7a7a472abf3dd9643fd615f6da379c4acb3e3a test.txt
$ git update-index --add new.txt

- Now you can write the changes
$ git write-tree

# Commit Objects
$ echo 'first commit' | git commit-tree d8329f
fdf4fc3344e67ab068f836878b6c4951e3b15f3d

- confirm the commit
$ git cat-file -p fdf4fc3
tree d8329fc1cc938780ffdd9f94e0d364e0ea74f579
author Scott Chacon <schacon@gmail.com> 1243040974 -0700
committer Scott Chacon <schacon@gmail.com> 1243040974 -0700

first commit

- Next, you’ll write the other two commit objects, each referencing the commit that came directly before it:

$ echo 'second commit' | git commit-tree 0155eb -p fdf4fc3
cac0cab538b970a37ea1e769cbbde608743bc96d
$ echo 'third commit'  | git commit-tree 3c4e9c -p cac0cab
1a410efbd13591db07496601ebc7a059dd55cfe9

# To see the log history
- run it on the last SHA
$ git log --stat 1a410e


# REFS
- Stores the files that contain the SHA-1 values
- Helps you not to remember every SHA-1 value.

- Manually add a ref
$ echo 1a410efbd13591db07496601ebc7a059dd55cfe9 > .git/refs/heads/master 
$ git log --pretty=oneline master

- You are not encouraged to directly edit this file but you can use the git safe way:
$ git update-ref refs/heads/master 1a410efbd13591db07496601ebc7a059dd55cfe9

--> When you run `$ git update-ref` this equates to running `branch`


# Git HEAD
- SHA-1 of the last commit
The HEAD is a symbolic link to the branch you are currently on.


