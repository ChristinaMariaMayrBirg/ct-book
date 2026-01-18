# Basiswissen Informatik


```{figure} ../../figs/overview/infrastructer-metaphor.png
---
height: 320px
name: infrastructer-metaphor
---
```
In diesem Teil schauen wir uns die „Infrastruktur“ an, auf der unsere Programme ausgeführt werden. Ein Programm läuft immer auf *irgendeiner* Rechenplattform – zum Beispiel auf einem Computer (Laptop/PC/Server) oder auf einem Mikrocontroller in einem eingebetteten System.
Diese Plattformen unterscheiden sich u. a. in Rechenleistung, Speicher, Betriebssystem und Schnittstellen. 

Im Rahmen dieser Vorlesung konzentrieren wir uns auf den **Computer** als Referenzmodell, weil er ein gut verständliches Grundmodell liefert, das sich später auf andere Systeme (z. B. Mikrocontroller) übertragen lässt.

Konkret sehen wir uns an: Was macht ein Computer eigentlich, wie werden Informationen verarbeitet, und welches Vokabular brauchen wir, um über Programme sauber zu sprechen.


Dieses Kapitel gibt Ihnen das gemeinsame **Grundvokabular** für die restliche Veranstaltung. Wir verbinden dabei drei Blickwinkel:

- **Computer & Informationsverarbeitung**: Was passiert grob, wenn ein Programm läuft?
- **Darstellung & Codierung**: Wie werden Zahlen, Text und andere Informationen als Bits repräsentiert?
- **Software Engineering (Praxisbezug)**: Wie ist Anwendungssoftware typischerweise aufgebaut – und warum sieht ein GitHub-Projekt anders aus als eine einzelne Python-Datei?


Nach diesem Kapitel können Sie …

- zentrale Begriffe **Algorithmus**, **Programmcode/Quellcode**, **Programm** und **Software** definieren und voneinander abgrenzen.
- den groben Ablauf der Programmausführung mit dem Vokabular **Eingabe – Verarbeitung – Ausgabe** (EVA) plus **Speicher/Zustand** beschreiben und die Rollen von **CPU**, **RAM** und **Betriebssystem** einordnen.
- erklären, warum Bitfolgen ohne Kontext keine Bedeutung haben und wie **Codierung** Bedeutung festlegt (z. B. Zahl vs. Zeichen).
- zwischen **Bedeutung** und **Darstellung** unterscheiden und typische Darstellungen (binär/dezimal/hex) in technischen Ausgaben wiedererkennen.
- den typischen Aufbau eines Softwareprojekts (z. B. auf GitHub) erklären und die Rollen von **Entrypoint**, **Workflow/Geschäftslogik** und **wiederverwendbaren Bausteinen/Modulen** zuordnen.
- den Zweck von `if __name__ == "__main__":` als **Guard** erklären und den Unterschied **direkt ausführen** vs. **importieren** beschreiben.
- die Konzepte **Kontrollstrukturen** und **Datenstrukturen** als Bausteine von Programmen benennen (ohne Python-Syntax zu wiederholen).
- Softwareideen zielgruppengerecht kommunizieren, z. B. durch **Pseudocode** oder **Struktogramme**, und das passende Medium auswählen.


