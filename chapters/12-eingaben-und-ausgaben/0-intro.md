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

# Eingaben und Ausgaben

In den vorherigen Abschnitten haben wir verschiedene *built-in* Datentypen von Python kennengelernt: Zahlen, Listen, Tupel, Zeichenketten, Mengen und Wörterbücher.
Diese Datentypen existieren jedoch nicht isoliert in unserem Programm.
In der Praxis müssen Programme häufig mit Daten arbeiten, die von außen kommen:
- von anderen Programmen
- von Nutzerinnen und Nutzern
- aus Dateien

Ebenso müssen Programme ihre Ergebnisse nach außen kommunizieren:
- an andere Programme
- an Nutzerinnen und Nutzer
- in Dateien

Diese Kommunikation mit der Außenwelt erfordert **Konvertierung von Datentypen**, da externe Daten meist nicht im gewünschten Datentyp vorliegen und interne Daten für die Ausgabe in ein geeignetes Format umgewandelt werden müssen.

## Eingaben (Input)

Konvertierung ist notwendig, wenn wir Input von außerhalb unseres Programms erhalten.
Dies kann auf verschiedene Weise geschehen:

**Fall 1: Input-Dateien**
Sie haben Messwerte in einer Excel-Tabelle (Input-Datei) abgelegt.
Diese möchten Sie nun in Ihrem Python-Programm weiterverarbeiten.

**Fall 2: Netzwerkkommunikation**
Ein anderes Programm berechnet Daten und kommuniziert diese direkt über eine Netzwerkverbindung an Ihr Programm.

**Fall 3: Nutzereingaben**
Ein Anwender kommuniziert seine Eingaben über eine Schnittstelle (z. B. Command Line Interface oder grafische Benutzeroberfläche).

## Ausgaben (Output)

Ebenso müssen wir Daten aus unserem Programm herausgeben.
Die Ausgabe kann auf verschiedene Weise erfolgen:

**Fall 1: Ausgabe-Dateien**
Sie möchten Ergebnisse in eine Datei schreiben (z. B. CSV, JSON, Textdatei).

**Fall 2: Netzwerkkommunikation**
Ihr Programm sendet Daten über eine Netzwerkverbindung an ein anderes Programm.

**Fall 3: Nutzerausgaben**
Ein Programm kommuniziert Ergebnisse an den Anwender über eine Schnittstelle (z. B. Terminal, Jupyter Notebook, grafische Benutzeroberfläche).

## Was erhalten wir über diese Schnittstellen?

Über diese Schnittstellen erhalten Programme in der Regel entweder:
- **Symbole (Text)**
- **Bytes**

```{admonition} Hinweis: Protokolle in Python
:name: tip-protocols-in-python
:class: tip

Ob Sie Symbole (Text) oder Bytes über eine Schnittstelle erhalten, hängt vom **verwendeten Protokoll** ab.

Wenn Sie in Python eine Funktionalität nutzen, die Kommunikation nach außen ermöglicht,  
lesen Sie immer nach, **welches Protokoll** dabei verwendet wird.

Grundsätzlich unterscheidet man:

1. **Textbasierte Protokolle**  
   Daten werden als Zeichen übertragen.  
   Beispiele: ``stdin/stdout``, HTTP (Text), JSON

2. **Binäre Protokolle**  
   Daten werden als Bytes übertragen.  
   Beispiele: TCP/IP
```

Unabhängig davon, ob wir Bytes oder Text bekommen, müssen wir uns darum kümmern, dass deren ursprüngliche Bedeutung in unserem Programm wiederhergestellt wird.

Nehmen wir an, wir haben den Text

```
"Meine Zahlen: 2,3,4"
```

erhalten.
Die Zeichen "2", "3" und "4" sind hier Text und keine echten Zahlen.
Zum Rechnen brauchen wir aber echte Zahlen.

**Wie sollen wir daraus wieder Zahlen herstellen?**

Wir müssen zwei Schritte durchführen:

1. **Konvertierung**: Das Objekt, das wir bekommen haben, umwandeln (z. B. Text "2" in die Zahl 2)
2. **Validierung**: Überprüfen, ob die Eingabe dem erwarteten Format entspricht

## Was geben wir über diese Schnittstellen aus?

Bei der Ausgabe müssen wir unsere internen Datentypen in ein Format umwandeln, das über die Schnittstelle übertragen werden kann.
In der Regel bedeutet das:
- **Konvertierung zu Text (String)**: Zahlen, Listen, Wörterbücher etc. werden zu Zeichenketten umgewandelt
- **Formatierung**: Die Darstellung wird so gestaltet, dass sie für den Empfänger verständlich ist

Die Funktion `print()` übernimmt diese Konvertierung automatisch für uns, aber es ist wichtig zu verstehen, was dabei passiert.

Im Folgenden sehen wir uns exemplarisch an, wie Eingaben und Ausgaben in Python funktionieren:
- **Eingaben**: Wie wir Daten von Nutzerinnen über Command Line Interface oder grafische Benutzeroberflächen erhalten
- **Ausgaben**: Wie wir Daten mit `print()` ausgeben und formatieren

