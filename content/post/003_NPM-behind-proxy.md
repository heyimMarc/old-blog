---
title: "Node.js und NPM trotz Unternehmensproxy verwenden"
showSocial: false
coverMeta: out
date: 2017-10-25
categories:
- programming
tags:
- tools
- npm
- nodejs
---

Node.js und npm trotz Unternehmensproxy verwenden.

<!--more-->

Für diejenigen, die wie ich teilweise über einen Proxy ins Internet müssen, kann gerade die Verwendung von Nodes Paketmanager npm ein richtiger Kampf werden. Anfangs habe ich gedacht, dass sich der Proxy wie üblich in der Linuxwelt über die Umgebungsvariablen ```HTTP_PROXY``` und ```HTTPS_PROXY```konfigurieren lässt. Leider falsch gedacht...

So wünscht sich npm die Proxy konfiguration:

BASH
```bash
npm config set proxy http://proxy.de:8080
npm config set https-proxy http://proxy.de:8080
```