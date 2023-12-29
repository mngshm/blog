+++
title = 'Christmas Night With Tmp Files'
date = 2023-12-26T01:36:25+05:30
draft = false
+++

This is a blog that will help me always remember that checking the command twice before running is the best way to not lead towards any fuck ups on a Linux machine. and also to give me trauma even ahead in the future. 

### I noticed tmp files 

I was working on some things inside the terminal and I noticed that there are a lot of temporary files with names ~/.bash_history-some id.tmp. I thought that these files must've got created when I left my laptop idle today yesterday (24 December 2023) from 2:00 to 4:36 PM because that was the time when I slept out of the blue on my chair. After I woke up I found that the laptop battery was dead to 4% and it was on suspend mode. So, I did a force reboot as pressing the power button wasn't turning it on because of less battery. 

After that, I found these files in my home directory. I tried deleting them but they weren't getting deleted. Why? because I was no more the user of those files. 

![temp files](/tmpfiles.png)

It was very ironic looking at this output, it basically said that someone called `users`. And continuing ahead I noticed that I was no longer the owner of my whole home directory itself. At this moment, I was thinking that today is going to be fun and hectic because I would be able to learn a lot while fixing this issue. (And indeed i learned a very big lesson)

![user was the owner](/perms.png)

I was talking with some of telegram friends at the same time discussing this with them. And one of my friend after asking told me the reason why these temporary files were getting created. And, according to him it was 

>bash wasn't able to append command history to ~/.bash_history due to messed-up permissions 

which I was pretty much not expecting because there was nothing inside these directories and I had no clue of this until he told me this because my ~/.bash_history was still getting rewritten with a newer set of commands which I was running. 

I wanted to know exactly when all of these files were getting created. I quickly did an ```ls -lrtha ~/.*tmp*``` and I saw that these files were getting created from November 5, 2023, If this was a hack then there would've been a specific time or event listener when these files were getting created but it was nothing like that. And common no hacker would make a plan to make empty tmp files in the home directory of a user. (I forgot to take a screenshot of the output of -lrtha).   

All of us were expecting that I had downloaded some wrong scripts and ran them in my home directory, but god damn I do not remember downloading anything other than CSV files, a couple of mp3/mp4's, some flac, and images (could've been a source tho). But it was nothing like that 

The suspicious actor in the whole drama was the user group ```users```. To everyone, I said that I did not run that command, because when I had done ```cat ~/.bash_history | grep -i "users"``` and I found nothing relevant.

### Users
I ran ``` ls -lrtha /home``` and there as well the owner of this home partition of my home directory was users. All of friends showed me the output with their home directories owned by ``` user:group```. But it was me who had it as ```users:users``` and I was like "god damn tf is happening". After checking out with ```groups``` command the output was in the following way

> `input users wheel`

Of course, it wasn't like I wanted it to be. I with the help of my friends tried investigating everything we could and that was the moment when [cyberknight](https://cyberknight777.dev) popped up asking me to check if there was something relevant to ```users``` in the ~/.bash_history of my root user. 

And Yes, I eventually ran this command back in the past: 
![my bad](/image_000.png)

It was the moment, when I was feeling very dumb and they were apparently laughing. I was finally fed up of myself now (P.S: I was already a lot stressed from 1-2 days before that) and this turned out to be the moment that was like a cherry on top of it. 

### The Fix 
As of now, I came up with the idea that all I have to do is to create a new usergroup with the name mangesh and add my user mangesh to it. And again take back the ownership of my /home/mangesh directory. I did that, after doing this I took ownership of all the tmp files in my home directory and removed them and this time it worked. This might be the temporary fix, but I want to temporarily fix this on purpose because, this way I can check for more issues that can come ahead because of users and permissions. 

Apparently, according to me I was supposed to run the users command with some different parameters and for different user or in a chroot environment. But, I ran it in my local system itself. That's why I thought could've gone wrong. I don't remember exactly why I ran that command.

### Realization 
Down the lane, this issue was a great help to me from a positive perspective. I learned a lot of new commands and flags and did a lot of searching on the internet. 

And, every moment I had the realization that Linux is so great that it gives me the freedom to peek and capture every moment of myself. Windows would've never given me the freedom to see when temporary files were getting created into my system or when I ran the command. I learned a lot of lessons (which I don't want to reveal), and I will fix all my mistakes from now on.
