# Find if content exists in some file

## Simple Search
Lets say we have to sarch if pluign exists in `~/.bashrc` file, then we can use

```bash
grep -r plugin  ~/.bashrc
```

the output is 

```bash title="output"
/Users/amar/.bashrc:# Which plugins would you like to load? (plugins can be found in ~/.oh-my-bash/plugins/*)
/Users/amar/.bashrc:# Custom plugins may be added to ~/.oh-my-bash/custom/plugins/
```


## Recursive Search

```bash
grep -R "domain" /etc/apache2/httpd.conf

# (1)
/etc/apache2/httpd.conf:# as error documents.  e.g. admin@your-domain.com 
```

1. Output of the grep command

## Finding exact text

!!! info ""
    Lets imagine we have a file named `file.txt` with below contents
 
```bash title="File contents"
$ cat file.txt 

Ottawa
is
an 
awesome
place
places
to
too
live
```

Below will find all words which have `to`

```bash title="Simple search"
$ grep to file.txt 

to
too
```

Finding the exact `to`

```bash title="Find exact text"
$grep -w to file.txt 

to
```