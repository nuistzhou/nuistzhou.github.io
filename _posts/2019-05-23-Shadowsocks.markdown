---
layout:     post
title:      "Shadowsocks Server Tutorial"
subtitle:   " \"Technology\""
date:       2019-05-23 19:00:00
author:     "Ping"
header-img: "img/in-post/tutorial_pythonpath/post-head-python.jpg"
catalog: true
tags:
    - Tool
---
Environment: Ubuntu

## Install dependencies

```bash
apt-get install python-pip
pip install shadowsocks
```


## Configuration

Create the config file for the shadowsocks. 
Feel free to put the config file wherever you want, but recommend put it under the **/etc/**. 
Here just put it in directory **/etc/shadowsocks_config/shadowsocks.json**, the file name doesn't matter, as long as 
you know where to find it, because it will be used later as a parameter when run the *shadowsocks* command.   
```bash
sudo nano /etc/shadowsocks_config/shadowsocks.json  
```

This command will open the file if exists, otherwise it will be created.

Next, copy and paste those commands into this **shadowsocks.json** file, see parameters documentation below.
```json
{
  "server":"my_server_ip", 
  "local_address": "127.0.0.1",
  "local_port":1080,
  "server_port":my_server_port,
  "password":"my_password",
  "timeout":300,
  "method":"aes-256-cfb"
}
```

| Parameter | Explanations |
|----------|-------------|
| server | your VPS's IP address |
| local_address | leave it as default |
| local_port  |  leave it as default |
| server_port |  put an available port as long as it is free, normally, 8388 is used |
| password  | as name suggests, just give password as string |
| timeout  | leave the default value 300 there |
| method  | use the default method *aes-256-cfb* |

## Run the shadowsocks application

Run in the foreground:
```bash
ssserver -c /etc/shadowsocks_config/shadowsocks.json
```

**OR** Run in the background (The recommend way):   
To start:
```bash
ssserver -c /etc/shadowsocks.json -d start
```

And to stop:
```bash
ssserver -c /etc/shadowsocks.json -d stop
```

To check if the application is running, simly using command:
```bash
pgrep ssserver
```


If there is a process id returned, usually a number, then should be okay.

However, the shadowsocks application might crash for no reason, or the VPS needs to be rebooted
sometime, to make your life easier, we can set the application as a server, 
whenever the application is not running, it will be restarted, and the OS will take care it for you 7*24. 
See next section. 

:stuck_out_tongue_winking_eye:
 
## Config the application as a system service

Create a *service* file under the path **/etc/systemd/system/**, let's name it *shadowsocks.service*
```bash
nano /etc/systemd/system/shadowsocks.service
```

Then copy and paste the following lines into the file, remember to adapt the **ExecStart** parameter to your own 
*shadowsocks.json* file path.
```editorconfig
[Unit]
Description=Shadowsocks Server
After=network.target
[Service]
ExecStart=/usr/local/bin/ssserver -c /etc/shadowsocks_config/shadowsocks.json
Restart=always
[Install]
WantedBy=multi-user.target
```
Now, run the following commands to take effect and start the service:

```bash
systemctl enable shadowsocks-server
systemctl start shadowsocks-server
```

------------------------------------
SUCCESS!
:beach_umbrella:

I also tested the shadowsocks on the Digital Ocean VPS, however, the google scholar was not able to be accessed 
properly with the error info:   

> We are sorry, but your computer or network may be sending automated queries, to protect our users, we 
cannot process your request right now.

After google, I noticed it has been an issue back from year 2014 since a lot of people are using DO's VPS doing 
Web crawling and those IPV4 addresses from DO are blocked by Google...

Some users came up with a solution by forcing the Shadowsocks using the IPV6 address, like in this [post](https://www
.flyzy2005.com/tech/shadowsocks-google-scholar/).
Unfortunately, I was not able to make it. More investigation needs to be done in the future...

A friendly suggestion:    
> Avoid using popular VPS suppliers like DO, Linode, .etc. could low the similar risk.
