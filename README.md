# siphon
`siphon` is a simple program for automatically moving files from one machine to another over ssh.

I often find myself with in a situation where files are generated on one computer, but need to be moved to another computer before they can be used. I got tired of configuring tools like [btsync](https://www.getsync.com/) and [Dropbox](https://www.dropbox.com/), which are clearly overkill for this type of problem, so I wrote `siphon`. 
  
`siphon` is simple. It moves files from one directory to another. Directories can be on the same machine or on different machines. Any new file that appears in the source directory will automatically be moved by `siphon` to the destination directory. `siphon` checks for new files in the source directory at a periodic rate. The default check rate is 60 seconds.

Here is what using siphon looks like:

```
$ siphon -d -t 10 user@example.com:/home/user/files ~/files
[04-04-16 21:03:24]  Siphoning files from 'user@example.com:/home/user/files' to '/home/user/files'
[04-04-16 21:03:24]  Use ctrl+c to exit...
[04-04-16 21:03:27]  copying  dir1
[04-04-16 21:03:31]  copied   dir1
[04-04-16 21:03:31]  copying  dir2
[04-04-16 21:03:35]  copied   dir2
[04-04-16 21:03:35]  copying  file1
[04-04-16 21:03:38]  copied   file1
[04-04-16 21:03:38]  copying  file2
[04-04-16 21:03:42]  copied   file2
[04-04-16 21:03:42]  copying  file3
[04-04-16 21:03:46]  copied   file3
...
```

By default, `siphon` prints to the terminal using pretty colors. To disable this, use the `-n` option.

## Installation:

Clone this repository and add it to your path, or copy `siphon` to a location on your path.

`siphon` assumes that you already have passwordless login setup for any remote machine you intend to copy files to or from. To set up passwordless login see [here](http://www.linuxproblem.org/art_9.html) or run the `sshkeyexchange` script provided in `util/`:

```
$ sshkeyexchange user@example.com
```

`sshkeyexchange` will ask for the password to the remote machine twice before copying over the local machine's public key.

## Using `siphon`:

Using `siphon` is very similiar to using `scp`.

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
$ siphon -t 10 user@example.com:/home/user/files ~/files
```

Don't use port 22 for `ssh`? No problem:

```
$ siphon -t 10 user@example.com:98765/home/user/files ~/files
```

Copy any new files from a remote machine, but delete them off the remote machine after they are copied:

```
$ siphon -d -t 25 user@example.com:/files/to/copy/and/then/delete
```

Copy any new files that appear on a remote machine to the current directory on the host machine:

```
$ siphon user@example.com:/home/user/files
```

Copy any new files that appear on a local machine to a remote machine:

```
$ siphon ~/files user@example.com/home/user/files 
```

Copy any new files that appear in one directory to another on a local machine:

```
$ siphon /path/to/dir1 /path/to/dir2 
```

#####Run `siphon` in the background while copying its output to a log:

```
$ siphon -n user@example.com:/home/user/files ~/files >> siphon.log &
```


    
