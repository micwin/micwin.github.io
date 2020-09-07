---
layout: page
title: Pro Bono
permalink: /probono/
---

{:toc}

Hin und wieder kristallisiert sich in meiner täglichen Arbeit 
ein Problem heraus, das sich mit Software lösen lässt. Dann setze 
ich mich hin und code einfach was um exakt dieses Problem zu lösen.

Natürlich passt das nicht in meinen Lebenslauf und meine 
professionelle Projektliste, denn erstens bekomme ich dafür ja kein Geld und 
manche Leute würden sowas als Hobby einstufen, und da ich ja immer 
dazulerne, sind zweitens die meisten Projekte sowieso nie abgeschlossen. 

Dies hier ist also der Platz um diese meine Dinge unterzubringen.

## clici (ab 2020)

Ich arbeite nun schon einige Zeit als DevOps-Ingenieur; das bedeutet, 
ich erstelle und warte Skripte, die Software automatisch baut, testet 
und deployt. Dabei helfen mir sogenannte ci/cd-Server wie Jenkins, 
GitLab und Team Foundation Server. Allesamt sind dies mächtige Tools, 
mit meiner Meinung nach spezifischen und relevanten Unterschieden und Stärken; 
sie haben aber auch spezielle Schwächen, die mich hin und wieder in den Wahnsinn treiben:

- wenn man mit einer Bash-ähnlichen Sprache arbeiten will, dann geht das bei allen; 
allerdings eben nur eine bash-_ähnliche_ Sprache, die eben nicht ganz an bash dran ist; 
so unterscheiden sich z.B. die Piping-Mechanismen, der Umgang mit Exit-Codes, der 
Umgang mit special characters (schon mal probiert, sed oder grep in einem GitLab-CI-Task zu verwenden?),
die line separator, das comment handling,... und und und. 
Kurz und gut: du kannst nicht einfach ein ganz normales Bash-Skript automatisch von irgendwo mit cURL downloaden  und es 
als task in dein CI integrieren; es gibt noch vieles anzupassen und zu debuggen, mit all den 
Konsequenzen für das Updaten der Skripte,  wenn sie sich in der ursprünglichen Quelle geändert haben sollten. 
Wie mein Sohn zu sagen pflegt: Schmutz.

- Du kannst die Skripte nicht einfach so mal lokal auf deiner Kiste laufen lassen und so testen. 
Nein, wenn du Glück hast, hast du ein Linting-Programm oder eine Linting-Website, das/die dir die 
__syntaktische Korrektheit__ deines CI-Skripts testet. Wenn du kein Glück hast, musst du das Skript ändern, manchmal committen und 
hochladen, und erst wenn es läuft - weisst du dass es läuft. Und selbst wenn du einen Linter hast, heisst das ja nicht dass die Skripte dann automatisch laufen; 
committen und hochladen ist immer noch der ultimative Test.

- Versuch doch mal, denselben CI-Workflow auf zweierlei CI-Servern laufen zu lassen, sagen wir auf 
Microsoft Team Foundation Server  und Atlassian Bamboo. Es läuft darauf hinaus, dass du zweierlei Skripte entwickelst 
und maintainst. Das ist gar nicht mal so selten, z.B. wenn du dieselbe Codebase mit einem internen Jenkins einerseits 
und einem kundenbasierten Gitlab andererseits baust.

- Wechsel doch mal mit deinem extensiven, viele Teams umfassenden CI-Workflow von Jenkins nach GitLab. 
Lange Rede kurz: Vergiss es. Du wirst jedes einzelne Projekt übersetzen müssen. Ich nenne sowas Vendor 
Lock In. Was kein Ding wäre wenn das Tool okay wäre aber - naja, du kennst Jenkins. 
Das Chuck Norris -Plugin war mal witzig gemeint... muss ich noch weiter reden? 

Irgendwann ist mir einfach der Kragen geplatzt und ich habe [clici](https://metafence.gitlab.io/clici/) 
entwickelt:

- da wo bash läuft, läuft auch clici; also auch bei dir auf der lokalen Maschine, in der cygwin-Box, 
wenns denn sein muss, oder in einem Docker container
- du musst clici nicht installieren (obwohl clici dich dabei unterstützt), es gibt keine Abhängigkeiten 
ausser bash und which, und es ist lediglich ~ 8kb gross
- kooperiert mit jedem CI-Server
- dead simple
- zur Not kannst du auch python verwenden

Interessiert? Hier nochmal  der Link zur Homepage: [clici](https://metafence.gitlab.io/clici/)

## ssh-relais (2017)

Und irgendwann hatte ich auf einem Rechner mal Zugriff auf Docker, aber keine Möglichkeit, einen SSH-Demon zu installieren. 
Will sagen - ich musste mich per RDP auf einen Terminal Server einwählen, von dem aus es dann per Telnet(!) und ohne 
Root-Rechte weiterging. Grausig.

Also baute ich mir ein [docker image](https://github.com/micwin/ssh-relais) und veröffentlichte es auf 
[docker hub](https://hub.docker.com/repository/docker/outpost/ssh-relais) und was soll ich sagen - das ist das bisher 
bei weitem Nützlichste meiner Projekte gewesen. Es ist sogar so, dass ich ohne dieses Know-How ein sehr profitables, 
anderes Projekt gar nicht hätte abwickeln können!

Man kann das Image für so viele Dinge benutzen:

- Ad-hoc Jump Hosts! Das ist der bei weitem häufigste Einsatzzweck, und dafür habe ich das Image ja auch erschaffen. 
Also eine Art "Brücke" zwischen zwei eigentlich nicht miteinander verbundenen Systemen

- Ad-hoc X-Hosts! Du kannst tatsächlich deine gesamte X11-Kommunikation durch das ssh-relais redirecten. Sehr nützlich 
in einem Projekt, in dem es darum ging, den Build-Prozess einer tcl/tk-basierten GUI in einen Container zu verschieben.
Der ssh-relais wurde als daemon gestartet, der build-Prozess wurde dann per ssh -XC gestartet. Auf dem 
Bildschirm des Entwicklers/Testers erschien die GUI des Compilats, bereit für Tests. Das hat überraschend gut 
funktioniert. 

- wenn man die Home-Directories des ssh-relais im tmpfs des Docker Hosts platziert, hat man eine super sichere 
bash-shell, die sofort allen content verliert sobald jemand mit dem Container rumspielt.

Schaus dir an, es ist sehr praktisch.

## ticino events a.k.a. tinEvents (2010 - 2015)

Ja, ich gestehe, ich war mal ein Wicket-Fan. Wicket, das war ein Web-Framework vergleichbar mit react oder jsf,
und aus meiner Sicht der beste Web-Framework in der Prä-Websocket-Welt. Ich weiss, ich weiss, Wicket hat sich auch 
weiterentwickelt, aber ich finde inzwischen andere Konzepte zielführender. Anyway,...

Wie war ich aufgeregt als Wicket dann Events eingeführt hat! Da konnte man, quer durch die Applikation und auch bis zu 
den Clients events feuern, losgelöst von irgendwelchen Methodennaḿen und ohne sich Gedanken machen zu müssen, wer die 
Daten überhaupt empfängt und was im Fehlerfall passiert,...

So wurde es jedenfalls angekündigt, oder vielleicht kam es bei mir auch nur so an. Die Implementierung der 
Wicket-Events waren dann nämlich doch nicht so einfach und generisch: 

- man musste eine Interface-Klasse erstellen, speziell für die Methodennamen der Sender und der Empfänger. D.h.  
sowohl der Sender als auch der Empfänger mussten das Interface implementieren. 
Dazu kam dann noch die Event-Klasse.

- die Events konnten erst ab einem bestimmten Zeitpunkt im Lebenszyklus der 
Wicket-Applikation empfangen werden. Will sagen: nicht während der Initialisierungsphase der Beans im 
damals aufkommenden Spring-Framework. Ich konnte also keine "Created" und "Initialized"-Events 
feuern und empfangen um meine eigenen Komponenten on-the-fly zu konfigurieren.

- die Events wurden nicht im Cluster verteilt. Wenn deine Wicket-Anwendung also in einem JEE-Cluster 
betrieben wurde, blieben die Events lokal.

- die Events beschränkten sich strikt auf Wicket, und hatten auch starke Abhängigkeiten zu Wicket. Ja ich weiss, das 
hätte ich mir auch vorher denken können; aber die Wicket-Leute hatten bis dahin einen nicht-intrusiven Charakter 
gefahren,  sodass es leicht war, Wicket-Module zu schreiben die du auch woanders verwenden kannst. Leider sind Events,
vergleichbar mit IPC, auf einer so hohen Abstraktionsebene, dass ich davon wirklich überrascht wurde. 
Swing-Anwendungen mit Wicket-Events ausstatten? Ein Ding der Unmöglichkeit.

Also setzte ich mich hin und erdachte mit den perfekten Event-Framework, mit folgenden Anforderungen:

- der Framework musste __standalone__ betreibbar sein, also am besten gar keine Abhängigkeiten zu 
Drittanbietern besitzen

- er musste sehr schnell initialisierbar und abschaltbar sein (sonst wäre tdd eine qual gewesen)

- er musste gut mit dem Java Garbage Collector klarkommen, weil sonst Memory Holes an der Tagesordnung wären

- er musste möglich sein, dass Methoden und Objekte, die nichts vom Event Framework wussten, sowohl senden als auch empfangen konnten
 
- er musste leicht zu erweitern sein, z.B. durch einen zuschaltbaren Internet-Transport

- es musste mit dem IoC-Pattern von Spring zurecht kommen.

Kurz und gut, er musste so einfach zu bedienen sein, dass er für jeden Sch**ssdreck verwendet werden konnte.

Tja, und das habe ich geschafft. 

Darf ich vorstellen: [ticino events](http://micwin.github.io/ticino/ticino-events/index.html)

Die "coolen Features" sind:

- weder Sender noch Empfänger eines Events müssen wissen, dass es ticino events gibt; es können so also sich fremde Klassen 
nachträglich verdrahtet werden ohne dass sie ein bestimmtes Interface bedienen müssten.

- Ich rate zwar, dedizierte Event-Klassen zu verwenden; es ist aber nicht nötig; man könnte 
also z.B. auch Java-Primitive verwenden, oder eine LinkedList, oder Java Interfaces, oder eine 
Lambda-Funktion, Future oder Promise.

- Sender und Empfänger werden in den __EventScopes__ zusammengebracht; diese dienen auch gleich als 
Kapselung. Man kann also sensitive Concerns in dedizierten EventScopes kapseln, während Allerwelt-
Events über eine Art  "globalen EventScope" gehandhabt werden können.

- ticino hat keine dedizierten Event-Klassen,  Superklassen oder Abstrakt-Klassen von denen 
abgeleitet werdne muss. Wie oben erwähnt können alle bereits bestehende Klassen als Event-Klassen 
verwendet werden und sogar Primitive und Lambdas. Deshalb kann in den Event-Klassen jede Information 
einprogrammiert  werden, die Sender, Empfänger und/oder Betreiber interessieren.
 
- ticino-events können synchron und asynchron abgesetzt werden. Im Falle der asynchronen 
Verarbeitung kann bestimmt werden, ob die Empfänger seriell oder parallel aktiviert werden. 

ticino events finden sich in der 
[maven central](https://search.maven.org/artifact/net.micwin.ticino/ticino-events/0.3.6/jar), die Dokumentation 
befindet sich [hier](http://micwin.github.io/ticino/ticino-events/index.html), das Repo [hier](https://github.com/micwin/ticino)

Leiderleider ist die Spring-Anbindung aber nicht sooo stabil wie ich das mir wünsche, aber ich habe mir schon 
vorgenommen, in einem Moment der Muße mach ich ticino Events perfekt. 

## ticino context (2015 und später)

Als ich mit dem minimalistischen Ansatz angefangen hatte, hatte ich natürlich Blut geleckt. Da war noch ein anderes Problem, 
das mich an Java genervt hat: die Collections.

Kann mir bitte einer sagen, warum bei Java immer so getan wird, als ob alles mit allem kompatibel ist - nur um es dann 
im entscheidenden Fall doch nicht zu sein? Warum bitte müssen ArrayLists und HashSets dasselbe Interface bedienen, es 
ist aber nicht möglich, einen ArrayList mnit einem Array zu initisalisieren? ? ArrayLists und HashSets sind schon vom 
Konzept her komplett unterschiedliche Dinge wobei sich Arrays und ArrayLists nur durch die Kapselung und ein, zwei 
Details unterscheiden! 

Also gut, dachte ich mir - pronbieren wir das mal. Was hatte ich für Anforderungen?

- keine Gemeinsamkeiten heucheln wo es keine gibt.

- Eigenschaften der Container sollten über Funktionen abfragbar sein

- Natural fits unterstützen, also z.B. Arrays leicht in ArrayLists (und umgekehrt) umwandelbar machen.

- bessere Unterstützung von Generics

Et voilà - [ticino context](http://micwin.github.io/ticino/ticino-context/index.html) - wobei,... geniesst das bitte 
mit Vorsicht, die Dokumentation ist crappy. 
Den Source Code findet ihr [hier](https://github.com/micwin/ticino/tree/develop/context/src/main/java/net/micwin/ticino/context), 
auf maven central ist das Projekt [hier](https://search.maven.org/artifact/net.micwin.ticino/ticino-context/0.3.6/jar).
 
Die Highlights:

- Element-Lookup mit Lambda

- Element-Validatoren, mit denen der Instanzierer des Containers sicherstellen kann, dass nur Elemente in den Container 
gehen, die einem Kriterium entsprechen

- Typsichere Unterscheidung von ReadOnly und ReadWrite-Containern

Das Projekt ist bei weitem nicht fertig und wurde leider schon weitestgehend, in den ursprünglichen Ansprüchen, von den 
neuen Entwicklungen des JDK überholt. Ich denke ich werde das Thema zwar aus reinem Interesse mal weiterführen, 
denke aber meine Bemühungen sind eher akademischer Natur und werden wohl keine Verbreitung oder Anwendung finden.

## verspielt: chance2 (2004-2006), open space (2012-2014)

Hatte ich schon erwähnt dass ich Wicket-Fan war? Nun, ich habe sogar ein Spiel mit Wicket programmiert: [open space](https://github.com/micwin/open-space).

Entstanden ist open-space aus dem Verlangen heraus, mein erstes Computerspiel, chance2-online, upzugraden; 
das hatte ich 2004  mit jsp entwickelt; das war eine Katastrophe, darum wechselte ich dazwischen auf struts, dann wurde 
alles nur noch schlimmer; bis zu dem Punkt wo es einfach unwartbar wurde. 2006 schaltgete ich dann den letzten Server ab 
und chance2 war tot. 

Der Server jedoch steht imme rnoch in meinem Keller, ich kann mich einfach nicht davon trennen. Aber wie war es glorreich! 
Ich hatte zeitweilig um die 100 User. chance2 war ein Browser-bassiertes  Mass Multiplayer Online Strategy Game, 
mit frei konfigurierbaren Schiffstypen, und weiteren, atemberaubenden Ideen. Ich hatte sogar eine Designerin beauftragt, 
die mir Postkarten erstellte und druckte. Und das wollte ich mit open space wieder aufleben lassen. Aber dieses mal 
richtig!

Tja, was soll ich sagen. Wicket-Anwendungen lassen sich schwer warten, und Open-Space war keine Single-Page-Anwendung. 
Somit starb open-space auch wieder. Der letzte Commit datiert auf den 1. Februar 2014.