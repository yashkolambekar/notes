## Basics

We intialise a github repository in the folder using

```console
git init
```

We can check the status of file changes using 

```console
git status
```

To add files to the staged commit, we have to do

```console
git add file.txt
```

We can replace `file.txt` with `.` for it to add all the files in the root and children

To send the files outside of the staging area we can do 

```console
git stash
````

all the files will be gone to backstage, and once we are done with all the things that we want to do in the staging area and we need those files that we sent in the backstage we can do

```console
git stash pop
```

To clear the stash, we can do clear but it is removed permanently.

```console
git stash clear
```

