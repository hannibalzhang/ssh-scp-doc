# "How Can SSH+SCP Improve My Life Energy?"  
_A Guide Perpetrated by The Computer Science Major's Committee;_  
_Authored by Dan Barella and Eli Rose_  

Are you intrigued by the possibility of **WORKING ON YOUR OWN PERSONAL COMPUTER** and then **AUTOMAGICALLY TRANSFERRING YOUR FILES TO OCCS TO HAND THEM IN** – all from the cozy comfort of your twin extra long bed? Well we're here to help!  

--- 

## SSH
`ssh` is a command that you run on the terminal which allows you to log in to your OCCS account remotely. The `s` prefix just means `secure`.

- `ssh` means _secure shell_, with `sh` referencing the _terminal shell_. On OCCS we run the `bash` shell, though there are many shells like `zsh`, `csh`, `tcsh`, bla bla bla.

This command essentially lets you drive around your OCCS account as if you were working on a lab machine. You can do this from *any* UNIX machine, not just your own.  

This is the syntax to use `ssh`:  

	ssh your_username@cs.oberlin.edu
	
Where `your_username` is your OCCS account username.

The terminal will ask for your password. When you type it in, you won't see anything being typed on the screen – don't worry, the terminal is still receiving your text, it's just not showing it cuz it's a paranoid panda.  

### Example – Logging in to OCCS

	Dan-Macbook-Pro:~ Dan$ ssh dbarella@cs.oberlin.edu
	Password: 
	Last login: Sun Sep 15 23:55:18 2013 from 132.162.89.59
	Sun Microsystems Inc.   SunOS 5.10      Generic January 2005
	< dbarella@occs >

Now we're logged in. Notice where the terminal prompt changes from `Dan-Macbook-Pro:~ Dan$` to `< dbarella@occs >`. The first prompt is the prompt on my laptop, the second is what's configured on the OCCS server.  

At this point it's pretty much identical to working on a lab machine except *programs which open other windows won't work*. So commands like `komodo <filename> &` won't work. At this point let's not worry about editing files, just about handing them in.

### Example – Remote handin over SSH  
Continuing from before, where I'm already logged into OCCS:

	< dbarella@occs >ls     
	hw1
	< dbarella@occs >handin -c 241 -a 1 hw1
	<bla bla bla>
	Handin of hw1 successful.  Thank you dbarella!
	< dbarella@occs >logout
	Dan-Macbook-Pro:~ Dan$ ls
	SSH and SCP.md

Here I'm showing an assignment handin, but I could also make some directories, copy files around, etc. When I `logout`, the connection is closed, the prompt changes back to my local terminal, and everything is good again. To make sure I'm home, I run `ls` which shows only `SSH and SCP.md`, instead of all my OCCS class folders.  

### Review
Think of `ssh` as a way to move around and do stuff on OCCS, like to remotely hand in files – It's not such a great way to work on files, unless you know how to use a terminal-based text editor like `nano`, `vim`, `emacs`, etc. It's usually much easier to work on your code locally (on your computer), then transfer them to OCCS and use `ssh` to hand them in. How to do the transfer part? That's where we'll need to use...  

---  

## SCP  

`scp` is a command-line program which lets you transfer files between computers over the internet. BTDubs this command is completely separate from `ssh` -- _you don't need to ssh into OCCS to use scp_

This is the syntax to use `scp`:  

	scp file your_username@cs.oberlin.edu:
	
Where  
- `file` is a file in the current directory  
- `your_username` is your OCCS account username  
-  The `:` is *VERY IMPORTANT!*. This tells `scp` to send the file to the server.  

### Example 1 – Transferring armadillos.txt to my OCCS account  
I want to transfer a file, `armadillos.txt` to my OCCS account. So that I can have armadillos. On my account.

	Dan-Macbook-Pro:~ Dan$ ls
	armadillos.txt
	scp armadillos.txt dbarella@cs.oberlin.edu:
	armadillos.txt                                100%    0     0.0KB/s   00:00

We have now transferred the file to my account on the server. Let's `ssh` in to see if it's there

	

#TODO
- `destination` is a directory on your OCCS account.  
