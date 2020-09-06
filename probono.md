---
layout: page
title: Pro Bono
permalink: /probono/
---
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
ausser bash und which, und es ist lediglich ~ 80kb gross
- kooperiert mit jedem CI-Server
- dead simple
- zur Not kannst du auch python verwenden

Interessiert? Hier nochmal  der Link zur Homepage: [clici](https://metafence.gitlab.io/clici/)