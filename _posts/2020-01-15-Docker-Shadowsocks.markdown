---
layout:     post
title:      "Run shadowsocks with Docker"
subtitle:   " \"\""
date:       2020-01-15 21:00:00
author:     "Ping"
header-img: "img/in-post/postgresql/postgresql.jpg"
catalog: true
tags:
    - VPN
---

Ubuntu 16.01 Minimal environment

1. Install the latest docker version
Steps [here](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-18-04)

2. Pull shadowsocks image and run  

```bash
docker pull oddrationale/docker-shadowsocks

# with server/local port as 2019 and replace the {pass} with your password
docker run --restart on-failure -d -p 2019:2019 oddrationale/docker-shadowsocks -s 0.0.0.0 -p 2019 -k {pass} -m aes-256-cfb

# check if container is running
docker ps -a
```

3. Download the shadowsocks client to connect. (Mac OS, Windows, Linux, IOS and Android)
Recommend **Wingy** on IOS and [ShadowsocksX-NG](https://github.com/shadowsocks/ShadowsocksX-NG) on Mac OS.
