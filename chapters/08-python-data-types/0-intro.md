---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

(sec-python-data-types)=
# Datentypen (Grundlagen)

Wie in Abschnitt [Repräsentation](sec-representation) beschrieben, befinden sich im Speicher des (digitalen) Computers ausschließlich [Bits](def-bit).
Sie können sich den Speicher als eine lange lange Liste von Bits vorstellen.
Diese Bits können nur einen von zwei Zuständen (0 und 1) annehmen.
Dennoch verarbeiten Computer Zahlen, Text, Bilder und mehr.

```{figure} ../../figs/python-tutorial/variables/ram.png
---
width: 400px
name: fig-ram-2
---
Der Arbeitsspeicher ist eine sehr lange Liste bestehend aus [Bits](def-bit).
Die Adresse ist im Wesentlichen die Nummer / der Index eines bestimmten Speicherplatzes.
```

Diese "Magie" geschieht durch die Wahl und Implementierung einer [Interpretation](sec-interpretation).
Unterschiedliche Interpretationen ermöglichen es, Bits und [Byte](def-byte) als Zahlen, Text, Bilder usw. zu verarbeiten.

Der *Datentyp* einer Variablen gibt an, wie die [Bits](def-bit) und [Bytes](def-byte) [interpretiert](sec-interpretation) werden.
Die Bits und Bytes des Speicherbereichs, auf welchen die Variable *zeigt*, machen den *Wert* der Variablen aus.
Im folgenden definieren und initialisieren wir Variablen mit unterschiedlichen Datentypen: 

+ [Ganze Zahl](sec-int) ``int``, 
+ [Fließkommazahl](sec-float) ``float``, 
+ [Zeichenkette](sec-string) ``str``, 
+ [Wahrheitswert](sec-bool) ``bool``, 
+ eine [Liste](sec-list) ``list``, welche ganze Zahlen ``int`` enthält und
+ ein [Tupel](sec-tuple) ``tuple``, welche Zeichenketten ``str`` enthält.

```{code-cell} python3
number = 111
floating_number = 1.3
characters = 'Hello'
boolean = True
mylist = [1,2,3,4]
mytuple = ('A', 'B', 'C')
```

Beim Datentyp ``list`` und ``tuple`` fällt auf, dass diese Werte eines anderen Datentyps enthalten, hier ``int`` und ``str``.
Solche Datentypen nennen wir [zusammengesetzt Datentypen](sec-datastructures)) wohingegen wir Datentypen, welche wir nicht zerlegen können als [atomare Datentypen](def-atomare-data-types) bezeichnen.
Diese *atomaren Datentypen* können zudem auch [atomare Datentypen](def-primitive-datatypes) sein.

Zudem gibt es Datentypen, welche von der jeweiligen Programmiersprache definiert sind und solche die Sie selbst definieren.
Erstere nennen wir *built-in Datentypen* und letztere werden durch *Klassen* realisiert.
Wir werden auf [Klassen](sec-class-and-object) erst am Ende des Kurses eingehen.

In Kapitel haben wir bereits gesehen, dass es 5 Kategorien an Datentypen gibt.

1. Primitive Datentypen,
2. atomare Datentypen
3. zusammengesetzte Datentypen,
4. built-in Datentypen und
5. eigens definierte Datentypen.


Die von ``Python`` vorab definierten Datentypen nennt man *built-in Datentypen*. Ziel der Veranstaltung ist es dass sie die built-in Datentypen kennen, die in der Praxis besonders häufig verwendet werden. 
Eine vollständige Liste der Datentypen finden Sie im Abschnitt [Built-in Datentypen](sec-built-in-data-types).

Um genau zu sein lassen sich *built-in Datentypen* in zwei Typen unterteilen: 

1. *Atomare Datentypen*, also Datentypen die sich auf einen einzelnen Wert beziehen und
2. *Zusammengesetzt Datentypen*

Haben Sie bereits Programmiererfahrung, so werden Sie *atomare Datentypen* als *primitive Datentypen* wahrnehmen, doch streng genommen gibt es in ``Python`` keine primitiven Datentypen.

```{admonition} Python und primitive Datentypen
:name: theorem-primitive-data-types-in-python
:class: theorem

Es gibt in ``Python`` keine primitiven Datentypen.
```

Der Wert eines *atomaren Datentyps* lässt sich nicht sinnvoll weiter in seine Einzelteile zersplittern.

*Zusammengesetzte Datentypen* sind zum Beispiel: Zeichenketten ``str``, Listen ``list``, Tupel ``tuple``, Mengen ``set`` und Wörterbücher ``dict``.

Den Datentyp einer Variable oder eines Wertes erfragen Sie mit der *built-in* Funktion ``type``.

```{code-cell} python3
x = 5
text = 'Hello'
print(type(x))
print(type(text))
print(type(3.1))
```

(sec-atom-data-type)=
## Atomare Datentypen 

Eine wesentlich Eigenschaft von *atomaren Datentypen* ist die Unveränderbarkeit ihres des Werts.
Der **Wert** einer Variable eines *atomaren Datentyps* liegt **unverändert** im Speicher.

```{admonition} Atomare Datentypen
:name: def-atomare-data-types
:class: python

*Datentypen* welche sich auf einen einzelnen Wert beziehen, d.h., ganze Zahlen ``int``, Wahrheitswerte ``bool`` und Gleitkommazahlen ``float`` sind *atomare Datentypen*.
```

Wird der **Wert** durch keiner Variablen adressiert, wird er (vom [Garbage Collector](def-garbage-collector)) zwar gelöscht.
In anderen Worten, wird der Speicher von Ihrem laufenden Programm nicht mehr benötigt, kümmert sich der Garbage Collector, den von Ihnen belegten Speicher wieder freizugeben.
Der Speicher der durch einen Wert eines *atomaren Datentyp* belegt ist kann also durchaus verändert werden, allerdings nur dann wenn er nicht mehr gebraucht wird.

```{admonition} Unveränderliche atomare Datentypen
:class: theorem
:name: theorem-immutable-atom-data-types
Atomare Datentypen sind *unveränderlich*.
```

Wir haben dieses Phänomen bereits im Abschnitt [Variablen](sec-variables) beobachtet.
Wir hatten festgehalten, dass Veränderungen der einen Variablen keinen Effekt auf die **Adresse** bzw. *Identität* ``id`` anderer Variablen haben.
Für *atomare Datentypen* gilt noch mehr: 

```{admonition} Unveränderliche atomare Datentypen
:class: remark
:name: remark-immutable-atom-data-types
Ändern wir den **Wert** einer Variable vom Typ ``int``, ``bool`` oder ``float``, so kann diese Änderung nicht den **Wert** einer anderen Variablen verändern.
```

Folgendes Beispiel illustriert diese Tatsache.

```{code-cell} python3
x = 12313
z = x
print(f'value of x = {x}')
print(f'id of x = {id(x)}')

print(f'value of z = {z}')
print(f'id of z = {id(z)}')
print('change value of x')
x = 11341
print(f'value of x = {x}')
print(f'id of x = {id(x)}')

print(f'value of z = {z}')
print(f'id of z = {id(z)}')
```

(sec-datastructures)=
## Zusammengesetzte Datentypen

*Zusammengesetzte Datentypen* oder auch *Datenstrukturen* bestehen hingegen aus mehreren Werten.
Sie strukturieren diese Werte.

```{admonition} Zusammengesetzt Datentypen 
:name: def-data-structures
:class: python

Datentypen welche Sammlungen von Werten modellieren, bezeichnen wir als *zusammengesetzte Datentypen* oder *Datenstrukturen*.
```

Anders als bei *atomaren Datentypen* lässt sich der **Wert** einer Datenstruktur verändern.
D.h., der Inhalt der Datenstruktur kann in der Regel verändert werden.

Sie können sich eine Datenstruktur wie ein Behältnis aus der Realwelt vorstellen.
Einen Rucksack können wir mit Dingen befüllen, die wir möglicherweise nicht verändern können.
Der Rucksack selbst, lässt sich demnach sehr leicht verändern.
Wir müssen lediglich Elemente hinauswerfen oder einfügen.

Nehmen wir einmal an, eine Datenstruktur enthält ausschließlich ganze Zahlen ``int``.
Verändern wir nun eine dieser Zahlen, so wird der **Wert** im Speicher, der diese Zahl repräsentiert, nicht verändert -- es ist ja ein *atomarer Datentyp*!
**Aber** es wird ein neuer Wert in den Speicher geschrieben und die Datenstruktur wird so manipuliert, dass einer ihrer Einträge nun auf diesen neuen Wert zeigt.

Im Abschnitt [Listen und der Speicher](sec-list-and-memory) sehen wir uns an was genau im Speicher vor sich geht, wenn wir mit Listen arbeiten.
Dies kann auf andere *Datenstrukturen* übertragen werden.




## Primitive Datentypen

```{admonition} Primitive Datentypen
:name: def-primitive-datatypes
:class: definition

*Primitive Datentypen* sind jene Datentypen aus denen alle anderen Datentypen einer Sprache hervorgehen.
Sie sind nicht weiter reduzierbar.
```

Unsere Definitionen von [atomaren](def-atomare-data-types) und [primitiven](def-primitive-datatypes) Datentypen ähneln sich sehr.

>Worin besteht der Unterschied zwischen einem primitiven und einem atomaren Datentyp?

Nehmen wir zum Beispiel den ``Python`` Datentyp ``int``.
Der Wert vom Typ ``int`` besteht nicht nur ais dem reinen Wert der ganzen Zahl sondern enthält zusätzlich noch einen Zähler, welcher angibt wie viele Variablen auf den Wert verweisen.
Das heißt wir können ``int`` weiter in den Zähler und den eigentlichen Wert zerlegen.
Allerdings macht es keinen Sinn diese beiden Teile zu zersplittern und separat weiter zu verarbeiten -- sie gehören zusammen, da sie nur gemeinsam verarbeitbar sind!
Zeichenketten sind weder primitiv noch atomar, denn eine Zeichenkette lässt sich in ihre einzelnen Zeichen zersplittern und die Weiterverarbeitung der einzelner Zeichen macht durchaus Sinn.

Übertragen wir das auf die 'echte' Welt, so könnte man bei einem Brief von einem Wert eines [zusammengesetzten Datentyps](def-data-structures) sprechen.
Dieser enthält einen Briefkopf, ein Datum einen Absender, Empfänger und den Text.
Das Datum ist wiederum ein *zusammengesetzten Datentyp* bestehend aus Tag, Monat und Jahr.
Der Tag ist schließlich ein *primitiver* oder (in ``Python``) ein *atomarer* Datentyp (eine Zahl zwischen 0 und 31).

```{exercise} Der Datentyp Zeichenkette
:label: datatype-str-exercise
Ist ``set``, d.h. eine Menge, ein atomarer oder zusammengesetzter Datentyp?
Begründen Sie Ihre Antwort.
```

```{solution} datatype-str-exercise
:label: datatype-str-solution
:class: dropdown

``set`` ist ein zusammengesetzter Datentyp dessen Wert eine variable Anzahl an Werten verschiedener Datentypen enthalten kann.
```

(sec-built-in-data-types)=
## Built-in Datentypen

*Built-in* Datentypen sind jene Datentypen, welche die Programmiersprache (ohne weitere Bibliotheken) mitliefert:



```{figure} ../../figs/python-tutorial/datatypes/datatypes-hierachy.png
---
width: 100%
name: fig-python-datatypes-hierarchy
---
Die Standard-Typ-Hierarchie von Python (Quelle: Wikimedia Commons, basierend auf „Python 3. The standard type hierarchy“, CC BY-SA 4.0, Urheber: Максим Пе).
```

Diese Datentypen stehen Ihnen zur Verfügung sobald Sie ``Python`` auf Ihrem System oder Ihrer Umgebung installiert haben.

Anders als in vielen anderen Sprachen müssen Sie den (built-in) Datentyp einer Variablen in ``Python`` nicht explizit angeben.
``Python`` schließt von der Schreibweise des Wertes automatisch auf den richtigen Datentyp.

Eine Folge von Ziffern mit einem optional vorangestellten Minuszeichen werden als ganze Zahl ``int`` interpretiert.
Befindet sich in der Folge ein Punkt ``.`` so wird der Wert als Fließkommazahl interpretiert.
Sie können den Datentyp einer Variablen ``x`` oder eines Wertes mit ``type(x)`` abfragen:

```{code-cell} python3
type(-3123)
```

```{code-cell} python3
type(1.313)
```

```{code-cell} python3
name = 'Anna'
type(name)
```

```{code-cell} python3
mylist = [1, 2, 3, 4, 'A']
print(f'List Type: {type(mylist)}')
print(f'Element 0 Type: {type(mylist[0])}')
print(f'Element 4 Type: {type(mylist[4])}')
```

## Zusammengesetzte Datentypen

Zusammengesetzte Datentypen definieren wir durch andere Datentypen, welche bereits definiert wurden.
Die Basis der zusammengesetzten Datentypen sind deshalb entweder *built-in Datentypen* der Sprache oder eigens definierte zusammengesetzte Datentypen.

Angenommen Sie wollen den Datentyp ``Person`` definieren welcher sich dadurch auszeichnet, dass er sich aus zwei Zeichenketten ``str`` nämlich dem Vor- und Nachnamen zusammensetzt.
Durch [Klassen](sec-class-and-object) können Sie einen solchen Datentyp definieren.
Wie wir dies machen, werden wir auf einen späteren Zeitpunkt verschieben.

Listen ``list``, Tupel ``tuple``, Mengen ``set`` und Wörterbücher ``dict`` sind *zusammengesetzter built-in Datentypen* und zugleich enthalten die Werte (Objekte) dieser Datentypen eine
variable Anzahl an Elementen unterschiedlicher Datentypen.
Eine gute Analogie zu diesen sog, [Sammlung / Kollektion (engl. Collections)](def-collection) sind physikalische Ordner, Schließfächer, Listen auf Papier geschrieben, Rücksäcke, Körbe, Tüten und andere physikalischen Objekte die wir im Alltag verwenden um andere physikalische Objekte zu ordnen, strukturieren oder schlicht zu halten.
Auch der Arbeitsspeicher ist in diesem Sinne eine sowohl physikalische wie auch virtuelle Kollektion an Bits.

```{admonition} Sammlung (Collection)
:name: def-collection
:class: definition

Als *Sammlung* bezeichnen wir alle Datentypen ([Tupel](sec-tuple), [Dictionary](def-python-dictionary), [Listen](sec-list), [Mengen](sec-set) usw.), die eine **variable Anzahl** an anderen Elementen (normalerweise mehrere) beinhalten.

```

Mit **variabler Anzahl** ist gemeint, dass es Sammlung gibt, welche 5 Elemente enthalten und Sammlung gibt die 1000 Elementen enthalten.
Es kann dennoch sein, dass eine Sammlung die 10 Elemente enthält nicht verändert werden kann, d.h. sie wird auf immer dieser 10 Elemente enthalten.

```{code-cell} python3
mylist = [1, 2, 'A', 3, 1.23, [1, 2, 3]]
mylist
```

```{code-cell} python3
mytuple = (mylist, 'D')
mytuple
```

```{code-cell} python3
mydict = {'firstname' : 'Paulina', 'lastname' : 'Schmidt', 'age' : 23 }
mydict
```

```{code-cell} python3
month = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12}
month
```

Eine Zeichenkette ``str`` ist ebenfalls eine Kollektion, jedoch sind deren Elemente alle vom gleichen Typ -- dem Zeichen.


## Hintergrundwissen
Für dynamisch getypte Sprachen, erweitern wir unsere Sichtweise um die Datentypinformation.
Eine *Variable* kann demnach als Tripel, bestehend aus

+ **Wert**
+ **Datentyp**
+ **Adresse**

verstanden werden.
Die **Speicheradresse** der Variable zeigt in den Arbeitsspeicher an eine bestimmte Stelle.
Dort steht jedoch nicht nur der **Wert** sondern auch der **Datentyp**, d.h. die *Information* wie dieser **Wert** zu interpretieren ist.

```{figure} ../../figs/python-tutorial/datatypes/data-type-key-pair.png
---
width: 800px
name: fig-data-type-key-pair-2
---
Variablen für dynamische Typisierung: Eine *Variable* dargestellt als Tripel aus (Adresse, Datentyp, Wert). 
Datentyp und Wert stehen im Speicher. Die Variable 'kennt' ihre Adresse.
In diesem Beispiel benötigt die Datentypinformation 3 Bit und der Wert 8 Bit.
```

Woher wissen wir und der [Interpreter](def-interpreter), an welcher Stelle im Speicher die Datentypinformation endet?
Eine Möglichkeit ist es eine feste Anzahl an Bits für Datentypen festzulegen.
In {numref}`Abbildung {number} <fig-data-type-key-pair-2>` wären dies 3 [Bits](def-bit).

Dynamische Typisierung, wie sie in ``Python`` besteht, ähnelt dem Konzept der Dateiformate.
So könnten wir ein Bild im ``PNG`` oder ``JPEG``-Format als *(Wert, Dateiformat)* Tupel ansehen.
Der *Wert* ist durch die Bits, die das Bild als solches ausmachen definiert.
Das *Dateiformat* ``PNG`` oder ``JPEG`` gibt an, wie diese Bits von der Computerhardware wie auch Software interpretiert werden müssen, um das Bild auch als Bild verarbeiten zu können.

```{admonition} Datentypen
:name: def-datatypes
:class: definition
Ein *Datentyp* oder auch kurz *Typ* ist ein Attribut eines Werts, welches dem [Compiler](def-compiler) oder [Interpreter](def-interpreter) angibt, wie der Wert zu verwenden bzw. zu interpretieren ist.

```

Blicken wir auf folgenden Code und fragen uns was der Interpreter daraus macht.

```python
x = 3       # <x, int>
y = 5       # <y, int>
z = x + y   # int + int -> int

x = 1.3     # <x, float>
y = 3.5     # <y, float>
z = x + y   # float + float -> float
```

Für die erste Addition von ``x`` und ``y`` holt sich der Interpreter die Datentypinformation.
Er weiß demnach, dass ``x + y`` bedeutet, dass eine Addition von zwei ganzen Zahlen auszuführen ist.
Er wandelt den Code so um, dass die CPU angewiesen wird, zwei ganze Zahlen zu addieren.
Der Addierer der CPU wird aktiv und addiert die beiden Zahlen.
Für die zweiten Addition führt der Interpreter die gleiche Übersetzung durch, jedoch für zwei Fließkommazahlen.
Eine **andere** Einheit, die Fließkomma-Einheit, der CPU wird aktiviert!

