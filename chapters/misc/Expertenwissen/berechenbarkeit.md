(sec-expert-berechenbarkeit)=
# Berechenbarkeit & Turing-Vollständigkeit (Expertenwissen)

Dieses Kapitel ist **optional** und dient als Hintergrundwissen zur theoretischen Informatik.
Im Haupttext der Vorlesung reicht es, die Begriffe grob einordnen zu können.

## Berechenbarkeit

```{admonition} Berechenbarkeit
:name: def-turing-computable
:class: definition

Ein Problem ist *allgemein berechenbar*, wenn es einen Algorithmus gibt, der für jede gültige Eingabe eine Lösung berechnen kann.
```

Ein zentrales Ergebnis der theoretischen Informatik ist: Es gibt Probleme, die **nicht** allgemein berechenbar sind.

## Das Halteproblem (Idee)

Das *Halteproblem* ist das bekannteste Beispiel: Es gibt keinen Algorithmus, der für ein beliebiges Programm und eine beliebige Eingabe entscheiden kann, ob das Programm mit dieser Eingabe jemals terminiert (anhält) oder in einer Endlosschleife läuft.

Warum ist das relevant?
- Es setzt prinzipielle Grenzen, was automatische Tools leisten können (z. B. „Beweise mir automatisch, dass dieses Programm nie hängt“).
- Es erklärt, warum manche Analysen in der Praxis nur **approximativ** oder für eingeschränkte Programmmengen möglich sind.

## Turing-Vollständigkeit

```{admonition} Turing-Vollständigkeit
:name: def-turing-complete
:class: definition

Ein System oder eine Programmiersprache ist *Turing-vollständig* (engl. *Turing-complete*), wenn sie all das berechnen kann, was eine Turingmaschine berechnen kann.
```

Intuition: Eine Programmiersprache ist „ausdrucksstark genug“, um prinzipiell jede berechenbare Funktion formulieren zu können.
Viele Sprachen (z. B. Python, Java, C) gelten als Turing-vollständig.

## Mini-Check

- Warum kann ein „Entscheider fürs Halteproblem“ nicht existieren (in einem Satz)?
- Was meint „Turing-vollständig“ – und was sagt es *nicht* über Laufzeit/Performance aus?

