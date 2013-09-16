## "How Can SSH+SCP Improve My Love Life?"  
_A Guide Perpetrated by The Computer Science Major's Committee;_  
_Authored by Dan Barella_  

So you've heard of this mysterious and slightly tantalizing set of commands that may or may not begin with an 's'. Perhaps you're intrigued by the possibility to **WORK ON YOUR OWN PERSONAL COMPUTER** and then **AUTOMAGICALLY TRANSFER YOUR FILES TO OCCS TO HAND THEM IN** – all from the cozy comfort of your twin extra long bed? Well we're here to help!  

`ssh` and `scp` are commands that you run on the terminal. The `s` prefix just means `secure`.


- `ssh` means _secure shell_, with _shell_ referencing the terminal. On OCCS we run the `bash` shell.
- `scp` means _secure copy_, where `cp` references the UNIX copy utility.  

These commands let you transfer files to your OCCS account, and then drive around your OCCS account as if you were working on a lab machine. You can do this from *any* UNIX machine, not just your own.  

--- 

###SSH

You'll use `ssh` to log into your OCCS account remotely. You just need to run the command:  

	ssh <your_username>@cs.oberlin.edu
	
The terminal will ask for your password. When you type it in, there will be no response – don't worry, the terminal is still receiving your text, it's just being a paranoid parakeet.   

Once you've logged in, it's pretty much identical to working on a lab machine except **Don't run commands like** `komodo <filename> &` **because your computer will attempt to install komodo over the network, which will be slow and lame.**  

Think of this as a way to remotely hand in files. It's not so much a way to edit your files, unless you know how to use `nano`, `vim`, `emacs`, etc. in which case you probably know what this guide is telling you already.

####Example  

	ssh dbarella@cs.oberlin.edu
	Password: 
	Last login: Sun Sep 15 23:55:18 2013 from 132.162.89.59
	Sun Microsystems Inc.   SunOS 5.10      Generic January 2005
	< dbarella@occs >ls
	cs150        cs151        cs210        cs241        cs275        Desktop      Documents    Downloads    mail         mbox         Music        OCCSWindows  Pictures     Public       Templates    Videos       workshop     www
	< dbarella@occs >cd cs241/
	< dbarella@occs >ls     
	hw1
	< dbarella@occs >handin -c 241 -a 1 hw1
	<bla bla bla>
	Handin of hw1 successful.  Thank you dbarella!
	< dbarella@occs >logout

And we're done!



