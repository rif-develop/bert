# Bert

Bert is a very simple download manager written for the Raspberry Pi (or any other embedded Linux device). 

![Screenshot of the web interface](/screenshot.png?raw=true "Screenshot of the web interface currently downloading the latest Kernel version")

Use case: I often need to download large files which I don't want to download via my computer since it bothers me having a process which can't interrupted by accident or on purpose. The Raspberry Pi is near the router and can download all the day without disturbing anybody or anything.

Bert uses `wget` and some other linux command line tools (e.g. `du`, `df`) as backend. NodeJS provides the server and application logic and invokes `wget` through some wrapper object and parses it output. 

[Click here to read more about Bert on my blog!](http://maxstrauch.github.io/2016/01/08/bert-downloads-it.html)

# Features

 - Simple
 - The web interface proivdes an easy way to add or monitor downloads
 - Queue behaviour: only one download active download at a time
 - Run user script from web interface (very useful to copy the downloaded files from the `downloads/` folder to an USB thumb drive without `ssh` into the Pi)
 - Clear the downloads folder from web interface
 - Shutdown server from web interface
 - Detection of downloading the same file multiple times

# Run it!

You can run it by simply invoking

	node server.js

I have created a `cron` entry in my Pi with `crontab -e` by adding the line `@reboot /bin/bash --login /home/pi/script.sh > /home/pi/work.log` which will excute a special script on reboot. `/home/pi/script.sh` contains the following:

	#!/bin/sh
	sleep 120
	(/usr/local/bin/node server.js > out.log) &

I don't know why there is a `sleep 120` anymore. But you all know the rule: never change a running system!

The configuration is done in the first 32 lines of `server.js` - each parameter is documented there.

# License

Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0). Click [here](http://creativecommons.org/licenses/by-sa/4.0/) for details. The license applies to the entire source code.

`This program is distributed WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.`

# Trivia

I'm a huge fan of NCIS. Guess who Bert is ... 

![Bert](/www/logo.png?raw=true)

