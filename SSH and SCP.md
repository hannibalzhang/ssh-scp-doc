# "How Can SSH+SCP Improve My Life Energy?"  
_A Guide Perpetrated by The Computer Science Major's Committee;_  
_Authored by Dan Barella_  

So you've heard of this mysterious and slightly tantalizing set of commands that begin with an 's'. Perhaps you're intrigued by the possibility to **WORK ON YOUR OWN PERSONAL COMPUTER** and then **AUTOMAGICALLY TRANSFER YOUR FILES TO OCCS TO HAND THEM IN** – all from the cozy comfort of your twin extra long bed? Well we're here to help!  

`ssh` and `scp` are commands that you run on the terminal. The `s` prefix just means `secure`.

- `ssh` means _secure shell_, with `sh` referencing the _terminal shell_. On OCCS we run the `bash` shell, though there are many shells like `zsh`, `csh`, `tcsh`, bla bla bla.
- `scp` means _secure copy_, where `cp` references the UNIX copy utility.  

These commands let you transfer files to your OCCS account, and then drive around your OCCS account as if you were working on a lab machine. You can do this from *any* UNIX machine, not just your own.  

--- 

## SSH

You'll use `ssh` to log into your OCCS account remotely. This is the syntax:  

	ssh <your_username>@cs.oberlin.edu
	
The terminal will ask for your password. When you type it in, you won't see anything being typed on the screen – don't worry, the terminal is still receiving your text, it's just not showing it cuz it's a paranoid panda.  

### Example – Logging in to OCCS

	: [Dan – 0: CSMC [master *]] ; ssh dbarella@cs.oberlin.edu
	Password: 
	Last login: Sun Sep 15 23:55:18 2013 from 132.162.89.59
	Sun Microsystems Inc.   SunOS 5.10      Generic January 2005
	< dbarella@occs >

Now we're logged in. Notice where the terminal prompt changes from `: [Dan – 0: CSMC [master *]] ; ` to `< dbarella@occs >`. The first prompt is the one I've configured on my laptop, the second is what's configured on the OCCS server.  

At this point it's pretty much identical to working on a lab machine except **commands like** `komodo <filename> &` **won't work.** At this point let's not worry about editing files, just about handing them in.

### Example – Remote handin over SSH
Continuing from before, where I'm already logged into OCCS:

	< dbarella@occs >ls  # On the OCCS server
	cs150        cs151        cs210        cs241        cs275        Desktop      Documents    Downloads    mail         mbox         Music        OCCSWindows  Pictures     Public       Templates    Videos       workshop     www
	< dbarella@occs >cd cs241/
	< dbarella@occs >ls     
	hw1
	< dbarella@occs >handin -c 241 -a 1 hw1
	<bla bla bla>
	Handin of hw1 successful.  Thank you dbarella!
	< dbarella@occs >logout
	: [Dan – 1: CSMC [master *]] ; ls  # Now I'm back on my computer
	SSH and SCP.md

Here I'm showing an assignment handin, but I could also make some directories, copy files around, etc. When I `logout`, the connection is closed, the prompt changes back to my local terminal, and everything is good again. To make sure I'm home, I run `ls` which shows only `SSH and SCP.md`, instead of all my OCCS class folders.  

### Review
Think of `ssh` as a way to move around and do stuff on OCCS, like to remotely hand in files – It's not such a great way to work on files, unless you know how to use a terminal-based text editor like `nano`, `vim`, `emacs`, etc. It's usually much easier to work on your code locally (on your computer), then transfer them to OCCS and use `ssh` to hand them in. How to do the transfer part? That's where we'll need to use...  

---  

## SCP
