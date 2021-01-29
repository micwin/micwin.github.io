---
layout: post
title:  "So etwas wie Sicherheit gibt es nicht."
date:   2021-01-29 00:00 +0200
categories: meta
---
Zugegeben, wir reden von IT-Sicherheit, also die Sicherheit, dass meine Daten, meine Computer oder ganz allgemein mein Netz sicher sind oder, wie auch oft formuliert, *hinreichend* sicher.

Und den Gedanken könnt ihr gleich mal streichen. Warum?

## Flak vs. Point Defense

Der Stoßrichtung meiner Argumentation ist die Unmöglichkeit, [Angriffsvektoren](https://de.wikipedia.org/wiki/Angriffsvektor) vorherzusagen, oder auch nur hinreichend einzuschränken. Es gibt einfach zu viele  Variablen und mögliche Motivationen, sich genau euer Netz, euren Computer, euer Handy herauszusuchen. Lasst mich das anhand meines Lieblingsbeispiels _WhatsApp_ erläutern.

*WhatsApp* ist ein sogenannter Messenger, d.h. ein Tool, um es einer Person zu erlauben, Nachrichten zu einer anderen Person zu schicken in einer einigermassen vertraulichen Umgebung. Der letzte Halbsatz ist wichtig, denn genau darin besteht der Unterschied zwischen WhatsApp und z.B. IRC, oder Twitter: Bei WhatsApp kann nicht jeder mitlesen, bei IRC/Twitter grundsätzlich schon. Wieso genau diese Sache dann letztendlich unsere Rettung ist, erkläre ich weiter unten.

Inwiewiet ist Vertraulichkeit gleich Sicherheit? Ist WhatsApp deshalb *sicher*? oder wenigstens *hinreichend* sicher?

Dafür müssen wir uns dann fragen: wie sicher wollen wir es denn? Was bedeutet für mich oder dich Sicherheit? Macht es dir etwas aus wenn Facebook weiss was du Onkel Otto schreibst? Oder deiner Liebhaberin von der deine Frau nichts wissen soll? Willst du dass der Staat grundsätzlich mitlesen kann, oder bestehst du auf unbedingt und verfassungsmässige, unverletzliche Privatsphäre? Du siehst, es gibt unendlich viele Varianten, den zu den obigen Themen hat fast jeder eine eigene Meinung, oder verlässt sich auf einen "common sense".

Klar, niemand will, dass intime Liebesbotschaften im Internet landen. Und ja, WhatsApp und Facebook geben sich sicher viel Mühe, dass genau das nicht passiert. Aber auch dort sitzen keine Götter, was die Pannen, die ja selbst bei so branchenriesen wie FaceBook oder iCloud immer wieder beweisen.

Zurück zu den Angriffsvektoren. Bei WhatsApp gibt es mindestens folgende Angriffsvektoren:

## Angriffsvektoren

1) Das Endggerät. Jemand könnte auf deinem oder dem Gerät eines Kontaktes  Schadsoftware installieren und mitlesen was du bei WhatsApp so eingibst. Und es sind schon viele Apps bekannt, die mit einer [Backdoor](https://de.wikipedia.org/wiki/Backdoor) ausgestattet sind.

2) Der App-Shop. Auch Google ist nicht perfekt und so schlüpft immer mal wieder eine Schadsoftware in den App Store bei Google und Apple. Interessante wäre einmal eine Aussage o.g. Firmen, wie oft sie eigentlich Software mit Namen ablehnen, die so ähnlich wie WhatsApp klingen, z.B. WhatApp, WahtsApp, WhatsAp oder solche, die so tun als seien sie offiziell von WhatsApp herausgebracht, z.B. WhatsApp Companion, WhatsApp Tool, WhatsHome.

3) Das Betriebssystem. Wie jede Software ist auch Android bzw. iOS fehleranfällig und wenn sich in das Betriebssystem ein Backdoor einschleicht (weil man als Entwickler eben auch nicht jeden Code auf Lücken prüfen kann).

4) der Server. WhatsApp ist eine Server-Anwendung. Das bedeutet, bei WhatsApp im Keller stehen Computer, die mit der bei dir installierten WhatsApp-Anwendung sprechen, alle Daten bekommen und die Nachrichten dann weiterleiten. Diese Server sind auch eine Kombination aus Hardware und Software und somit für obige Angriffsvektoren anfällig

5) Die Infrastruktur zwischen den Servern und der App. Deine Nachrichten an Onkel Otto werden über Netzwerk-Kabel, Router, Firewalls und Jump Points weitergeleitet, von denen jederwieder ein Angriffsvektor für sich darstellt.

6) Die Mitarbeiterschaft des Herstellers, also diejenige Leute, die dein Gerät, deinen App Store, dein Betriebssyystem, den Server und/oder die Infrastruktur am Besten kennen. Diese können erpresst werden, oder gierig werden, oder auch einfach aus bestem Treu und Glauben Hintertüren einbauen um die Software besser testen zu können (und  diese dann ganz oder teilweise vergessen rauszunehmen).

Aber können wir nicht wenigstens mit Software und Schulung das Risiko auf ein überschaubares oder bzw. ertragbares Maß reduzieren?  

## Die Unheilige Dreifaltigkeit

1) man kann sich mit Software und Schulung (Und auch Hardware, sogenannte Security-Appliances) ) nur gegen *bekannte oder spekulative* Angriffsvektoren schützen, also Vektoren, über die wir wenigstens etwas wissen oder vermuten, nicht gegen *unbekannte*. Und Angriffsvektoren entstehen jeden Tag aufs Neue; neue Hard- und Software kommt zum Einsatz; neue Leute arbeiten in der Firma, die Technologie macht einen Sprung nach vorne und schon sind Massnahmen wieder nutzlos und müssen überdacht werden. Dabei hilft es auch nicht, das einmal für die Gesellschaft als Ganzes zu durchdenken denn Angriffsvektoren sind oft (nicht immer!) sehr speziell und sehr persönlich.

2) Solange es Beute gibt, gibt es Jäger. Und auch die Jäger lernen dazu.

3) Das Gesetz der grossen Zahlen. Es gibt inzwischen viel zu viele talentierte [Grey- und Blackhats](https://de.wikipedia.org/wiki/Hacker_(Computersicherheit)#White-,_Grey-_und_Black-Hats) da draussen und viele davon sitzen in unerreichbaren Juristidktionen, oder kämpfen ums überleben. Wie motiviert bist du eine IBM zu hacken oder ein paar Bitcoins zu ziehen wenn du in Somalia am Hungertuch nagst und der grosse Warlord droht dich kaltzumachen? Oder würdest du dich wirklich wehren wenn dein Boss dir beim Kaffeetrinken beiläufig in den Kopf setzt, mal die Web-Seite eures grössten Konkurrenten auf [XSS-Vulnerabilität](https://de.wikipedia.org/wiki/Cross-Site-Scripting) abzuklopfen?

Also, wie bekommen wir die Sicherheit, die wir uns wünschen?

Gar nicht. Denn keiner bekommt genug Geld, um es *für uns* zu machen. Wir müssen das selbst in die Hand nehmen.

Also, wie wär's? Hier meine Vermutungen, oder Anregungen, die das Ergebnis vieler Jahre in der IT-Branche sind:

## Setze konsequent auf Open Source

Ja, Open Source liegt für Hacker quasi nackig auf dem OP-Tisch und Closed Source hört sich in dieser Hinsicht sicherer an. Security by Obscurity, richtig?

Aber für die White Hats eben auch. White Hats sind Hacker, die mit wenig oder ohne Entgeld, quasi aus Leidenschaft und als Hobby, Software hacken um sie *sicherer* zu machen. Sie sind sozusagen die Bürgerwehr der IT. Und von denen gibt es Millionen. Wenn also eine Open Source mal ein paar Jahre draussen ist und einigermassen Beliebtheit erlangt hat, kannst du sicher sein dass schon mal ein paar White Hats drüber geschaut haben und  die Software recht sicher ist.

Bei Closed Source sieht das anders aus. Ja, zu Beginn ist die Sicherheit bei einer neuen, kommerziellen Software höher da (vermutlich!) gleich von Anfang an mehr Leute am Thema Sicherheit sitzen (und die Blackhats keine Ahnung vom Code haben); aber es sind eben immer dieselben, drehen sich im Kreis und einige haben vielleicht auch gar keine Lust immer denselben Code zu reviewen. Ich will nicht sagen dass jeder bezahlte Sicherheitsexperte schlechter ist als ein x-beliebiger Freiwillige; aber ich denke, wenn du für deine Freizeit nicht bezahlt wirst, machst du eher das Beste draus. Und vermutlich ist der Anteil der frustrierten mit innerer Kündigung bei den bezahlten Sicherheitsexperten vergleichbar mit dem Schnitt der Gesellschaft?!? Mach dir einfach eines klar: Closed-Source-Software analysiert man gegen Geld oder um sie auszunutzen; open source Software auch, aber es kommen noch die vielen leidenschaftlichen Freeiwilligen *dazu*.

Das aus dem Weg, was bedeutet das?

- Firefox/Chromium statt Edge/IE/Safari/Chrome (Chrome != Chromium)
- Linux/OpenBSD/FreeBSD statt Windows/MacOS
- matrix.org statt WhatsApp/Threema/Telegram/

Und es ist wichtig dass du das überall konsequent durchziehst, also 

* das Endgerät: Bei Handy und Tablet sollte das ein Android-Derivat sein; am besten Stock, ohne Provider-Tools oder Bloatware; bei Laptop oder Desktop solltest du auf Linux (Ubuntu?), BSD o.ä. setzen; 

* der App-Store: sollte auch als Open Source vorliegen, beim Android-Phone also FDroid, bei den Linux-Rechznern ist das schon eingebaut mit apt, yum, pacman etc.

* die Apps, die du verwendest: Nimm auf Android doch FairMail, K9 und wie sie alle heissen, statt Gmail; nimm Element statt WhatsApp, Signal und Threema. Und stell auch sicher dass diese selbst auch nur Open Source, z.B. für ihren Server, einsetzen. Wenn du das nicht herausfindst dann vielleicht deshalb weil sie etwas zu verbergen haben. Das ist auch der Grund warum ich Signal und Threema *nicht* zu den sicheren Tools zähle: Die CLients sind Open Source; das Protokoll ist Open Source; aber die Server, die sind es nicht.

## Lern dich in den Computer-Kram ein

Für Nicht-ITler ist der ganze Computerkram echt hart. Die Weichheit einer freudigen Diskussion mit dem Nachbarn weicht der digitalen Rücksichtslosigkeit von in Eisen gebrannten, anscheinend unsichtbaren Regeln. Und warum stellt die Kiste auch immer diese Fragen? Ich will doch nur einen Brief schreiben?!?

Ehrlich, das geht die nächsten Jahre nicht weg und wird immer schlimmer. Was du jetzt gelernt hat musst du in 5 Jahren nicht mehr lernen und vielleicht weisst du ja schon was?

## Computer-Nerds möchten auch nur zeigen was sie können

Vielleicht hast du einen dieser introvertierten, pupertierenden Computer-Fuzzies in deiner Nachbarschaft der immer so komisch guckt und unmögliche Klamotten anhat? Ja das ist natürlich der Volltreffer. Sprich ihn an, bitte ihn um Hilfe! Er will helfen, versprochen. Er hat nur Angst ausgelacht zu werden, und die Angst musst du ihm nehmen. Trau dich!

## Es geht nicht nur dir so

Da draussen sind viele Leute denen die Materie Angst macht. Such sie. Schlage Treffen vor um das Thema gemeinsam zu erforschen.

## Lass den Admin deiner Firma seinen Job machen

Das ist sein Job, nicht sein Hobby. Lass ihn *seinen Job* machen. Deine privaten IT-Probleme sind *dein* Job, kümmer  dich selbst drum. Es mag verlocken den kompetenten IT-Profi zu fragen aber in Echt: möchtest du in deiner Freizeit auf deinen Job angesprochen werden? Sicher, ein paarmal; aber auf regelmässiger Basis? 

Und? Was machst du jetzt? Ist dir die Sicherheit den Aufwand wert oder darf WhatsApp, Google und Microsoft weiter zuhören?

Lass uns reden, du erreichst mich unter [@micwin:matrix.org](https://matrix.to/#/@micwin:matrix.org)