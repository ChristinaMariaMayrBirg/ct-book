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

# Python-Beispiele

Am besten testen Sie den Live-Code gleich selbst aus: Aktivieren Sie „Live Code“ über die Rakete und klicken Sie anschließend auf „Run“.


```{code-cell} python3
:tags: [skip-execution]

myname = "Christina"
print("hello")
print(myname)
```
Das ist nicht Ihr Name? Dann ändern Sie den Namen einfach ab und führen erneut „Run“ aus.

```{admonition} Mini-Aufgabe
:label: namechange

- Ändern Sie `myname` und führen Sie die Zelle erneut aus.
- Fügen Sie eine weitere Zeile `print(...)` hinzu (z. B. Ihren Studiengang oder ein Emoji als Text) und beobachten Sie den Unterschied.
- Bonus: Machen Sie absichtlich einen kleinen Tippfehler und beheben Sie ihn wieder – Fehlermeldungen sind hier Teil des Lernens.
```

Wie der Live-Code funktioniert und warum man auf einer Website überhaupt Python-Code ausführen kann, ist technisch relativ komplex, auch wenn es auf den ersten Blick nicht so aussieht. Im Hintergrund laufen viele Prozesse ab. Einen Teil davon werden wir in dieser Vorlesung kennenlernen.

Wichtig ist vor allem, was Sie auf der Website konkret tun können: Sie können Python-Programme ausführen und sie direkt verändern.

**Installieren von Paketen**

Zusätzlich können Sie Python-Pakete installieren und nutzen. Pakete stellen Ihnen zusätzliche Funktionalitäten bereit, sodass Sie viele Dinge nicht komplett selbst programmieren müssen. Ein Beispiel ist `pyfiglet`. Damit können Sie Schriftbanner erzeugen. Wenn Sie die folgende Code-Zelle ausführen, wird das Paket installiert. Anschließend „importieren“ wir es und nutzen dann die Banner-Funktion.


```{code-cell} python3
:tags: [skip-execution]

!pip install pyfiglet
import pyfiglet

myname = "Christina"
print(pyfiglet.figlet_format(f"Hello {myname}"))
```

```{admonition} Mini-Aufgabe
:label: hellobanner

- Ändern Sie den Text im Banner (z. B. „Hello“ → „Willkommen“).
- Bonus: Probieren Sie einen Namen mit Umlaut (z. B. „Jörg“) und schauen Sie, wie die Ausgabe aussieht.
```

Wichtig: Sie müssen den Programmcode in diesem Beispiel und in den folgenden Beispielen noch nicht verstehen. Es geht hier nur darum zu zeigen, was auf der Website möglich ist. Einige dieser Dinge werden wir im Laufe der Vorlesung aufgreifen. Dazu gehört zum Beispiel, wie man Animationen programmiert und direkt auf der Website ausführt.

**Programmierte Animationen**

Sie können im Live-Code Animationen erstellen und ausführen.

```{code-cell} python3
:tags: [skip-execution]

# -----------------------------
# Einstellungen
# -----------------------------

myname = "Christina"         # Dein Name
fontsize = 28                # Schriftgröße
letter_spacing = 0.9         # Abstand zwischen Buchstaben (kleiner = enger, größer = weiter)
frame_interval = 60          # Geschwindigkeit der Animation (größer = langsamer)
random_colors = True         # True = zufällige Farben, False = schwarz

# -----------------------------
# Programm
# -----------------------------

%matplotlib inline
import matplotlib as mpl
mpl.rcParams["animation.html"] = "jshtml"
mpl.rcParams["animation.embed_limit"] = 50

import matplotlib.pyplot as plt
from matplotlib.animation import FuncAnimation
import random

start_height = 1.4            # Startposition der Buchstaben (größer = weiter oben)
fly_frames = 10               # Dauer des Einfliegens (größer = langsamer)
target_height = 0.5           # Zielposition (vertikale Mitte)
message = f"Hello {myname}"   # Schriftzug

fig, ax = plt.subplots(figsize=(8, 2))
ax.set_xlim(0, 1)
ax.set_ylim(0, 1)
ax.axis("off")

font = dict(fontfamily="DejaVu Sans Mono", fontsize=fontsize)

# Horizontale Positionen automatisch berechnen
dx = letter_spacing / max(1, len(message) - 1)
x0 = 0.5 - dx * (len(message) - 1) / 2
xs = [x0 + i * dx for i in range(len(message))]

# Textobjekte erzeugen
letters = []
for i, ch in enumerate(message):
    color = (
        random.random(), random.random(), random.random()
    ) if random_colors else "black"

    txt = ax.text(
        xs[i],
        start_height,
        ch,
        ha="center",
        va="center",
        color=color,
        **font
    )
    letters.append(txt)

# Animationsfunktion
def update(frame):
    for i, txt in enumerate(letters):
        start = i
        end = i + fly_frames

        if frame < start:
            y = start_height
        elif frame >= end:
            y = target_height
        else:
            y = start_height + (target_height - start_height) * (frame - start) / fly_frames

        txt.set_position((xs[i], y))
    return letters

ani = FuncAnimation(
    fig,
    update,
    frames=len(message) + fly_frames + 1,
    interval=frame_interval,
    blit=True
)

plt.close(fig)
ani
```

```{admonition} Mini-Aufgabe
:class: hint

- Ändern Sie im Block „Einstellungen“ `fontsize` und `frame_interval` und lassen Sie die Zelle erneut laufen.
- Schalten Sie `random_colors` auf `False` (oder wieder auf `True`) und beobachten Sie den Effekt.
```
**Komplexere Animationen**

Oder, falls Ihnen das immer noch zu langweilig ist: Lassen Sie einen Roboter den Ausweg aus einem Labyrinth finden.

Die folgende Welt enthält unseren Roboter (blau), das Ziel (lila), begehbare Zellen (hellgrau) und unbegehbare Hindernisse (dunkelgrau). Wenn Sie auf „Run“ klicken, werden Roboter und Ziel zufällig in einer Umgebung platziert – einem Raster aus 5×7 Kacheln.

```{code-cell} python3
:tags: [skip-execution]

%matplotlib inline
import matplotlib as mpl
mpl.rcParams["animation.html"] = "jshtml"
mpl.rcParams["animation.embed_limit"] = 50


import roboworld as rw

world = rw.complex_maze(nrows=5, ncols=7)
world.show()
```

```{admonition} Mini-Aufgabe
:label: change

Die Position der Hindernisse, des Roboters und des Ziels wird per Zufall bestimmt. Testen Sie das, indem Sie die Zelle erneut mit „Run“ ausführen.
```
Jetzt möchten wir beobachten, wie der Roboter (irgendwann) ans Ziel kommt.

In den folgenden Code-Zellen wird festgelegt, dass der Roboter nur **nach vorne laufen** und sich **um 90° nach links drehen** kann. Wie oft er sich vor dem nächsten Schritt nach links dreht, entscheidet der Zufall:
- **0× links**: geradeaus weiter
- **1× links**: nach links
- **2× links**: umdrehen
- **3× links**: nach rechts (dreimal links ist einmal rechts)

Führen Sie die folgende Code-Zelle aus, um den Zufallslauf (*random walk*) des Roboters zu beobachten.

```{code-cell} python3
:tags: [skip-execution]

import random as rnd

%matplotlib inline
import matplotlib as mpl
mpl.rcParams["animation.html"] = "jshtml"
mpl.rcParams["animation.embed_limit"] = 50


def random_move(robo):
    turns = rnd.choice([0,1,2,3]) # zufällig 0 ... 3 mal nach links drehen
    for _ in range(turns):
        robo.turn_left() # so oft nach links drehen wie oben gewählt
    if not robo.is_wall_in_front():
        robo.move()


robo = world.get_robo()
robo.disable_print()
while not robo.is_at_goal():
    random_move(robo)

rw.animate(world)
```

```{admonition} Mini-Aufgabe
:label: nrows

- Ändern Sie `nrows` und `ncols` und erzeugen Sie eine kleinere Welt (z. B. 4×6).
- Hinweis: Die Code-Zellen bauen aufeinander auf. Die Animation nutzt die zuvor erzeugte Welt. Gehen Sie daher so vor:
  - Führen Sie zuerst die **Welt-Zelle** (oben, `complex_maze(...)`) mit „Run“ aus.
  - Starten Sie danach die **Animations-Zelle** (hier) mit „Run“.
```