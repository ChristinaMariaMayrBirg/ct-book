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

# Parsing

Julia startet im „Build“-Pfad ganz unten: Sie liest die CSV-Daten selbst ein und legt sie in einer Datenstruktur ab, die sie später leicht testen und weiterverarbeiten kann.


Beispieldaten (CSV-Ausschnitt):

```text
datetime,station_antwerp,station_paris,station_london
2019-05-07 02:00:00,,,23.0
2019-05-07 03:00:00,50.5,25.0,19.0
2019-05-07 04:00:00,45.0,27.7,19.0
2019-05-07 05:00:00,,50.4,16.0
...
```

Ziel-Datenstruktur: Für jede Station speichert sie die Zeitpunkte und die zugehörigen NO₂-Werte. Fehlende Messwerte (leere Felder) lässt sie weg. Das ist eine **Designentscheidung**: Genauso gut hätte sie `NaN`-Werte oder Platzhalter (z. B. leere Strings) speichern können – vgl. die Tabelle im vorherigen Abschnitt; dort waren fehlende Werte als leere Felder dargestellt.

```{code-cell} python3

def parse_air_quality_csv_v2(csv_text):
    """
    Sehr einfacher CSV-Parser.

    Annahmen (für unser Lehrbeispiel):
    - Trennzeichen ist ein Komma.
    - Es gibt keine Anführungszeichen und keine Kommata innerhalb von Feldern.
    - Erste Spalte heißt 'datetime' und bleibt als String (wir parsen sie hier NICHT).

    Rückgabe:
      {
        "station_antwerp": {"time": [...], "no2": [...]},
        "station_paris":   {"time": [...], "no2": [...]},
        ...
      }

    Leere Messwerte (z. B. ,,) werden ignoriert.
    """
    lines = [ln.strip() for ln in csv_text.strip().splitlines() if ln.strip()]
    if not lines:
        raise ValueError("CSV ist leer.")

    header = [h.strip() for h in lines[0].split(",")]
    if not header or header[0] != "datetime":
        raise ValueError("Erste Spalte muss 'datetime' heißen.")

    stations = header[1:]
    result = {s: {"time": [], "no2": []} for s in stations}

    for line in lines[1:]:
        parts = [p.strip() for p in line.split(",")]
        # falls am Zeilenende Werte fehlen: mit leeren Strings auffüllen
        if len(parts) < len(header):
            parts = parts + [""] * (len(header) - len(parts))

        t = parts[0]
        for idx, station in enumerate(stations, start=1):
            value = parts[idx] if idx < len(parts) else ""
            if value == "":
                continue
            result[station]["time"].append(t)
            result[station]["no2"].append(float(value))

    return result
```

Mini-Demo (optional): einmal parsen und prüfen, welche Stationen gefunden wurden.

```{code-cell} python3
:tags: [skip-execution]

sample = """\
datetime,station_antwerp,station_paris,station_london
2019-05-07 02:00:00,,,23.0
2019-05-07 03:00:00,50.5,25.0,19.0
2019-05-07 04:00:00,45.0,27.7,19.0
2019-05-07 05:00:00,,50.4,16.0
"""

data = parse_air_quality_csv_v2(sample)
list(data.keys())
```

## Testing

Julia sichert das Verhalten mit ein paar Unit-Tests ab. Da sie- wie wir hier - Notebooks nutzt, greift sie dafür auf `ipytest` zurück (siehe auch das Test-Kapitel).

```{code-cell} python3
import ipytest
ipytest.autoconfig()
ipytest.clean()

def _sample_csv_comma():
    return """\
datetime,station_antwerp,station_paris,station_london
2019-05-07 02:00:00,,,23.0
2019-05-07 03:00:00,50.5,25.0,19.0
2019-05-07 04:00:00,45.0,27.7,19.0
2019-05-07 05:00:00,,50.4,16.0
"""


def test_parse_returns_all_stations():
    data = parse_air_quality_csv_v2(_sample_csv_comma())
    assert set(data.keys()) == {"station_antwerp", "station_paris", "station_london"}


def test_parse_ignores_missing_values():
    data = parse_air_quality_csv_v2(_sample_csv_comma())
    # In der ersten Zeile (02:00) hat nur London einen Wert.
    assert data["station_antwerp"]["time"][0] != "2019-05-07 02:00:00"
    assert data["station_paris"]["time"][0] != "2019-05-07 02:00:00"
    assert data["station_london"]["time"][0] == "2019-05-07 02:00:00"


def test_parse_converts_values_to_float():
    data = parse_air_quality_csv_v2(_sample_csv_comma())
    assert isinstance(data["station_london"]["no2"][0], float)

ipytest.run()
```

Auf einem Laufwerk entdeckt Julia weitere Messdateien. Dort sind die Werte allerdings nicht durch `,`, sondern durch `;` getrennt.

Sie schreibt einen zusätzlichen Test, um zu prüfen, wie **generisch** ihr Code ist – also wie viele ähnliche Eingabeformate er abdecken kann.

Wie erwartet ist der Code noch wenig generisch: Der Test ist **rot** (Fail), weil der Parser (noch) nicht mit `;` umgehen kann.

```{code-cell} python3
def _sample_csv_semicolon():
    return """\
datetime;station_antwerp;station_paris;station_london
2019-05-07 02:00:00;;;23.0
2019-05-07 03:00:00;50.5;25.0;19.0
"""


def test_parse_with_semicolon_delimiter_should_work():
    # Erwartung (aus Nutzersicht): Semikolon funktioniert genauso.
    # Realität: unser Parser ist (noch) auf Komma fest verdrahtet -> der Test scheitert.
    data = parse_air_quality_csv_v2(_sample_csv_semicolon())
    assert "station_london" in data

ipytest.run()
```

## Error handling

Wie soll Julia mit dieser Erkenntnis umgehen, dass das Parsing nicht mehr funktioniert sobald das Trennzeichen anders ist? 

Sie hat zwei Möglichkeiten:

- Entweder macht sie ihren Code generischer, d. h. sie erkennt und verarbeitet mehrere Trennzeichen.
- Oder sie weist den Nutzer darauf hin, dass die Eingabe nicht dem erwarteten Format entspricht.

Julia hat nicht mehr viel Zeit. Variante 1 ist für heute zu groß – also entscheidet sie sich für Variante 2.

Sie implementiert die Funktion erneut, bleibt aber bei Komma als einzig unterstütztem Trennzeichen. Dafür liefert sie bei „Semikolon-CSV“ eine klare, hilfreiche Fehlermeldung. Julia nennt diese Zwischenlösung `parse_air_quality_csv_v2_strict`.

```{code-cell} python3

def parse_air_quality_csv_v2_strict(csv_text):
    """
    Sehr einfacher CSV-Parser (Zwischenlösung).

    Annahmen:
    - Trennzeichen ist ein Komma `,`.
    - Keine Anführungszeichen, keine Kommata innerhalb von Feldern.
    - Erste Spalte heißt `datetime` (wir parsen sie hier NICHT).

    Fehlerbehandlung:
    - Wenn die Eingabe nach Semikolon-CSV aussieht, geben wir eine klare Fehlermeldung aus.
    """
    lines = [ln.strip() for ln in csv_text.strip().splitlines() if ln.strip()]
    if not lines:
        raise ValueError("CSV ist leer.")

    first_line = lines[0]
    if "," not in first_line and ";" in first_line:
        raise ValueError(
            "Unerwartetes Trennzeichen ';'. Dieser Parser erwartet Komma ',' als Trennzeichen."
        )

    header = [h.strip() for h in first_line.split(",")]
    if not header or header[0] != "datetime":
        raise ValueError(
            "Ungültiger Header: erste Spalte muss 'datetime' heißen (Komma ',' als Trennzeichen)."
        )

    stations = header[1:]
    result = {s: {"time": [], "no2": []} for s in stations}

    for line in lines[1:]:
        if "," not in line and ";" in line:
            raise ValueError(
                "Unerwartetes Trennzeichen ';' in den Datenzeilen. Dieser Parser erwartet Komma ','."
            )

        parts = [p.strip() for p in line.split(",")]
        if len(parts) > len(header):
            raise ValueError(
                f"Zu viele Spalten in Zeile: {line!r} (erwartet {len(header)}, gefunden {len(parts)})."
            )
        if len(parts) < len(header):
            parts = parts + [""] * (len(header) - len(parts))

        t = parts[0]
        for idx, station in enumerate(stations, start=1):
            value = parts[idx] if idx < len(parts) else ""
            if value == "":
                continue
            try:
                result[station]["time"].append(t)
                result[station]["no2"].append(float(value))
            except ValueError as e:
                raise ValueError(
                    f"Ungültiger Messwert {value!r} für {station!r} in Zeile: {line!r}."
                ) from e

    return result
```

Dann passt Julia die Tests an: Semikolon-Eingaben sollen **nicht** „irgendwie“ geparst werden, sondern mit einer klaren Fehlermeldung abbrechen.

```{code-cell} python3

ipytest.clean()

import pytest

def test_parse_still_works_with_comma_csv():
    data = parse_air_quality_csv_v2_strict(_sample_csv_comma())
    assert set(data.keys()) == {"station_antwerp", "station_paris", "station_london"}


def test_parse_raises_on_semicolon_delimiter():
    with pytest.raises(ValueError, match=r"Trennzeichen.*';'.*Komma"):
        parse_air_quality_csv_v2_strict(_sample_csv_semicolon())

ipytest.run()
```
Ganz zufrieden ist Julia noch nicht: Andere Trennzeichen (z. B. `|`) werden weiterhin nicht unterstützt. Deshalb dokumentiert sie die Einschränkung und erstellt ein internes Ticket für eine generische Lösung.

## Refactoring: kleine, testbare Funktionen

Das größere Problem ist aber: Aktuell steckt (fast) die gesamte Logik in einer einzigen Funktion. Zum Beispiel kann sie das Parsen einzelner Messwerte (String → `float`) nicht unabhängig vom gesamten CSV-Einlesen testen.

Sie entscheidet sich daher für ein Refactoring: Die **Funktionalität bleibt gleich**, aber der Code wird in kleine, klar abgegrenzte Funktionen zerlegt. So kann sie einzelne Schritte gezielt testen und der Code wird leichter zu warten.

Julia trennt die Verantwortlichkeiten:
- **Text → Zeilen** (leere Zeilen ignorieren)
- **Delimiter-Check** (schnell erkennen, ob `;` benutzt wurde)
- **Header parsen**
- **Messwert parsen** (isoliert testbar!)
- **Gesamtes CSV parsen** (setzt die Bausteine zusammen)

```{code-cell} python3

def _non_empty_lines(text):
    return [ln.strip() for ln in text.strip().splitlines() if ln.strip()]


def _ensure_comma_delimiter(lines):
    """
    Zwischenlösung: Wir unterstützen NUR Komma.
    Wenn es nach Semikolon aussieht, geben wir eine klare Fehlermeldung.
    """
    if not lines:
        raise ValueError("CSV ist leer.")

    first_line = lines[0]
    if "," not in first_line and ";" in first_line:
        raise ValueError(
            "Unerwartetes Trennzeichen ';'. Dieser Parser erwartet Komma ',' als Trennzeichen."
        )


def _parse_header(header_line):
    header = [h.strip() for h in header_line.split(",")]
    if not header or header[0] != "datetime":
        raise ValueError(
            "Ungültiger Header: erste Spalte muss 'datetime' heißen (Komma ',' als Trennzeichen)."
        )
    stations = header[1:]
    if not stations:
        raise ValueError("Header enthält keine Stationsspalten.")
    return header, stations


def _parse_no2_value(value, station, line):
    """
    Parsen eines einzelnen Messwerts.

    - Leere Felder geben wir als None zurück (d.h. Messwert fehlt).
    - Nicht-leere Felder müssen in float umwandelbar sein.
    """
    value = value.strip()
    if value == "":
        return None
    try:
        return float(value)
    except ValueError as e:
        raise ValueError(
            f"Ungültiger Messwert {value!r} für {station!r} in Zeile: {line!r}."
        ) from e


def parse_air_quality_csv_v3(csv_text):
    lines = _non_empty_lines(csv_text)
    _ensure_comma_delimiter(lines)

    header, stations = _parse_header(lines[0])
    result = {s: {"time": [], "no2": []} for s in stations}

    for line in lines[1:]:
        if "," not in line and ";" in line:
            raise ValueError(
                "Unerwartetes Trennzeichen ';' in den Datenzeilen. Dieser Parser erwartet Komma ','."
            )

        parts = [p.strip() for p in line.split(",")]
        if len(parts) > len(header):
            raise ValueError(
                f"Zu viele Spalten in Zeile: {line!r} (erwartet {len(header)}, gefunden {len(parts)})."
            )
        if len(parts) < len(header):
            parts = parts + [""] * (len(header) - len(parts))

        t = parts[0]
        for idx, station in enumerate(stations, start=1):
            parsed = _parse_no2_value(parts[idx], station, line)
            if parsed is None:
                continue
            result[station]["time"].append(t)
            result[station]["no2"].append(parsed)

    return result
```

Tests für den refaktorierten Parser:

```{code-cell} python3
ipytest.clean()

import pytest

def test_parse_v3_parses_comma_csv():
    data = parse_air_quality_csv_v3(_sample_csv_comma())
    assert set(data.keys()) == {"station_antwerp", "station_paris", "station_london"}
    assert data["station_london"]["time"][0] == "2019-05-07 02:00:00"


def test_parse_v3_raises_on_semicolon_delimiter_in_header():
    with pytest.raises(ValueError, match=r"Trennzeichen.*';'.*Komma"):
        parse_air_quality_csv_v3(_sample_csv_semicolon())


def test_parse_v3_raises_on_semicolon_delimiter_in_data_lines():
    bad = """\
datetime,station_london
2019-05-07 02:00:00;23.0
"""
    with pytest.raises(ValueError, match=r"Trennzeichen.*';'.*Komma"):
        parse_air_quality_csv_v3(bad)


def test_parse_v3_raises_on_too_many_columns():
    bad = """\
datetime,station_london
2019-05-07 02:00:00,23.0,EXTRA
"""
    with pytest.raises(ValueError, match=r"Zu viele Spalten"):
        parse_air_quality_csv_v3(bad)


def test_parse_v3_raises_on_invalid_number():
    bad = """\
datetime,station_london
2019-05-07 02:00:00,abc
"""
    with pytest.raises(ValueError, match=r"Ungültiger Messwert"):
        parse_air_quality_csv_v3(bad)


def test_parse_v3_raises_on_empty_csv():
    with pytest.raises(ValueError, match=r"CSV ist leer"):
        parse_air_quality_csv_v3("")

ipytest.run()
```

Jetzt kann Julia z. B. das Float-Parsing unabhängig testen (ohne komplettes CSV zu bauen):

```{code-cell} python3
ipytest.clean()

import pytest

def test_parse_no2_value_empty_is_none():
    assert _parse_no2_value("", "station_x", "dummy") is None


def test_parse_no2_value_parses_float():
    assert _parse_no2_value(" 23.0 ", "station_x", "dummy") == 23.0


def test_parse_no2_value_raises_on_invalid_number():
    with pytest.raises(ValueError, match=r"Ungültiger Messwert"):
        _parse_no2_value("abc", "station_x", "dummy")

ipytest.run()
```