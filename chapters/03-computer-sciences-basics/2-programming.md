(sec-programming)=
# Programmieren

Programmieren ist eine Tätigkeit bei der wir unsere Ideen und Konzepte in Text überführen.
Ob das Programmieren nun wirklich mit dem Schreiben des Codes beginnt oder wir den ganzen Prozess der Softwareentwicklung als das Programmieren betrachten sei dahingestellt.
Auch ist klar, dass geschriebener Code wie auch die Betrachtung von Code neue Ideen hervorrufen wird und zu neuen Lösungen führen wird.

Als gute Programmierer\*innen müssen wir 

+ unseren Kontext kennen,
+ logisch und mathematisch Denken können,
+ uns exakt ausdrücken können und uns auch unmissverständlich mit anderen austauschen können und
+ unsere Entwicklungswerkzeuge beherrschen können.
  
Wir benötigen ein Grundverständnis davon wie ein [Computer funktioniert](sec-information-processing) und wie wir uns in der abstrakten Welt der [Kontroll-](sec-control-structures) und [Datenstrukturen](sec-data-structures) ausdrücken können.

## Begrifflichkeiten

Die Begriffe *Algorithmus*, *Pseudocode*, *Programmcode* und *Programm* ähneln sich sehr und wir haben noch keine strickte Differenzierung durchgenommen.
Im Abschnitt [Algorithmen](sec-algorithms) ist klar definiert, was genau ein Algorithmus ist.

```{admonition} Pseudocode
:name: def-pseudocode
:class: definition

*Pseudocode* ist eine einfache, weniger strikte Beschreibung eines Algorithmus in einer Sprache, die der natürlichen Sprache ähnelt.
```

Mit *Pseudocode* können wir einen Algorithmus in einer Sprache beschreiben, die keine bestimmte Programmiersprache zur Basis hat.

```{admonition} Programm
:name: def-program
:class: definition

Ein *Programm* ist eine Folge von Instruktionen, die ein konkreter Computer (über die Umwege eines [Übersetzers](def-compiler) oder [Interpreters](def-interpreter)) ausführen kann.
```

Ein *Algorithmus* ist eine wohldefinierte Sequenz von Anweisungen, welche eine Lösung für ein bestimmtes Problem berechnet.
Er kann in der Form von *Pseudocode* niedergeschrieben werden, sofern die Beschreibung alle Eigenschaften für einen Algorithmus erfüllt.
Er kann aber auch in einer ganz anderen Form niedergeschrieben werden, z.B., einem Flussdiagramm.

*Pseudocode* orientiert sich an der Syntax von Programmiersprachen, wird aber sprachenübergreifend verwendet.

Ein *Programm* ist im Gegensatz dazu in einer Programmiersprache wie ``Python`` geschrieben und kann auf einer Maschine ausgeführt werden.
*Programmiercode* auch genannt *Quellcode*, *Source Code* oder kurz *Code*, ist das Resultat der *Programmierung* und teil eines *Programms*.
Das heißt zur Ausführung des *Quellcodes* fehlt möglicherweise ein Teil des gesamten Codes.

*Pseudocode*, *Quellcode*, *Programme* und *Algorithmen* sind verschiedene Formen, um Problemlösungen in endlichem Text zu beschreiben.

Ein *Algorithmus* kann auch in einer Programmiersprache niedergeschrieben werden.
Dies werden wir in diesem Kurs bevorzugen und den Umweg über *Pseudocode* weitestgehend vermeiden.



## Kenne deinen Kontext

Das Entwerfen eines Algorithmus und das Programmieren gehen fließend ineinander über.
Oftmals, gerade bei einfachen Problemen, entwerfen Sie ihren Algorithmus indem Sie ihre Gedanken in Programmiercode umwandeln.
Bei komplexeren Problemen ist es jedoch oft ratsam zu Stift und Papier zu greifen durch Skizzen und Mitschriften zu unterstützen.


Ein wesentlicher Teil der Problemlösung findet vor dem Programmieren statt.
Das Programmieren ist dann die Realisierung der Lösung.
Ist Ihr Algorithmus, den Sie programmieren möchten, gut durchdacht und kennen Sie Ihren *Kontext* gut genug, dann ist das schreiben des Programmcodes oft keine allzu große Herausforderung mehr.

Wenn wir vom Programmieren sprechen, meinen wir oft beides:

1. Das Entwerfen eines Algorithmus und
2. dessen Realisierung (*Implementierung*) durch eine Programmiersprache.
