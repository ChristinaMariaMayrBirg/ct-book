# Eigenentwicklung

Nachdem Julia die Programmieraufgabe gelöst hat, stellt sie entsetzt fest: Sie hat eine wichtige Firmenvorgabe übersehen. Für neue externe Bibliotheken braucht es vorab eine Freigabe (Compliance-Prozess). Zwar ist `pandas` unter der BSD-3-Clause-Lizenz grundsätzlich auch in kommerziellen Produkten nutzbar, aber die Firma fordert in diesem Fall zusätzliche Schritte (z. B. Third-Party-Notices aktualisieren, Abhängigkeiten dokumentieren/SBOM pflegen, Security-Check der Lieferkette). Das Team will für dieses Projekt jedoch **keine neuen Abhängigkeiten** aufnehmen – aus Zeitgründen, wegen interner Regeln oder weil das Produkt „so schlank wie möglich“ bleiben soll. Julia muss also umplanen: statt „Buy“ (Bibliothek nutzen) bleibt hier nur „Build“ (selbst entwickeln).

Das bedeutet aber auch: Wenn Julia selbst Funktionalität implementiert, muss sie auch dafür sorgen, dass sie korrekt ist. Tests sind damit kein „Extra“, sondern Teil der Eigenentwicklung.

Im folgenden sehen wir uns an wie Julia vorgeht.