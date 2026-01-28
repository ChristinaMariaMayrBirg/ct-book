# Wie werden Programme entwickelt?

** Grundprinzip: Einkaufsteile vs. Eigenentwicklung**

Softwareentwicklung und Hardwareentwicklung unterscheiden sich gar nicht so stark. Eine zentrale Frage ist immer: Was muss ich selbst entwickeln und was kann ich einkaufen?

Beispiel Hardware: Wenn Sie einen Motor entwickeln, ist die Schraube vermutlich ein Einkaufsteil. Sie kaufen eine Schraube, die Ihren Anforderungen entspricht, aber Sie entwickeln nicht den Herstellungsprozess der Schraube.

Beispiel Software: Ähnlich ist es mit Software: Es gibt sehr viele Einkaufsteile (Bibliotheken), die Sie einfach nutzen können! 

In diesem Kapitel werden wir uns ansehen anhand eines Praxisbeispiels ansehen wie Programmieraufgaben üblicherweise in der Praxis umgesetzt werden.

```{exercise} Fallbeispiel: Sensordaten statistisch auswerten
:label: exercise-sensordata

**Ausgangslage:**
Julia bekommt von ihrer Kollegin eine Datei mit echten Messwerten, die die NO2-Konzentration an verschiedenen Flughäfen zu unterschiedlichen Zeitpunkten... 


**Aufgabe:**
Die Statistik der Messdaten soll bestimmt werden:
- Grafisch: Die Verteilung der Daten visualisieren
- Tabellarisch: Eine Übersichtstabelle erstellen, in der die statistischen Momente und Percentile enthalten sind
```

## Datensatz

Die Datei mit den Messdaten liegt auf github:

url = "https://raw.githubusercontent.com/pandas-dev/pandas/main/doc/data/air_quality_no2.csv"


Die verwendeten Daten sind reale Messdaten zur Stickstoffdioxid-Konzentration (NO₂) in der Umgebungsluft.

- Gemessen in µg/m³ (Mikrogramm pro Kubikmeter)
- Zeitlich aufgelöste Messreihen (Zeitstempel)
- Mehrere städtische Messstationen in Europa (z. B. London, Paris, Antwerpen)

Die Daten stammen aus öffentlichen Umweltmessstationen (u. a. nationale Umweltbehörden, European Environmental Agency). Die Messdatei stammt aus der pandas-Dokumentation und wurden für Lehr- und Demonstrationszwecke leicht vorverarbeitet, in der Größe reduziert, und in ein CSV-Format überführt.

Es handelt sich nicht um synthetische Daten, sondern um reale Messwerte mit typischem Messrauschen, Ausreißern und fehlenden Werten.



