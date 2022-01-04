Amazon Cloud Application that collects data 24/7 on Amazon AWS Cloud, involving lots of AWS & Linux configuration.

The AWS service of choice was EC2. The database choice was SQLite inside the instance/EBS, which should cut down on Write Cost units

The largest challenge of this app was to really make sure the Python Script inside was running 24/7, because sometimes memory leaks crop in one of the imported Python libraries which ruin the CPU Utilization.

Fortunately there was CloudWatch & CloudWatch alarms that did a Status Instance check every 5 minutes, and it even came with an ACTION to automatically REBOOT when the Instance check failed, so that's activated.

Despite this setup, I detected that sometimes the script inside called "Cloud.py" still isn't running after the reboot.

I did a Cron Job as a Python Script that would check if the script was running with "ps -a", and if it wasn't, then start it, and if multiple copies were running, then remove the processes except for one.

I had some severe problems with the CronJob for a while, then I discovered that people should NOT use the squiggly line/symbol as "Home" inside the cron entry through "crontab -e" (or /etc/cron.d), but rather the FULL path retrieved from "pwd" without the ~ symbol. I learned hours the hard way.

The star of the show is the "Screen" application in Linux, that was what I used. Screen allows processes to start when there is no active SSH connection going! According to the internet, "Screen or GNU Screen is a terminal multiplexer. In other words, it means that you can start a screen session and then open any number of windows (virtual terminals) inside that session. Processes running in Screen will continue to run when their window is not visible even if you get disconnected"

I'll describe more about this in the future, or you can ask me!
