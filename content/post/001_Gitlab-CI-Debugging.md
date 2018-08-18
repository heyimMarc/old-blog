---
title: "Gitlab CI Debugging"
showSocial: false
coverMeta: out
date: 2017-08-29
categories:
- programming
tags:
- Gitlab
- debugging
---

Ich möchte hier kurz zeigen wie mittels Gitlab CI ein CI Prozess lokal debugged werden kann.

Häufig sehe ich bei Neuanlage von Projekten ein Feuerwerk von fehlgeschlagenen Gitlab CI Test. Dabei ist es ganz einfach, den CI Prozess vorab lokal zu testen bevor dieser in das Repo gepushed wird.

<!--more-->

Zunächst setze ich ein installiertes Docker voraus, das findet ihr [hier:](https://www.docker.com/get-docker)

Außerdem benötigt ihr ein GIT Projekt und das zugehörige [.gitlab-ci.yml](https://docs.gitlab.com/ce/ci/quick_start/README.html) welches euren CI Prozess definiert. 

# Das GitlabCI Dashboard

Das Dashboard ist Teil von Gitlab und kann durch folgende Aktionen gesteuert werden:
- git push zu deinem Gitlab Server
- über das Web Interface
- über Gitlab Webhooks
- über Gitlab Crons

Das Dashboard ist allerdings nur ein Webinterface, es führt nicht die CI Prozesse aus, sonder delegiert diese an einen Pool von Runnern. Wenn das Dashboard die Anweisung bekommt eine Pipeline zu starten, fügt es diese Pipeline einer Warteschlange hinzu. Die Warteschlange (Queue) wird von den Runen, dann abgearbeitet.

# Der Gitlab Runner

Die Runner selbst sind Prozesse die auf beliebigen Instanzen gestartet werden können. Klassischerweise registrieren die Runner sich von alleine bei der angegebenen Gitlab Instanz.

Die Runner können mit Namen und Tags versehen werden, erhalten ihre Instruktionen vom Gitlab Dashboard und Reporten das Ergebnis zurück.

GitlabCI Runner können auch ohne eine Verbindung zur Gitlab CI Instanz arbeiten. Im Offline Modus, ist die Funktionalität zwar limitiert, aber es möglich das lokale .gitlab-ci.yml auszulesen und sogar auszuführen. Offline Runner müssen allerdings via Kommandozeile ausgeführt werden.

# Installation des Gitlab Runners

In meinen Fall führe ich die Installation für Mac OS aus, hier verlinke ich aber nochmal die [offizielle Dokumentation](https://docs.gitlab.com/runner/install/osx.html#installation) welche auch andere Betriebssysteme unterstützt. 

Es ist auch möglich den Runner direkt über Docker zu starten [siehe.](https://hub.docker.com/r/gitlab/gitlab-runner/)

```bash
$ sudo curl --output /usr/local/bin/gitlab-ci-multi-runner https://gitlab-ci-multi-runner-downloads.s3.amazonaws.com/latest/binaries/gitlab-ci-multi-runner-darwin-amd64
```

```Bash
$ sudo chmod +x /usr/local/bin/gitlab-ci-multi-runner
```

# Testen der Gitlab Runner Installation
```Bash
$ gitlab-ci-multi-runner
```

sollte folgendes anzeigen:

{{< image classes="fancybox fig-100" src="/img/ci-debugging/05561FD7-FE82-4A7B-8E92-E8C10828DADF.jpg" thumbnail="/img/ci-debugging/05561FD7-FE82-4A7B-8E92-E8C10828DADF.jpg" >}}

# Ein Job mittels Gitlab Runner laufen lassen

Als Beispiel .gitlab-ci.yml nehme ich folgendes file:

```
image: node:latest

task1:
  script:
    - npm install
    - npm test
```

Task1 lässt sich nun folgendermaßen ausführen:

```
$ cd path/to/project
$ ls .gitlab-ci.yml
.gitlab-ci.yml
$ gitlab-ci-multi-runner exec docker task1
```

Nun sollte der Prozess laufen, klar Gitlab Cache und Artefakte werden beim lokalen Gitlab Runner nicht funktionieren, aber allein die Möglichkeit ein CI File lokal schnell ausführen und debuggen zu können ohne Teammitglieder des Projektes mittels fehlgeschlagener Pipelines zu benachrichtigen ist Gold wert, ganz zu Schweigen von der ersparten Zeit.