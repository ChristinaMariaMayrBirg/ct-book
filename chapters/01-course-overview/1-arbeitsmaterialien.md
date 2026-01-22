---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

# Empfohlene Arbeitsmaterialien
Entweder sind Sie gerade auf der interaktiven Website unterwegs oder Sie haben das Skript vor sich liegen. So oder so: Schritt 1 ist geschafft – Sie haben bereits mindestens einen Teil Ihrer Arbeitsmaterialien erfolgreich im Einsatz.

Damit Sie die Inhalte der Vorlesung möglichst effizient bearbeiten können, empfehle ich Ihnen:

- die interaktive Website zu nutzen.
- sich das Vorlesungs-Skript (siehe [Downloads](../misc/downloads.html)) zuzulegen.




```{admonition} Hinweis
:name: remark-sample
:class: remark
Falls noch nicht geschehen: Melden Sie sich zum Moodle-Kurs an. Den Kursnamen auf Moodle sowie das Passwort erhalten Sie in der ersten Vorlesung. Falls Sie dort nicht anwesend sein können, kontaktieren Sie bitte Ihre Dozentin.
```

Die Website und das Skript sind thematisch identisch.
Das Skript dient Ihnen dazu, während der Vorlesung Notizen zu machen.
Auf der interaktiven Website können Sie viele der gezeigten Programmierbeispiele direkt im Webbrowser ausführen. Sie können also entweder live während der Vorlesung mitmachen oder die Beispiele später in Ruhe zu Hause nacharbeiten, verändern und erweitern.

## Wie und wann kann ich Python-Code auf der Website ausführen?

Nicht alle Seiten auf dieser Website enthalten ausführbaren Python-Code.
Ob eine Seite ausführbaren Code enthält, erkennen Sie daran, ob im Menü eine Rakete angezeigt wird.

```{figure} ../../figs/01-course-overview/code-ausfuehren1.png
---
width: 700px
name: fig-code-ausfuehren1
---
Beispiel einer Seite mit Rakete im Menü (Seite enthält ausführbaren Code).
```
Python-Code erkennen Sie außerdem daran, dass er in einer Code-Zelle steht – einer Art „Box“ mit abgerundeten Ecken.

Um Python-Code interaktiv auf der Website auszuführen, klicken Sie zunächst auf die Rakete und wählen dann „Live Code“ aus.

```{figure} ../../figs/01-course-overview/code-ausfuehren2.png
---
width: 700px
name: fig-code-ausfuehren2
---
Die Rakete öffnen und „Live Code“ auswählen, um interaktive Ausführung zu aktivieren.
```

Danach müssen Sie einmalig warten (zwischen ca. 5 Sekunden und 2 Minuten). In dieser Zeit wird Python im Hintergrund für Sie eingerichtet. Sie müssen sich um nichts kümmern. Sobald die Einrichtung abgeschlossen ist, können Sie auf der Website zwischen Seiten wechseln und neue Code-Zellen ausführen, ohne noch einmal warten zu müssen.

```{figure} ../../figs/01-course-overview/code-ausfuehren3.png
---
width: 700px
name: fig-code-ausfuehren3
---
Während der Einrichtung läuft die Statusanzeige; fertig ist es bei „ready“.
```
Die Einrichtung ist erfolgreich, wenn die Statusmeldung „ready“ erscheint.
Ab diesem Zeitpunkt sehen Sie bei jeder Code-Zelle ein Menü.

Sie können den Code nun beliebig anpassen und beliebig oft über „Run“ ausführen.

```{figure} ../../figs/01-course-overview/code-ausfuehren4.png
---
width: 700px
name: fig-code-ausfuehren4
---
Über das Zellen-Menü können Sie Code ausführen („Run“) und erneut starten.
```

Am besten testen Sie es gleich hier auf dieser Seite: Aktivieren Sie „Live Code“ über die Rakete, ändern Sie die folgende Code-Zelle ab, und führen Sie sie über „Run“ aus.


```{code-cell} python3
:tags: [skip-execution]
myname = "Christina"
print("hello")
print(myname)
```

## Notfalllösung (JupyterHub)

Falls die Einrichtung von „Live Code“ einmal fehlschlägt, können Sie die Beispiele alternativ im **JupyterHub der Hochschule München** ausführen. Die Oberfläche sieht dort etwas anders aus, aber das Prinzip ist identisch: Sie arbeiten mit Zellen, die Sie ausführen können.

Eine kurze Anleitung finden Sie im Expertenwissen unter [Jupyter Notebooks](../misc/Expertenwissen/jupyter-notebooks.html).

Sie starten den JupyterHub über die Rakete, indem Sie „JupyterHub“ auswählen:

```{figure} ../../figs/01-course-overview/fallback.png
---
width: 400px
name: fig-jupyterhub-fallback
---
Notfall-Variante, wenn „Live Code“ nicht funktioniert.
```




