# Softwareentwicklung


## Produktlebenszyklus einer Software
Um sicherzustellen, dass die Software am Ende das tut was sie soll wird üblicherweise nach einem bestimmten Schema vorgegangen. Je nach Firma und Projekt gibt es unterschiedliche Schemata wie man Software entwickeln kann, die sich darin unterscheiden, wann welche Aufgabe in einem bestimmten Umfang als erledigt betrachtet wird. Unabhängig davon werden im Rahmen einer Entwicklungsprozesses folgenden Phasen durchlaufen:


```{figure} ../../figs/02-course-concept/overview/development-phases.png
---
width: 600px
name: fig-development-phases
---
Entwicklungsphasen der Softwareentwicklung nach dem Wasserfallmodell
```

Quelle: {cite}`sommerville`

Bei der **Analyse und Definition der Anforderungen** werden die Ziele des Systems bzw. der Software in Zusammenarbeit mit den Nutzern definiert. Beim **System- und Softwareentwurf** wird eine übergeordnete Systemarchitektur erstellt, wobei festgelegt wird welche Funktionalitäten von welchen Hardware- und Softwarekomponenten übernommen wird. Es geht darum ein abstraktes Modell des Systems zu entwerfen. Bei Der **Implementierung und Modultests** wird der Softwarentwurf durch eine Menge von Programmen oder Programmeinheiten umgesetzt. Das Testen der Einzelmodule stellt sicher, dass jede Einheit ihre Spezifikation erfüllt. Beim der **Integration und Systemtest** werden die Einzelprogramme integriert und als Ganzes - wenn mölich auf der Zielinfrastruktur -- getestet. Nach einem erfolgreichen Test wird das System ausgeliefert. **Betrieb und Wartung**: das System wird auf der Kundeninfrastruktur installiert und zum Gebrauch freigegeben. Frühe Fehler, die nicht erkannt wurden, werden behoben. Kommen neue Anforderungen auf, werden diese ggf. umgesetzt.

Phasen-übergreifend wird außerdem
- die IT-Security berücksichtigt
- die Safety berüchsichtigt
- Konfigurationsmanagement betrieben 
- die Softwarequalität monitored


```{admonition} Hinweis
:name: remark-sample
:class: remark
Das Software Engineering Compentency Model (SWECOM) der IEEE Computer Society beschreibt welche Kompetenzen ein Softwareentwickler benötigt, um die Phasen-bezogenen und phasen-übergreifenden Aufgaben zu erledigen.
```

## Fokus dieser Vorlesung

Softwareentwicklung beinhaltet viele Aspekte. Im Rahmen dieser Vorlesung können wir nicht auf alle eingehen. Wir nehmen an, dass:

- das Problem ("Die Aufgabe") bekannt ist (Anforderungsdefinition erledigt)
- Ihr Programm von keinem anderen Menschen oder keiner anderen Software benutzt werden muss (Systemplanung und Integration entfällt)
- Ihr Programm nur auf dem Rechner laufen muss, auf dem es entwickelt wurde (Systemplanung und Systemintegration, Betrieb und Wartung entfällt)
- Sie den Algorithmus nur über einen begrenzten Zeitraum nutzen wollen (keine Softwareupdates!)

Im Rahmen dieser Vorlesung liegt der Fokus auf den Grundlagen des Programmierens, was der Phase "Implementierung und Modultests" entspricht.
Dabei lernen Sie, wie man einen Algorithmus entwickelt, in einem Computerprogramm umsetzt ("implementiert") und testet. 


```{admonition} Hinweis
:name: algorithmus
:class: remark
Im Rahmen dieser Vorlesung entwickeln wir Programme, bei denen alles nacheinander ausgeführt wird (Single-Thread-Anwendungen). Programme, bei denen mehrere Schritte nebenläufig ausgeführt werden (z.B. Multithreading oder parallele Programmierung), sind nicht Teil der Veranstaltung.
```




