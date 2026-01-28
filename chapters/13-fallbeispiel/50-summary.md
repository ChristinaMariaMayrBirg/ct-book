# Zusammenfassung

Abstraktionsgrad: praktische Auswirkungen

Im Kapitel zum Abstraktionsgrad ging es darum, **auf welchem Level** Sie programmieren (High-Level: *was*, Low-Level: *wie*). In der Praxis hat diese Entscheidung ein paar sehr konkrete Konsequenzen.

Generizität (Beispiel: Parsing)

Beim Parsing-Teil haben wir gesehen, wie **wenig generisch** eigener Quellcode oft am Anfang ist: Er löst genau den aktuellen Fall, aber ist (noch) nicht robust gegenüber Varianten (fehlende Werte, andere Trennzeichen, neue Spalten, kaputte Zeilen usw.). Das ist normal – bedeutet aber, dass Low-Level-Implementierungen häufig mehr Aufwand in Fehlerfälle und Erweiterbarkeit brauchen.

Performance (Beispiel: Sortieren)

Beim Sortieren der Listen haben wir gesehen, dass Built-in-Funktionalitäten wie `list.sort()` ein Vielfaches schneller sein können. Gründe dafür sind z. B.:

- Teile der Implementierung laufen in CPython auf C-Ebene (weniger Interpreter-Overhead).
- Es wird ein sehr guter (und gut optimierter) Algorithmus verwendet.

Testaufwand und Wartbarkeit

Wir haben gesehen, wie viele Zeilen Code Julia produziert hat – und wie viele Zeilen zusätzlicher Code notwendig sind, um diesen Code zu testen. Wenn Sie gut getestete Bibliotheken wie `pandas` verwenden, können Sie sich einen Teil dieses Testaufwands sparen (und profitieren zusätzlich von Wartung/Fehlerfixes durch die Community).

Make-or-buy: was beziehen, was selbst bauen?

Wenn Sie Software entwickeln, stehen Sie immer vor der Herausforderung:

- **Was kann ich beziehen (Library/Framework) und was muss ich selbst implementieren?**
- **Wenn es mehrere Implementierungen gibt:** Wie finden Sie heraus, welche in Ihrem Softwareprodukt am besten geeignet ist – z. B. bezüglich Laufzeit, Arbeitsspeicher, Robustheit und Wartbarkeit?

Exkurs: Sicherheit (CVE)

```{admonition} Hinweis: CVE
:class: remark

Common Vulnerabilities and Exposures (CVE) ist ein öffentliches Referenzsystem zur eindeutigen Identifikation bekannter Sicherheitslücken in Software und Hardware. Jede CVE erhält eine standardisierte Kennung (z. B. CVE-2024-12345), die eine konsistente Kommunikation über Schwachstellen zwischen Herstellern, Sicherheitstools und Organisationen ermöglicht. CVEs bilden die Grundlage für viele Vulnerability-Scanner, Patch-Management-Prozesse und Risikobewertungen. Die offizielle CVE-Datenbank wird von der MITRE Corporation gepflegt und ist unter [cve.org](https://www.cve.org) abrufbar.
```

