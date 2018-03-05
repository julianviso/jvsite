---
title: "Discord Bot Project and More"
author: Julian Viso
layout: post
tags: [blog]
---

Another year, another domain renewal notification, another blog post. By now it's a running habit that around this time of the year this site will receive a few updates. 2017 was met with a lot of highs and a lot of lows. To quickly recap,

*   I met an amazing person in the summer of 2017.
*   I grew a lot spiritually. I did my first communion and confirmation as a Catholic since my last blog post.
*   I got in quite possibly the best shape of my life.
*   I learned typescript and more web oriented languages
*   I'm finally looking at colleges again to start getting my masters degree in Computer Science 

Unfortunately there were also some lows for the past year, however there's no need to discuss that. More importantly, I've recently started a new mini project which has surprisingly received a decent reception. 

Last December at my work we had a week long hackathon where you could spend time away from work focusing on learning anything that interested you. I've been curious to learn Swift and IOS development, so I took the time to learn a little IOS dev via tutorials. Near the end of the hackathon I decided it would be interesting to create an IOS app for a game that I sometimes play (Guild Wars 2) which calls the game's API and fetches some data for the user. The hackathon ended before I had time to fully create the app however, and then the holidays happened which killed off that project.

Fast forward to last week, and I decided it would be interesting to port some of the code that I had written for my app idea to a discord bot. I had never created any bots for discord previously, and was unsure how difficult it would be to create one. It turned out to be extremely simple with the basics being the following lines of code for python.

```
import discord
from discord.ext import commands

bot = commands.Bot(command_prefix='-', description='Help Description here')
bot.run('generated_token')
```

In order to create an actual command you simply have to add an ```@bot.command()``` to any functions that you create.

After porting over my code to a discord bot, I had several users message me expressing interest in my bot, and requesting extra features added to it. I decided that I needed some way to keep the bot running 24/7 since I didn't want to leave my python script running constantly on my laptop, so decided to finally take advantage of an old gen 1 model B raspberry pi I've had sitting around for almost a year. I set the raspberry pi to always run in the background my python program and whenever it gets reboot it launches the program on startup.

This was my first time getting to play with a raspberry pi, and I did encounter certain difficulties getting everything in my pi's environment set up to work well. The main issues that I ran into were having to install python 3.6 on the pi, and launching my program on startup.

On my raspberry pi I had python 3.2 initially installed, however I needed python 3.4 or greater to work with ```discord.py.``` I ended up having to completely make python 3.6. To do this run the following commands.

```
sudo apt-get install build-essential checkinstall
sudo apt-get install libreadline-gplv2-dev libncursesw5-dev libssl-dev libsqlite3-dev tk-dev libgdbm-dev libc6-dev libbz2-dev

cd /usr/src
sudo -s
bash configure
make altinstall
exit
```

By using make altinstall you avoid replacing the default python binary files in /usr/bin/python.

Now in order to create a startup script for my raspberry pi I had to look up a little bit about crontabs. A crontab is essentially a background process that allows executing scripts at specific times. I set mine to where on reboot it would launch my python program so that whenever I update my bot I can lazily tell my raspberry pi to reboot rather than relaunching the program myself. To do this was quite simple after finding a helpful guide on stackoverflow, here are the steps.

*   Make a launcher script
*   Make your launcher script executable (chmod 755)
*   Add the script to your crontab
*   Sit back and watch your program run

Creating the shell script is simple enough. The crontab however may be something that users aren't too certain of how to do so here are the steps for that.

```
sudo crontab -e //Brings up the crontab window
@reboot sh /home/pi/repos/launcher.sh //or wherever you place your shell script
```

Currently I intend to continue adding more features as they get requested to my bot. As of this moment about 150-200 users are able to use it in a discord server (which is 147 more users than what I was originally expecting), so it has been pretty exciting. Once this project dies in terms of activity, I will probably go back to experimenting with IOS as a hobby. It's still on my list of ToDos...
