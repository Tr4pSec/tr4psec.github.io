# Troubleshooting boot times in Linux

My Linux Mint installation took forever to boot one day, and I had to figure out how to solve it. 
This is what I found:

You can run ``` systemd-analyze ``` to see startup information: 
<img src="https://raw.githubusercontent.com/Tr4pSec/tr4psec.github.io/master/.pictures/Screenshot%20from%202023-01-07%2020-00-17.png">

You can also run ``` systemd-analyze blame ``` to see what took the most time.

<img src="https://raw.githubusercontent.com/Tr4pSec/tr4psec.github.io/master/.pictures/Screenshot%20from%202023-01-07%2020-01-39.png">

The ``` systemctl ``` command showed me an error about a service failing.

In my case there was a service called ``` systemd-udev-settle ``` that loaded forever until it failed. 

I searched online and found out that this service wasn't needed for the system to run. So I found a command to "disable it": ``` sudo systemctl mask systemd-udev-settle ```

This fixed my super long boot time 👍