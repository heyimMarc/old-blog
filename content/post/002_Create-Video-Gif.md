---
title: "Licecap für bessere Bugtickets"
showSocial: false
coverMeta: out
date: 2017-09-20
categories:
- tools
tags:
- tools
- productive
---

Wie man mit Licecap Bildschirmvideos aufnimmt und bessere Bugtickets erzeugt.

<!--more-->

Licecap ist ein Tool zum erstellen von Bildschirmaufnamen, die anschließend in ein animiertes Gif konvertiert werden und somit einfach in ein Ticket Tool wie zum Beispiel Jira geposted werden können. 

{{< image classes="fancybox fig-100" src="/img/video-gif/licecap.jpg" thumbnail="/img/video-gif/licecap.jpg" >}}

Licecap ist sehr einfach gehalten da es nur 2 Buttons besitzt. Einen um die Aufnahme zu starten und einen zum stoppen.

Ich habe ein ähnliches Tool heute im Sprint Review durch einen Kollegen gesehen und werde Licecap nun beim erzeugen von Bugtickets nutzen, da ein Video häufig deutlich Aussagekräftiger ist wie Text der für sich alleine steht. Das schöne an animierten Gif's ist das kein eingebetteter Videoplayer genutzt werden muss, sondern nativ funktioniert. In Jira reicht es das Gif als Anhang an das Ticket zu hängen, es wird beim öffnen des Tickets direkt abgespielt.

Das Resultat sieht dann so aus:

{{< image classes="fancybox fig-100" src="/img/video-gif/licecap_example.gif" thumbnail="/img/video-gif/licecap_example.gif" >}}

Licecap findet ihr [hier:](https://www.cockos.com/licecap/)

oder falls ihr Mac User seid, könnt ihr euch Licecap auch über Brew installieren.
```bash
$ brew cask install licecap
```