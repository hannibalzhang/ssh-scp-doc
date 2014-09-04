# "How Can SSH+SCP Improve My Life Energy?"  
_A Guide Perpetrated by The Computer Science Major's Committee;_  
_Authored by Dan Barella and Eli Rose_  

Are you intrigued by the possibility of **WORKING ON YOUR OWN PERSONAL COMPUTER** and then **AUTOMAGICALLY TRANSFERRING YOUR FILES TO OCCS TO HAND THEM IN** – all from the cozy comfort of your twin extra long bed? Well we're here to help!  

--- 

## SSH
`ssh` is a command that you run on the terminal which allows you to log in to your OCCS account remotely. The `s` prefix just means `secure`.

- `ssh` means _secure shell_. Roughly, a _terminal_ or _console_ is the window that you type commands (like `cd` and `ls`) into, while a shell is the program running inside this window. The shell is responsible for taking your commands and doing something with them. On OCCS we run the `bash` shell, though there are many shells like `zsh`, `csh`, `tcsh`, bla bla bla.

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
	< dbarella@occs >handin -c 150 -a 1 hw1
	<bla bla bla>
	Handin of hw1 successful.  Thank you dbarella!
	< dbarella@occs >logout
	Dan-Macbook-Pro:~ Dan$ ls
	SSH and SCP.md

Notice that I ran `handin -c 241 -a 1 hw1` instead of just `handin`. (Those letters with dashes in front of them are called _command-line arguments_. `-c` is followed by the class number, which here is 150, and `-a` is followed by the assignment number, which here is 1. The thing we're handing in, `hw1` is the last one, and is preceded by no letter. In general, command-line arguments are a way to give information to a program you're running from the shell. Here, they serve as a way to tell `handin` our class and assignment numbers all at once. We could have gotten the same thing done just by typing `handin` and then entering our class and assignment number ordinarily. This is just the "cool" way to do it, like riding your bike without handlebars.)

These particular command-line arguments are specific to `handin`. Another program might not have a `-c` argument, or it might have a `-c` argument that does something completely different. 

Here I'm showing an assignment handin, but I could also make some directories, copy files around, etc. When I `logout`, the connection is closed, the prompt changes back to my local terminal, and everything is good again. To make sure I'm home, I run `ls` which shows only `SSH and SCP.md` (this file! hey!), instead of all my OCCS class folders.

### Review
Think of `ssh` as a way to move around and do stuff on OCCS, like to remotely hand in files – It's not such a great way to work on files, unless you know how to use a terminal-based text editor like `nano`, `vim`, `emacs`, etc. It's usually much easier to work on your code locally (on your computer), then transfer it to OCCS and use `ssh` to hand them in. How to do the transfer part? You've got options. If you like doing things by the command line, use `scp` (coming up next). If you don't, skip the next section and we'll talk about other options.

#TODO
- More non-command-line options. What do Windows people use?

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

	Dan-Macbook-Pro:~ Dan$ ssh dbarella@cs.oberlin.edu
	Password: 
	Last login: Sun Sep 15 23:55:18 2013 from 132.162.89.59
	Sun Microsystems Inc.   SunOS 5.10      Generic January 2005
	< dbarella@occs > ls
	Desktop    Downloads  OCCSWindows  Public     Videos
	Documents  Music      Pictures     Templates  www
	armadillos.txt

If you don't have exactly the same folders (`Desktop`, `Public`, etc.) don't worry about it. All that matters is that `armadillos.txt` is there. That means our `scp` worked. Now we can run `handin` to hand our assignment in, just like we did above.

### More SCP
- You can specify a destination in your OCCS account where you want to send the files. Just put it after the `:`. For example, `scp armadillos.txt dbarella@cs.oberlin.edu:cs150` would copy `armadillos.txt` to your account's `cs150` folder (if there is one). You can put a whole file path here too: `scp armadillos.txt dbarella@cs.oberlin.edu:cs150/lab01` will copy it to the lab01 folder inside the cs150 folder.
- The `-r` command-line option copies entire directory. So the command `scp -r lab01 dbarella@cs.oberlin.edu:` will copy the folder named `lab01` from the current directory to your occs account. Most of the time this is easier than copying every individual file. Actually, `-r` will copy individual files too, so it does the same thing, only better.
- `scp` can copy many files at once. Just list them all, like this: `scp file1.txt file2.txt dbarella@cs.oberlin.edu:`. 
