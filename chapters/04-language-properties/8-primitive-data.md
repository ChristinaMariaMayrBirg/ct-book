# Zahlen

```{admonition} Behauptung
:class: remark
In Python muss ich mich nicht darum kümmern, wie groß meine Zahlen sind: 10 oder 100000000000. Das macht keinen Unterschied.
```

Diese Aussage ist **in vielen Fällen richtig** – und sie erklärt, warum Python sich oft „komfortabel“ anfühlt.

Denn grundsätzlich gilt in der Informatik: Zahlen müssen als **Bits** gespeichert werden. Wenn die Bitbreite **fest** ist (z.B. 32‑Bit oder 64‑Bit), ist auch der **Wertebereich** fest – und es kann zu **Überlauf** kommen.

**Was bedeutet Überlauf?** Stellen Sie sich vor, Sie speichern eine Zahl mit nur **4 Bits**. Dann können Sie nur Werte von `0000` (0) bis `1111` (15) darstellen.
Wenn Sie bei `1111` (15) noch 1 addieren, passt das Ergebnis nicht mehr in 4 Bits. Bei vielen Systemen passiert dann ein **Wrap‑around**: Es „springt“ zurück auf `0000`.

```text
0000 (0)
0001 (1)
0010 (2)
0011 (3)
...
1110 (14)
1111 (15)

1111 (15) + 0001 (1) = 1 0000 (16)
                 ^ der linke Übertrag passt nicht mehr in 4 Bits → Ergebnis: 0000 
```

Python löst das für ganze Zahlen elegant: Eine Ganzzahl (`int`) kann (praktisch) beliebig groß werden, weil die Python‑Implementierung intern bei Bedarf mehr Speicher reserviert.

Warum das geht: Python nutzt **Arbitrary‑Precision Integer Arithmetic** (Ganzzahlen mit variabler Länge). Praktisch heißt das: Der Wert wird intern in „Ziffernblöcken“ gespeichert, und wenn die Zahl wächst, werden einfach mehr Blöcke verwendet.
Das ist sehr komfortabel, denn Sie müssen sich nicht um einen Überlauf kümmern. 

Wenn Sie die Bitbreite festlegen (z.B. `numpy.int32`)

Wenn Sie Speicherrepräsentation/Bitbreite bewusst vorgeben wollen, passiert das in Python typischerweise über spezialisierte Bibliotheken (z.B. `numpy`) oder über Schnittstellen zu C/C++.

Beispiel mit `numpy` (feste Bitbreite + Überlauf):

```{code-cell} python
import numpy as np

# feste Bitbreite: 32-bit signed integer
info = np.iinfo(np.int32)
print("int32 range:", info.min, "bis", info.max)

x = np.int32(info.max)
print("x:", x)
print("x+1:", x + np.int32(1))  # Überlauf / Wrap-around
print("x+2:", x + np.int32(2))

# Speicherbedarf ist dann ebenfalls fest pro Wert:
a = np.array([1, 2, 3], dtype=np.int32)
print("dtype:", a.dtype, "nbytes:", a.nbytes)
```

```{admonition} Achtung
:class: warning
Wenn Sie z.B. in `numpy` einen Datentyp wie `int32` vorgeben, arbeiten Sie mit einem **festen Wertebereich**. Ergebnisse außerhalb dieses Bereichs können zu **Überlauf** führen (z.B. Wrap‑around statt Fehlermeldung). Prüfen Sie deshalb Wertebereiche und Grenzfälle gezielt.
```

```{admonition} Klarstellung
:class: note
- `int` ist in Python (praktisch) beliebig groß (dynamischer Speicher), `float` hat typischerweise endliche Präzision.
- Wenn Sie feste Bitbreiten nutzen (z.B. `numpy.int32`), müssen Sie Wertebereich und Überlauf aktiv im Blick behalten.
```
