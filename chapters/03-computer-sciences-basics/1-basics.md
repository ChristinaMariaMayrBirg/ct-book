(sec-computer-basics)=

# Computer

Ein *Computer* ist die konkrete technische Realisierung eines **Informationsverarbeitungssystems** (Hardware + Software). Um Programme zu verstehen (und später selbst zu schreiben), hilft es, ein klares Modell davon zu haben, **wie** ein Computer Informationen einliest, speichert, verarbeitet und ausgibt.


Alle Computer basieren auf diesen vier grundlegenden Aufgaben:

1. Informationen **einlesen**
2. Informationen **speichern**
3. Informationen **verarbeiten**
4. Informationen **ausgeben**

Sie bilden das Fundament eines jeden Computers.
Die Verarbeitung von [Information](sec-information) wird symbolisch vollzogen, d.h. Computer manipulieren auf Grundlage von bestimmten Regeln die Symbole der Eingabe um die Symbole der Ausgabe zu bestimmen.

```{admonition} EVA-Prinzip
:class: remark
:name: remark-eva
Der Computer basiert auf dem sog. *EVA-Prinzip* (**Eingabe**, **Verarbeitung** und **Ausgabe**).
```

Ein Computer erweitert das EVA-Prinzip um den **Speicher** und damit um einen **Zustand**.
Wäre der Computer zustandslos würde er bei gleicher **Eingabe** $x$ auch stets die gleiche **Ausgabe** $y$ erzeugen.
Durch den Speicher kann sich, je nach Eingabe, der Zustand $z$ des Computers verändern und, je nach seinem Zustand, kann dieselbe Eingabe zu unterschiedlichen Ausgaben führen.

```{figure} ../../figs/digital-computer/basics/dfa.png
---
width: 600px
name: fig-dfa
---
Ein Modell eines Computers mit 4 Zuständen. 
Der Computer befindet sich in Zustand $z = z_1$ (rot).
Die Ausgabe $y$ hängt von der Eingabe $x$ als auch vom aktuellen Zustand $z$ (hier $ = z_1$) des Computers ab.
Während der Berechnung der Ausgabe verändert der Computer seinen Zustand auf $g(z, x)$.
$f$ und $g$ sind mathematische Funktionen.
```

Über *Eingabegeräte* (z.B. Tastatur, Maus, Sensoren) werden Informationen in eine Folge von zwei Zuständen (0 und 1) transformiert und im Speicher abgelegt.
Der Prozessor **ließt** diese digitalen Informationen aus dem Speicher, **manipuliert** sie durch das Abarbeiten eines [Algorithmus](def-algorithm) und **schreibt** die veränderte Information zurück in den Speicher.
Die verarbeitete Information wird schließlich durch *Ausgabegeräte* (z.B. Monitor, Lautsprecher) **ausgegeben**, die die Folge von 0 und 1 in Bilder, Ton und andere Formate umwandeln.


(sec-information-flow)=
# Der Informationskreislauf

Wie wird aus Gattern, elektrischen Leitungen und dem Speicher ein vollwertiger (digitaler) Computer, der alle vier grundlegenden Aspekte der *Informationsverarbeitung* realisiert?

(sec-von-neumann)=
## Die Von-Neumann-Architektur

Die *Von-Neumann-Architektur* ist die bekannteste und meist verwendete Hardware-Architektur, die den Aufbau von Computern beschreibt.
Sie legt fest, wie die wesentlichen Bauteile miteinander interagieren.

```{figure} ../../figs/digital-computer/informationcycle/von-neumann-architecture.png
---
height: 300px
name: von-neumann-architecture-2
---
Die Von-Neumann-Architektur auch bekannt als Princeton Architektur.
```

```{admonition} Arbeitsspeicher
:name: def-main-memory
:class: definition
Der *Arbeitsspeicher* oder *Hauptspeicher* oder *RAM (Random Access Memory)* eines Computers ist jener temporärer Speicher, der die gerade auszuführenden **Programme** oder **Programmteile** und die dabei benötigten **Daten** enthält.
Er erlaubt den direkten Zugriff auf beliebige Speicheradressen.
```

```{admonition} Bus
:name: def-bus
:class: definition
Ein *Bus* ist ein Kommunikationssystem über das [Bits](def-bit) und [Bytes](def-byte) übertragen werden.
Der *Bus* verbindet durch elektrische Leitungen verschiedene Komponenten innerhalb eines Computers oder zwischen mehreren Computern.
```

```{admonition} Central Processing Unit (CPU)
:name: def-cpu
:class: definition
Der *Hauptprozessor* oder *Central Processing Unit (CPU)* besteht aus Leitungen, Registern, der Kontrolleinheit, der arithmetische/logische Einheit und möglicherweise spezielle Einheiten für bestimmte Berechnungen wie etwa die Fließkomma-Recheneinheit.
Die CPU ist die Kernkomponente eines Computers, die für die Ausführung von Anweisungen aus Computerprogrammen verantwortlich ist.
Sie interpretiert und führt Befehle aus dem Arbeitsspeicher aus und verarbeitet Daten, indem sie arithmetische und logische Operationen durchführt.
```

```{admonition} Register
:name: def-register
:class: definition
*Register*, sind extrem schnelle kleine flüchtige Speichereinheiten innerhalb der CPU, welche die CPU für viele Operationen verwendet.
```

Die wichtigsten Komponenten sind:

- **Hauptspeicher (RAM)**: Enthält das auszuführende Programm und die zu verarbeitenden Daten. Er ist *flüchtig* - verliert alle Daten bei Stromausfall.
- **CPU**: Besteht aus der *Kontrolleinheit* (liest Befehle, delegiert Aufgaben) und der *arithmetische/logische Einheit* (führt Berechnungen durch).
- **Register**: Extrem schnelle, kleine Speichereinheiten innerhalb der CPU für aktuelle Operationen.
- **Bus**: Verbindet alle Komponenten über elektrische Leitungen.

Programme werden auf einem *persistenten* (nicht flüchtigen) Speicher wie einer Festplatte gespeichert und vor der Ausführung in den Hauptspeicher geladen.
Die *Flüchtigkeit* des Hauptspeichers ermöglicht hohe Geschwindigkeit, während persistente Speicher die Daten dauerhaft erhalten.

Damit die [Bits](def-bit) und [Bytes](def-byte) nicht durcheinander gelesen, manipuliert und geschrieben werden, ist die CPU *getaktet*.
Eine globale Uhr gibt vor, wann Komponenten aktiv werden können.
Eine CPU mit 3 Gigahertz (GHz) führt 3 Milliarden Zyklen pro Sekunde durch.

## Das Betriebssystem

```{admonition} Betriebssystem
:name: def-operating-system
:class: definition
Das *Betriebssystem* eines Computers ist ein spezielles Hauptprogramm, welches alle anderen Programme und die Rechnerressourcen des Computers verwaltet.
```

Das *Betriebssystem* (z.B. Ubuntu, Windows 10, Mac OS) bestimmt, wann welches Programm welche Hardware nutzen darf und auf welchen Speicherbereich das jeweilige Programm zugreifen darf.
Hat ein Computer nur eine CPU (mit nur einem Kern), so erscheint es nur so, als würden viele Programme gleichzeitig laufen.
In der Realität wechselt das Betriebssystem die aktiven Programme fortwährend durch.

```{admonition} Bootvorgang
:name: def-booting
:class: definition
Der *Bootvorgang* ist der Prozess, bei dem ein Computer nach dem Einschalten oder Neustarten sein Betriebssystem und weitere essenzielle Software lädt, um betriebsbereit zu werden.
```

Das *Betriebssystem* wird beim Start des Computers geladen (*Booten*).
Der Schlüssel hierzu ist ein kleines Programm auf dem *Festwertspeicher (ROM)*, das von der Hardware selbst geladen wird.
Die Logik zum Laden des ersten Programms ist in den Bauteilen selbst fest verdrahtet.
Der Festwertspeicher ist nicht flüchtig und bleibt auch nach dem Ausschalten erhalten.

(sec-run-program)=
## Programme ausführen

Starten Sie ein Programm, teilen Sie dem [Betriebssystem](def-operating-system) mit, dass Sie dieses Programm ausführen möchten.
Das *Betriebssystem* lädt es in den Hauptspeicher und teilt ihm entsprechende Ressourcen zu.
Laut der *[Von-Neumann-Architektur](von-neumann-architecture-2)* liegen **Daten** und **Programme** im gleichen *Hauptspeicher*.
Das Programm ist eine zusammenhängende Folge von 0 und 1, welche Befehle repräsentieren, z.B.:

- $\text{ADD} \ \$5 \ \$6 \ \$7$: Addiere Zahlen in Register $\$5$ und $\$6$, speichere Ergebnis in Register $\$7$
- $\text{LOAD} \ \#15 \ \$5$: Lade Daten aus Hauptspeicheradresse $\#15$ ins Register $\$5$
- $\text{STORE} \ \$7 \ \#16$: Speichere Daten von Register $\$7$ im Hauptspeicher an Adresse $\#16$

```{figure} ../../figs/digital-computer/informationcycle/program-run.png
---
width: 700px
name: fig-program-run
---
Zusammenspiel zwischen Kontrolleinheit und arithmetische/logische Einheit, Register, Befehlszeiger (CPU) und Arbeitsspeicher.
```

```{admonition} Befehlszeiger
:name: def-program-counter
:class: definition
Der *Befehlszeiger* ist ein spezielles [Register](def-register) der *Kontrolleinheit* welches die *Arbeitsspeicheradresse* des nächsten auszuführenden Befehls enthält.
Bei der Ausführung eines Programms wird der Befehlszeiger aktualisiert, um auf die nächste Anweisung zu zeigen, die ausgeführt werden soll.
```

Die *Kontrolleinheit* liest Befehle aus dem Hauptspeicher, lädt die benötigten Daten in Register, aktiviert die Recheneinheiten und schreibt Ergebnisse zurück.
Der *Befehlszeiger* zeigt dabei auf die nächste auszuführende Anweisung.
Register sind deutlich schneller als der Hauptspeicher und befinden sich näher an den Recheneinheiten, weshalb häufig verwendete Werte dort zwischengespeichert werden.

Wenn das Betriebssystem entscheidet, dass ein anderes Programm an der Reihe ist, wird der aktuelle Zustand des laufenden Programms gesichert (z. B. der Befehlszeiger).
Sobald das Programm wieder aktiv wird, werden alle notwendigen Daten wieder geladen.

```{admonition} Exkurs: Mikrocontroller vs. Computer
Ein **Mikrocontroller** ist ebenfalls ein Computer im weiteren Sinne – aber typischerweise für eine *spezielle Aufgabe* optimiert: Er integriert CPU, Speicher und Ein-/Ausgabe (GPIO, Timer, ADC, Kommunikationsschnittstellen) auf einem Chip und arbeitet oft mit deutlich weniger Ressourcen.

Wichtige Konsequenzen fürs Programmieren:

- **Wenig Unterstützung durch ein Betriebssystem**: Auf einem Mikrocontroller müssen Sie sich im Programm oft um Aufgaben kümmern, die auf einem „normalen“ Computer das Betriebssystem für Sie übernimmt (z. B. zeitgesteuerte Abläufe, Zugriff auf Hardware oder das gleichzeitige Abarbeiten mehrerer Aufgaben).
- **Knappere Ressourcen**: RAM/Flash sind begrenzt. Speicher- und Laufzeitkosten werden wichtiger (z. B. keine großen Datenstrukturen, vorsichtiger Umgang mit Speicher).
- **Echtzeit/Timing**: Reaktionen müssen oft innerhalb fester Zeiten erfolgen (z. B. Regelung, Kommunikation). Das beeinflusst Programmstruktur und Tests.
- **Ein-/Ausgabe ist hardware-nah**: Statt Dateien/Fenstern arbeiten Sie mit Pins, Registern und Peripherie.
```