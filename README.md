# siphon
A simple script for automatically moving files from one machine to another over ssh.

I often find myself with in a situation where files are generated on one computer, 
but need to be moved to another computer before they can be used. I got tired of 
configuring tools [btsync](https://www.getsync.com/) and [Dropbox](https://www.dropbox.com/), which are clearly overkill for this type of 
problem, so I wrote `siphon`. 
  
`siphon` is simple. It moves files from one directory to another. Directories 
can be on the same machine or on different machines. Any new file that appears in the source directory will 
automatically be moved by `siphon` to the destination directory. `siphon` checks 
for new files in the source directory at a periodic rate.
