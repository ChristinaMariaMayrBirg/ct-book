(sec-computer-basics)=

# Computer

Alle Computer basieren auf diesen vier grundlegenden Aufgabe:

1. Informationen **einlesen**
2. Informationen **speichern**
3. Informationen **verarbeiten**
4. Informationen **ausgeben**

Sie bilden das Fundament eines jeden Computers.
Die Verarbeitung von [Information](sec-information) wird symbolisch vollzogen, d.h. Computer manipulieren auf Grundlage von bestimmten Regeln die Symbole der Eingabe um die Symbole der Ausgabe zu bestimmen.
Computer haben keine eigene Intention oder agieren aus einer Emotion heraus.
Sie haben auch keinerlei Verständnis von der Eingabe.
Zum Beispiel können Computer Texte in unterschiedlichen Sprachen übersetzen was jedoch nicht bedeutet, dass sie "verstehen" was sie da übersetzen.
Inwieweit symbolische Manipulationen zu einem "Verstehen" führen könnten, wird derzeit rege im Bereich der *künstlichen Intelligenz* diskutiert.

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

Über *Eingabegeräte*, die den Computer mit der Eingabe füttern, ist er mit der Außenwelt verknüpft.
Tastatur und Maus sind beispielsweise Eingabegeräte, die uns Menschen eine unmittelbare Möglichkeit geben, um *Informationen* in den *Computer* zu speisen.
Als weitere Eingabegeräte können wir eine Kamera oder andere Sensoren wie Messgeräte, die den Puls oder Blutzucker messen, anfügen.

Die Eingabe eines Computers kann analog zu unserer eigene Wahrnehmung gesehen werden.
Nach dem vereinfachten empirischen Menschenbild, nehmen wir durch Stimulierungen unserer Sinne die Welt wahr und unser "menschlicher Prozessor" verarbeitet die aufgenommenen Informationen.
Der Unterschied zwischen unserer Eingabe und der eines Computers, ist die Art mit der Informationen repräsentiert werden.
Wir Menschen übertragen und verarbeiten Informationen (analog) durch Nervenenden und chemische Prozesse.
Die Eingabe eines Computers wird durch das *Eingabegerät* in eine Folge von zwei Zuständen 0, 1 transformiert und in den Speicher des Computers abgelegt.
Hier sei erwähnt, dass das soeben beschriebene Menschenbild als Analogie genommen wird und nicht in dieser Weise zutreffen muss.
Die Grenze zwischen Mensch und seiner Welt, d.h. dem Subjekt und seinen Objekten, ist möglicherweise weit aus weniger klar als wir uns das vorstellen.

Der Prozessor eines Computers **ließt** (digitale) Informationen aus dem Speicher, **manipuliert** sie durch eine Abfolge von Symbolmanipulationen, d.h., durch das Abarbeiten eines [Algorithmus](def-algorithm) (eine endliche Folge von Anweisungen) und **schreibt** die **veränderte** Information zurück in den Speicher.

Wenn alle Arbeit getan ist, wird die verarbeitete Information durch die *Ausgabegeräte* **ausgegeben**.
Ausgabegeräte können Monitore, Lautsprecher aber auch andere Geräte, wie zum Beispiel VR-Brillen sein.
Die Ausgabegeräte erhalten als Information eine Folge von 0 und 1.
Sie transformieren diese Information in Bilder, Videos und mehr.


#todo hinweis
Der Begriff *Computer* hatte ursprünglich eine andere Bedeutung.
Anstatt digitaler Maschinen waren es menschliche Computer die unentwegt Berechnungen durchführten.
Die ersten maschinellen Computer bestanden noch aus Holz, Metall, mechanischen Hebeln und Getrieben.
Im 20. Jahrhundert wurden schließlich die mechanischen Komponenten durch elektrische Bauteile abgelöst.
Die daraus resultierenden Computer waren dennoch riesig und, im Vergleich zu heute, enorm langsam.
Um eine einfache Gleichung zu lösen brauchten diese Rechner, die einen ganzen Raum füllten, mehrere Stunden.

(sec-information-flow)=
# Der Informationskreislauf

Sie kennen nun die vier grundlegenden Aufgaben eines Computers und wissen wie er aus den zwei Zuständen **Strom aus** und **Strom an** Informationen der unterschiedlichsten Art repräsentieren kann.
Zudem haben wir uns angesehen, wie aus primitiven boolschen Operationen, welche über Gatter/Schaltungen realisiert werden, komplexe Berechnungen entstehen.

Bereits an dieser Stelle wird deutlich, dass *Abstraktion* und *Komposition* eine zentrale Rolle in der Informatik spielen.
Das konkrete Rasterbild ist auf der abstrakten Ebene nichts anderes als eine Folge von 0 und 1.
Durch die Komposition und Hintereinanderschaltung/Wiederholung einfacher Gatter, entstehen aus primitiven Operationen komplexe Berechnungen.

Ein einfacher $n$-Bit-Addierer gleicht einem Taschenrechner, doch ist ein Taschenrechner noch kein vollwertiger Computer.
Manche Taschenrechner lassen sich zwar Programmieren, doch sind sie nicht im Stande all das zu berechnen, was Informatiker\*innen als [berechenbar](def-turing-computable) wahrnehmen.
Anders als ein Taschenrechner, ist ein Computer *[Turing-vollständig](def-turing-complete)*.
Weshalb ist er das?
Wie wird aus Gattern, elektrischen Leitungen und dem Speicher ein vollwertiger (digitaler) Computer, der alle vier grundlegenden Aspekte der *Informationsverarbeitung*

1. Informationen **einlesen**,
2. Informationen **speichern**,
3. Informationen **verarbeiten**, und
4. Informationen **ausgeben**
   
realisiert?

(sec-von-neumann)=
## Die Von-Neumann-Architektur

Bevor wir diese Frage klären brauchen wir ein konzeptionelles Verständnis der wesentlichen Bauteile und deren grundsätzlichen Interaktion miteinander.
Zusammengenommen bilden sie den *digitalen Computer*.
Eine solche Beschreibung bezeichnen wir als *Hardware-Architektur*.
Sie kann selbstverständlich unterschiedlich detailliert ausfallen.
So gibt es auch Beschreibungen einzelner Bauteile die wiederum die Interaktion ihrer Einzelkomponenten beschreiben.

Wie der Bauplan eines Hauses, in dem festgelegt ist wie Küche und Bad miteinander verbunden sind und wie die Bewohner das Gebäude nutzen können, legt eine Architektur fest, über welche Leitungen beispielsweise der Speicher mit den Recheneinheiten interagiert.

```{figure} ../../figs/digital-computer/informationcycle/von-neumann-architecture.png
---
height: 300px
name: von-neumann-architecture-2
---
Die Von-Neumann-Architektur auch bekannt als Princeton Architektur.
```

Die *Von-Neumann-Architektur* ist wohl die bekannteste und zugleich meist verwendete Hardware-Architektur bzw. *Rechnerarchitektur*, die den Aufbau der Computer beschreibt.
Jeden Rechner, den Sie je benutzt haben, basiert höchstwahrscheinlich auf dieser Architektur.

```{admonition} Arbeitsspeicher
:name: def-main-memory
:class: definition
Der *Arbeitsspeicher* oder *Hauptspeicher* oder *RAM (Random Access Memory)* eines Computers ist jener temporärer Speicher, der die gerade auszuführenden **Programme** oder **Programmteile** und die dabei benötigten **Daten** enthält.
Er erlaubt den direkten Zugriff auf beliebige Speicheradressen.
```

Die erste wichtige Komponente ist der sogenannten *Hauptspeicher*, auch *Arbeitsspeicher* genannt.
Im Bild oben haben wir *Hauptspeicher* und *Festplattenspeicher* mit Speicher zusammengefasst.
Was der unterschied dieser beiden Speicherkomponenten ist besprechen wir weiter unten.
Im *Speicher* befinden sich die Anweisungen der Informationsmanipulation, d.h. das **auszuführende Programm** als auch alle zu verarbeitenden **Daten**, welche vom Programm verarbeitet werden.

```{admonition} Bus
:name: def-bus
:class: definition
Ein *Bus* ist ein Kommunikationssystem über das [Bits](def-bit) und [Bytes](def-byte) übetragen werden.
Der *Bus* verbindet durch elektrische Leitungen verschiedene Komponenten innerhalb eines Computers oder zwischen mehreren Computern.
```

Wir sprechen häufig von unterschiedlichen *Bus-Teilen*, zum Beispiel ist die Grafikkarte über den sogenannten PCI-Express Bus mit dem Rest des Computers verbunden.
Der *interne Bus* auch *Speicher-Bus* oder *System-Bus* genannt, verbindet alle internen Komponenten eines Computers mit der *Hauptplatine* (Motherboard/Mainboard).
Es gibt aber auch *Bus-Systeme* die unterschiedliche Computer oder andere Geräte (z.B. externen Speicher) miteinander verbinden.

Die *Hauptplatine* ist jenes Bauteil auf dem die CPU-nahen Komponenten (CPU, Hauptspeicher, Grafikkarte, interne Bus-Systeme) montiert werden.

Die *Kontrolleinheit* besteht aus einer Komposition von Gattern, einem *Instruktionsregister* sowie einem [Befehlszeiger](def-program-counter).
Sie fungiert als Programminterpreter oder "Mastermind" und delegiert Aufgaben an die jeweils dafür geeigneten Recheneinheiten weiter.
Sie ließt die Programmanweisungen aus dem Hauptspeicher und realisiert diese indem sie die *arithmetische/logische Einheit* mit Instruktionen und den notwendigen, aus dem Hauptspeicher geladenen Daten versorgt.
Fließkommaoperationen delegiert die Kontrolleinheit häufig an eine spezielle (hier nicht eingezeichnete) *Fließkomma-Recheneinheit*.
Der *Befehlszeiger* beinhaltet eine Hauptspeicheradresse, die auf den aktuelle auszuführenden Befehl im Hauptspeicher zeigt. 
Der Befehl $\text{ADD}$ steht zum Beispiel für die Addition von zwei ganzen Zahlen.
Er wird allerdings im Hauptspeicher als Binärfolge abgespeichert!
Ein solcher Befehl wird aus dem Hauptspeicher ins Instruktionsregister geladen.
Die Zahlen, die addiert werden sollen, werden ebenfalls von der Kontrolleinheit aus dem Hauptspeicher in Register der arithmetische/logische Einheit geladen.
Dann wird die arithmetische/logische Einheit aktiviert.
Diese berechnet das Ergebnis und schreibt es in ein weiteres [Register](def-register).
Die Kontrolleinheit schreibt das Ergebnis an die vom Programm definierte Stelle (Adresse) im Hauptspeicher.

Die Recheneinheiten (arithmetische/logische Einheit und Fließkomma-Recheneinheit) sind ebenfalls nichts weiter als Kompositionen von Gattern (das was rechnet) kombiniert mit Registern (das was kleine Informationseinheiten enthält), die mit anderen Einheiten über den [Bus](def-bus) (das was Daten von einer Einheit zur anderen transportiert) verbunden sind.

```{admonition} Central Processing Unit (CPU)
:name: def-cpu
:class: definition
Der *Hauptprozessor* oder *Central Processing Unit (CPU)* besteht aus Leitungen, Registern, der Kontrolleinheit, der arithmetische/logische Einheit und möglicherweise spezielle Einheiten für bestimmte Berechnungen wie etwa die Fließkomma-Recheneinheit.
Die CPU ist die Kernkomponente eines Computers, die für die Ausführung von Anweisungen aus Computerprogrammen verantwortlich ist.
Sie interpretiert und führt Befehle aus dem Arbeitsspeicher aus und verarbeitet Daten, indem sie arithmetische und logische Operationen durchführt.
```

*Register* sind die kleinsten aber auch schnellsten *flüchtigen* (engl. volatile) Speichereinheiten.
Sie sind dafür gedacht die Variablen einer Operation zu halten.
Addieren wir zum Beispiel zwei Zahlen $x$ und $y$ so werden die Werte aus zwei Registern gelesen, die Gatter verrichten ihre Arbeit und legen das Ergebnis in einem neuen Register ab.
Der Programmcode hierfür könnte wie folgt aussehen:

$$\text{ADD } \text{Reg}_1 \text{ Reg}_2 \text{ Reg}_3$$

Was soviel heißt wie: Addiere Zahl in Register 1 mit Zahl in Register 2 und speicher das Ergebnis in Register 3.
Register wie auch der Hauptspeicher werden aus den gleichen elektrischen Grundbauteilen wie Gatter konstruiert.
Sogenannte *Flip-Flops* können, anders als reine Logikgatter, elektrische Einheiten stabil halten und freigeben.
Konzeptionell sind sie eine Kombination aus rückgekoppelten Logikgatter.
Für die Speicherung von Bits benötigen sie allerdings eine Stromversorgung.
Deshalb sind Register wie auch der Hauptspeicher *flüchtig* - sie verlieren alle Daten sobald die Stromverbindung unterbrochen wird.

```{admonition} Register
:name: def-register
:class: definition
*Register*, sind extrem schnelle kleine flüchtige Speichereinheiten innerhalb der CPU, welche die CPU für viele Operationen verwendet.
```

Deshalb werden Programme und viele Daten als Binärcode oder in anderen Formaten auf einem *persistenten* (*nicht flüchtigen* / engl. *non-volatile*) Speicher wie einer Festplatte *persistent* gespeichert.
Sie werden vor ihrer Ausführung in den Hauptspeicher geladen.
Wie und von wem?
Das sehen wir gleich.
Die *Flüchtigkeit* der Speicher verleiht ihnen Geschwindigkeit, d.h. es ist möglich in sehr kurzer Zeit Daten von einen *flüchtigen* Speicher zu lesen und in ihn zu schreiben.
Der Geschwindigkeitsunterschied ist enorm.
Anstatt in die nächst gelegene Stadt zu reisen (Hauptspeicher), fliegen wir zum Mond (Festplattenspeicher).

```{figure} ../../figs/digital-computer/informationcycle/memory-cache-register.png
---
width: 450px
name: fig-memory-cache-register
---
Zusammenhang zwischen Größe und Geschwindigkeit der verschiedenen *flüchtigen* Speicher des Computers.
```

```{admonition} Cache
:name: def-cache
:class: definition
Ein *Cache* ist ein schneller, temporärer Speicherbereich, der dazu dient, häufig verwendete Daten oder Anweisungen zwischenzuspeichern, um den Zugriff darauf zu beschleunigen. 
Er ist eine Art (kleiner) Puffer.
Er enthält einen (kleinen) Teil der Daten die zeitlich gesehen gerade verwendet werden.
Er dient dazu wiederholte Zugriffe auf ein langsames Hintergrundmedium (wie den Hauptspeicher) zu vermeiden.
Durch die Nähe zum Prozessor oder zu anderen wichtigen Komponenten minimiert der Cache die Zeit, die für den Datenaustausch benötigt wird, und erhöht dadurch die Systemleistung. 
```

Zwischen Hauptspeicher und Register liegen weitere sehr schneller Speicher, die wir als *Cache* bezeichnen.
Für unser Verständnis der Funktionsweise können wir sie ignorieren.
Caches sind deutlich kleiner als der Hauptspeicher.
Sie beinhalten die Daten die zuletzt von der CPU verwendet wurden.
Fordert die CPU diese Daten erneut an, so ist der Zugriff über den Cache noch einmal viel schneller als über den Hauptspeicher.
Dieses Konzept wird verallgemeinert und so gibt es mehrere Caches die hintereinandergeschaltet sind.
Auch der Cache ist natürlich *flüchtig*.

```{admonition} Von-Neumann vs. Harvard-Architektur
:class: remark
:name: remark-neumann-vs-harvard

Eine weitere beachtenswerte Architektur ist die sog. *Harvard-Architektur*.
Im Unterschied zur *Von-Neumann-Architektur* hat sie zwei unterschiedliche und separierte Speicher, einen für den Programmcode und einen für die zu verarbeitenden Daten.
Das verkompliziert die Architektur und erfordert mehr Bauteile, jedoch kann die CPU **gleichzeitig** Programmcode laden als auch in den [Hauptspeicher](def-main-memory) schreiben oder aus ihm lesen.

```

Wie spielen die verschiedenen Einheiten der Architektur nun zusammen?
Folgende Beschreibung liefert eine vereinfachte konzeptionelle Antwort:

*Eingabegeräte* wandeln die eingelesenen Informationen ins Binärsystem um.
Die [CPU (Central Processing Unit)](def-cpu) manipuliert Informationen, wobei sie durch den *Speicher*, d.h. einen Zustand, unterstützt wird.
Am Ende des Informationskreislaufs wandeln *Ausgabegeräte* die verarbeiteten Informationen in Bild, Ton und andere Formate um.
Die *Ausgabe* des Computers muss nicht zum Konsum für uns Menschen gedacht sein.
Sie kann auch als *Eingabe* für andere Computer oder Maschinen dienen.

Damit die [Bits](def-bit) und [Byte](def-byte) nicht durcheinander gelesen, manipuliert und geschrieben werden ist die CPU *getaktet*.
Es gibt eine (global) tickende Uhr, die vorgibt wann die Komponenten aktiv werden können.
Bei jedem Tick oder anders gesagt, in jedem *CPU-Zyklus*, können die jeweiligen Komponenten aktiv werden.
Eine CPU, die mit 3 Gigahertz (GHz) getaktet ist, führt 3 Milliarden Zyklen in der Sekunde durch.
Nicht jede Berechnung oder jeder Speichertransfer benötigt die gleiche Anzahl an Zyklen.
Zum Beispiel benötigt die Division zweier Zahlen deutlich mehr Zyklen als die Addition.

## Das Betriebssystem

Soweit so gut.
Wie funktioniert das aber im Detail?
Was passiert zum Beispiel, wenn ich in meinem Textverarbeitungsprogramm die Taste ``A`` drücke.
Auf dem Bildschirm erscheint ein ``A``-Zeichen, wie ist diese Magie zu erklären?
Nun bevor wir dazu kommen, müssen wir überlegen was hierzu nötig ist:

1. Der Computer muss hochgefahren sein und
2. das Textverarbeitungsprogramm muss gestartet sein.

Wie aber startet der Computer?
Wie führt er nicht nur einzelne Operationen sondern ein ganzes Programm aus?
Und wie ist es möglich, dass scheinbar gleichzeitig viele verschiedene Programme auf einem Computer laufen?
Antworten finden wir wenn wir uns das "Masterprogramm" eines Computers ansehen: Das *Betriebssystem*.

```{admonition} Betriebssystem
:name: def-operating-system
:class: definition
Das *Betriebssystem* eines Computers ist ein spezielles Hauptprogramm, welches alle anderen Programme und die Rechnerressourcen des Computers verwaltet.
```

Das *Betriebssystem* (z.B. Ubuntu, Windows 10, Mac OS) bestimmt wann, welches Programm, welche Hardware nutzen darf und auf welchen Speicherbereich das jeweilige Programm und der jeweilige Benutzer zugreifen darf.
Hat ein Computer nur eine CPU (mit nur einen Kern), so erscheint es nur so als würden viele Programme gleichzeitig laufen.
In der Realität wechselt das Betriebssystem die aktiven Programme fortwährend durch.

Das *Betriebssystem* wird beim Start des Computers geladen.
Diesen Vorgang nennen wir *Booten*.
Aber wie soll das funktionieren?
Braucht es nicht ein Programm um das Betriebssystem zu laden und braucht dieses Programm nicht wieder ein Programm um es zu laden?
Befinden wir uns nicht in einem Henne-Ei-Problem?

```{admonition} Bootvorgang
:name: def-booting
:class: definition
Der *Bootvorgang* ist der Prozess, bei dem ein Computer nach dem Einschalten oder Neustarten sein Betriebssystem und weitere essenzielle Software lädt, um betriebsbereit zu werden.
```

Der Schlüssel hierzu ist ein kleineres Programm was auf dem sog. *Festwertspeicher (ROM)* liegt.
Dieses Programm wird von der Hardware selbst geladen.
Die Logik um das erste Programm vom *Festwertspeicher* zu laden ist also in den Bauteilen selbst fest verdrahtet (Software in Hardware gegossen).
Der Festwertspeicher kann nur gelesen werden und ist nicht flüchtig.
Das heißt, das Programm auf dem Festwertspeicher bleibt auch nach dem Ausschalten des Computers vorhanden.
Der Computer zieht sich quasi wie Münchhausen an den Haaren selbst aus dem Sumpf.

(sec-run-program)=
## Programme ausführen

Starten Sie ein Programm, sagen Sie eigentlich dem [Betriebssystem](def-operating-system), dass Sie dieses oder jenes Programm ausführen möchten.
Das *Betriebssystem* sorgt dafür, dass es in den Hauptspeicher geladen wird und teilt ihm entsprechende Ressourcen zu.
Erinnern Sie sich an die *[Von-Neumann-Architektur](von-neumann-architecture-2)*?
Laut dieser liegen die **Daten** als auch die **Programme** im gleichen (flüchtigen) *Hauptspeicher* bzw. *Arbeitsspeicher*.
Das Programm ist nichts anderes als eine zusammenhängende Folge von 0 und 1, welche Befehle repräsentieren.
Zum Beispiel bedeutet 

$$\text{ADD} \ \$5 \ \$6 \ \$7,$$

dass die Zahl, welche in Register $\$5$ steht, mit der Zahl, die in Register $\$6$ steht, addiert wird und das Ergebnis in den Register $\$7$ geschrieben werden soll.
Andere Befehle wie etwa

$$\text{LOAD} \ \#15 \ \$5 $$

oder

$$\text{STORE} \ \$7 \ \#16 $$

laden ($\text{LOAD}$) Daten aus dem Hauptspeicher an der Adresse (Stelle) $\#15$ ins Register $\$5$ bzw. speichern ($\text{STORE}$) die Daten von Register $\$7$ im Hauptspeicher an Adresse $\#16$.

Da Informationen mit einer unvorstellbaren Geschwindigkeit durch den Computer rasen, spielt die Distanz der Bauteile zueinander eine große Rolle.
Register sind nicht nur deutlich schneller als der *Hauptspeicher* sie befinden sich auch viel näher an den Recheneinheiten.

Wenn ein benötigter Wert noch im Register liegt (eventuell von einer zuvor ausgeführten Berechnung) wird dieser nicht erneut vom [Hauptspeicher](def-main-memory) geladen.
Stattdessen benutzt die CPU den Wert im Register und gewinnt dadurch an Berechnungsgeschwindigkeit.
Sie spart sich einige Zyklen die nötig wären um die Daten aus dem Speicher in den Register zu laden.

```{figure} ../../figs/digital-computer/informationcycle/program-run.png
---
width: 700px
name: fig-program-run
---
Zusammenspiel zwischen Kontrolleinheit und arithmetische/logische Einheit, Register, Befehlszeiger (CPU) und Arbeitsspeicher.
```

Innerhalb der *Kontrolleinheit* befindet sich ein spezielles *Register*, welches die *Arbeitsspeicheradresse* des nächsten auszuführenden Befehls enthält.
Dieses Register nennen wir *Befehlszähler* oder *Befehlszeiger*.
Ist der Befehl an der angegebenen Adresse ein *Sprungbefehl* ändert sich der Wert des *Befehlszeigers* entsprechend.
Andernfalls wird der Befehl (z.B. $\text{ADD } \text{Reg}_1 \text{ Reg}_2 \text{ Reg}_3$) von der CPU ausgeführt und der *Befehlszeiger* wird um 1 erhöht.

```{admonition} Befehlszeiger
:name: def-program-counter
:class: definition
Der *Befehlszeiger* ist ein spezielles [Register](def-register) der *Kontrolleinheit* welches die *Arbeitsspeicheradresse* des nächsten auszuführenden Befehls enthält.
Bei der Ausführung eines Programms wird der Befehlszeiger aktualisiert, um auf die nächste Anweisung zu zeigen, die ausgeführt werden soll.
```

Wenn das Betriebssystem entscheidet, dass ein anderes Programm an der Reihe ist, wird der aktuelle Zustand des laufenden Programms gesichert.
Z.B. wird der *Befehlszeiger* in den Arbeitsspeicher oder auf die Festplatte geschrieben.
Sobald das Programm wieder aktiv wird, werden alle notwendigen Daten wieder in den Hauptspeicher und die Register geladen.

```{exercise} CPU-Workflow
:label: cpu-workflow-exercise
Betrachten Sie das obige Bild {ref}`CPU-Workflow <fig-program-run>`.
Welche Befehle hat die CPU zuletzt ausgeführt und was wird der nächste Befehl bezwecken?
```

```{solution} cpu-workflow-exercise
:label: cpu-workflow-solution
:class: dropdown
Die Kontrolleinheit hat zum einen den Befehl $\text{ADD}$ inklusive der Registeradressen in Register geladen.
Dann hat sie die Werte 17 und 5, welche addiert werden sollen in Register der arithmetischen Einheit geladen.
Sie hat die arithmetische Einheit instruiert die Addition durchzuführen und das Ergebnis in Register $\$7$ abzulegen.

Im nächsten Schritt wird die Kontrolleinheit den Wert (22) dieses Registers ($\$7$) in den Hauptspeicher an die Adresse $\#16$ schreiben und somit den Wert 5 überschreiben.
```

## Der EVA-Kreislauf

Haben wir (1) den Computer *gebootet* und (2) das Textverarbeitungsprogramm gestartet und drücken dann ``A``, was passiert dann?
Das Eingabegerät (die Tastatur) sendet eine Unterbrechungsanforderung (Interrupt Request (IRQ)) an die CPU.
Nach der Anforderung führt die CPU eine Unterbrechungsroutine aus, diese leitet das ``A`` an das Textverarbeitungsprogramm weiter.

```{admonition} Interrupt Request (IRQ)
:name: def-irq
:class: definition
Ein *Interrupt Request* (IRQ) ist ein Signal, das an die CPU gesendet wird, um sie auf ein Ereignis oder eine Bedingung aufmerksam zu machen, die sofortige Aufmerksamkeit erfordert. Durch den Interrupt wird der aktuelle Ablauf des Programms unterbrochen, und die CPU führt eine spezielle Unterbrechungsroutine aus, um das gemeldete Ereignis zu behandeln. Anschließend wird die Ausführung des ursprünglichen Programms fortgesetzt.
*Interrupts* (Unterbrechungen) werden häufig für Hardware-Ereignisse, Zeitgeber oder zur Kommunikation zwischen verschiedenen Systemkomponenten verwendet.
```

Das Textverarbeitungsprogramm hat sich hierfür über eine *Arbeitsspeicheradresse* für einen solchen IRQ registriert.
Das heißt, es wird der Programmcode, der an dieser Adresse beginnt, ausgeführt.

Über viele tausende Operationen berechnet das Textverarbeitungsprogramm wie das ``A`` dargestellt werden soll (in welcher Schriftart, und welcher Position und so weiter).
Die Darstellung besteht aus vielen Pixeln welche das Programm an den Monitor weiterleitet.
Dieser wandelt die Folge aus 0 und 1 in viele unterschiedlich gefärbte Pixel um.


Computer arbeiten auf der Basis von zwei Zuständen (0 und 1).
Salopp sagt man auch, dass sie die Binärsprache "sprechen".
Da die kleinste Informationseinheit, das [Bit](def-bit), nur zwei Zustände annehmen kann, sind die Operationen äußerst simpel.
Die Komplexität und die damit einhergehende Rechenfähigkeit entsteht durch das Kombinieren und Hintereinanderschalten von Millionen dieser Operationen.

Als *Programmier* kümmern wir uns kaum um die genaue Manipulation der [Bits](def-bit) und [Bytes](def-byte).
Wir Abstrahieren diese Aufgabe durch [Programmiersprachen](sec-programming-languages), die uns weitaus komfortablere Möglichkeiten bieten.
Dennoch sind diese Informationseinheiten und deren [Manipulation](sec-manipulation) von wesentlicher Bedeutung, um die Funktionsweise eines Computers zu verstehen.

In einem Computer befinden sich mikroskopisch kleine Leitungen und Schaltkreise, welche alle Informationen eines Computers speichern, übertragen und verarbeiten.
Anstatt 0 und 1 verwendet der Computer also eigentlich elektrische Signale bzw. Spannungen, gespeichert in Milliarden von Transistoren und übertragen durch sog. [Bus-Systeme](def-bus) (Leitungen/Kabel).

Wie aber lassen sich Informationen mit solchen elektrischen Signalen darstellen?
Stellen wir uns eine Lampe mit zwei Zustände vor.
Die Lampe ist entweder aus (0) oder sie ist an (1).

```{figure} ../../figs/digital-computer/representation/lamps.png
---
width: 200px
name: fig-lamps
---
Eine Lampe die entweder aus (links) oder an (rechts) geschaltet sein kann.