# siphon
`siphon` is a simple program for automatically moving files from one machine to another over ssh.

I often find myself with in a situation where files are generated on one computer, but need to be moved to another computer before they can be used. I got tired of configuring tools like [btsync](https://www.getsync.com/) and [Dropbox](https://www.dropbox.com/), which are clearly overkill for this type of problem, so I wrote `siphon`. 
  
`siphon` is simple. It moves files from one directory to another. Directories can be on the same machine or on different machines. Any new file that appears in the source directory will automatically be moved by `siphon` to the destination directory. `siphon` checks for new files in the source directory at a periodic rate. The default check rate is 60 seconds.

## Using siphon:

Using `siphon` is very similiar to using `scp`. Below are some possible uses for siphon:

```
$ siphon -h
Usage: siphon [-h?ndt] [username@hostname:]/path/to/source [[username@hostname:]/path/to/destination]
Options: -t time interval in seconds to wait between copying new files
         -d delete remote files after copying
         -n disable color output
         -h print usage
         -D show debug prints
```

Copy any new files that appear on a remote machine to a directory on the host machine; check for new files every 10 seconds:

```
$ ./siphon -t 10 username@MyRemoteMachine.com:/home/username/myfiles ~/myfiles
```

Don't use port 22 for `ssh`? No problem:

```
$ ./siphon -t 10 username@MyRemoteMachine.com:98765/home/username/myfiles ~/myfiles
```
Copy any new files from a remote machine, but delete them off the remote machine after they are copied:

```
$ ./siphon -d -t 25 username@MyRemoteMachine.com:/files/to/copy/and/then/delete
```

Copy any new files that appear on a remote machine to the current directory on the host machine:

```
$ ./siphon username@MyRemoteMachine.com:/home/username/myfiles
```

Copy any new files that appear on a local machine to a remote machine:

```
$ ./siphon ~/myfiles username@MyRemoteMachine.com/home/username/myfiles 
```

Copy any new files that appear in one directory to another on a local machine:

```
$ ./siphon /path/to/dir1 /path/to/dir2 
```

Run `siphon` in the background while copying its output to a log:

```
$ ./siphon -n username@MyRemoteMachine.com:/home/username/myfiles ~/myfiles >> siphon.log &
```


    
