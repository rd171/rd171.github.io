---
layout: post
title:  "ubuntu-ubuntu突然不能上网"
date:   2020-1-16 19:00:00 +0200
categories: ubuntu
---

```
sudo service network-manager stop
sudo rm /var/lib/NetworkManager/NetworkManager.state
sudo service network-manager start
```
