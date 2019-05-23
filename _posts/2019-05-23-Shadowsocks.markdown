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
> sudo nano /etc/shadowsocks_config/shadowsocks.json  

This command will open the file if exists, otherwise it will be created.

Next, copy and paste those commands into this **shadowsocks.json** file, see parameters documentation below.
> {
  "server":"my_server_ip", 
  "local_address": "127.0.0.1",
  "local_port":1080,
  "server_port":my_server_port,
  "password":"my_password",
  "timeout":300,
  "method":"aes-256-cfb"
}

Parameter | Explanations
----------|-------------
server | your VPS's IP address
local_address | leave it as default
local_port  |  leave it as default
server_port |  put an available port as long as it is free, normally, 8388 is used
password  | as name suggests, just give password as string
timeout  | leave the default value 300 there
method  | use the default method *aes-256-cfb*

## Run the shadowsocks application

Run in the foreground:
> ssserver -c /etc/shadowsocks_config/shadowsocks.json

**OR** Run in the background (The recommend way):
To start:
>ssserver -c /etc/shadowsocks.json -d start

And to stop:
>ssserver -c /etc/shadowsocks.json -d stop

To check if the application is running, simly using command:
> pgrep ssserver

If there is a process id returned, usually a number, then should be okay.

However, the shadowsocks application might crash for no reason, or the VPS needs to be rebooted
sometime, to make your life easier, we can set the application as a server, 
whenever the application is not running, it will be restarted, and the OS will take care it for you 7*24. 
See next section. 

:stuck_out_tongue_winking_eye:
 
## Config the application as a system service

Create a *service* file under the path **/etc/systemd/system/**, let's name it *shadowsocks.service*
> nano /etc/systemd/system/shadowsocks.service

Then copy and paste the following lines into the file, remember to adapt the **ExecStart** parameter to your own 
*shadowsocks.json* file path.

>[Unit]
Description=Shadowsocks Server
After=network.target
[Service]
ExecStart=/usr/local/bin/ssserver -c /etc/shadowsocks_config/shadowsocks.json
Restart=always
[Install]
WantedBy=multi-user.target

Now, run the following commands to take effect and start the service:

> systemctl enable shadowsocks-server
systemctl start shadowsocks-server

------------------------------------
SUCCESS!
:beach_umbrella:
