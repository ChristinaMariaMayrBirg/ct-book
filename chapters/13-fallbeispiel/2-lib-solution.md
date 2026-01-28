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

# Lösung mit Library

Wir sehen uns an, wie man mit "Einkaufsteilen" (Bibliotheken) sehr schnell Programme erstellen kann. Eine wichtige Regel in der Softwareentwicklung ist: "Do not reinvent the wheel!" Das heißt: Nutzen Sie Einkaufsteile, die gut getestet sind und gewartet werden! Eine Sammlung von Einkaufsteilen wird in der Softwareentwicklung als **Library** bezeichnet. Konkret sehen wir uns an, wie Julia das Fallbeispiel mithilfe einer Library lösen kann.


```{admonition} Hinweis
:class: remark

Sie führen den Code gerade auf einem Server aus. Deshalb können Sie **nicht** einfach Dateien von Ihrem Rechner hochladen oder von Ihrem Rechner-Pfad einlesen. Die Messdaten-Datei ist bereits auf dem Server für Sie abgelegt. 
```

Bitte führen Sie den folgendenen Code nochmals aus, um in Ihrem Setup den Pfad zur Datei zu identifizieren. Verwenden Sie die Variable `csv_file_path` um auf die Datei zuzugreifen:


```{code-cell} python3
csv_file_path = "https://raw.githubusercontent.com/fk03ingenieursinformatik/ingenieurinformatik-buch-deploy/refs/heads/master/data/air_quality_no2.csv"

print(f"Die Datei wird bezogen über: {csv_file_path}")
```

Als erstes liest Julia die Messdaten aus der CSV-Datei ein und werfen einen Blick auf die Tabelle.


```{code-cell} python3

import pandas as pd

df = pd.read_csv(
    csv_file_path,
    parse_dates=["datetime"]
)

df = df.rename(
    columns={
        "station_antwerp": "Antwerp",
        "station_paris": "Paris",
        "station_london": "London",
    }
)

df.head()
```

Als Nächstes bereiten wir die Daten so vor, dass Zeitpunkte bequem als Index genutzt werden können.

```{code-cell} python3

df = df.set_index("datetime")
df.head()
```

Nun lassen wir uns zentrale Kennwerte (z. B. Mittelwert, Standardabweichung und Perzentile) automatisch berechnen.

```{code-cell} python3

stats = df.describe().T
stats
```

Zum Abschluss visualisieren wir die Verteilung der Messwerte als Histogramme.

```{code-cell} python3
import matplotlib.pyplot as plt

axs = df.hist()
for ax in axs.ravel():
    ax.set_xlabel("NO₂-Konzentration (µg/m³)")
    ax.set_ylabel("Häufigkeit")

plt.tight_layout(h_pad=2.0, w_pad=1.0)
plt.show()
```

Und wir sind fertig!