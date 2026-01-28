# Vorgehen


In {numref}`fig-se-flow-simple` sehen Sie einen vereinfachten, aber praxisnahen Software-Entwicklungsprozess.
Ausgehend von einer gegebenen Problemstellung wird zunächst geprüft, ob existierende Bibliotheken oder Frameworks das Problem vollständig abdecken (*Buy*).
Ist dies nicht der Fall, wird das Problem in Teilprobleme zerlegt. Für jedes Teilproblem wird erneut entschieden, ob eine Fremdlösung verwendet oder eine eigene Implementierung entwickelt werden muss (*Build*).

```{figure} ../../figs/13-fallbeispiel/se-flow-simple.png
---
width: 900px
name: fig-se-flow-simple
---
Vereinfachter Software-Entwicklungsprozess im Sinne eines *Build-vs.-Buy*-Entscheidungsablaufs.
```

Im Folgenden unterscheiden wir drei typische Ausprägungen dieses Vorgehens:

1. **Bezug einer Fremdlösung**

   Fremdsoftware: **100 %**, Eigenimplementierung: **0 %**  
   Die Problemstellung kann vollständig durch eine bestehende Bibliothek oder ein Framework gelöst werden. Der Entwicklungsaufwand beschränkt sich auf Auswahl, Einbindung und Konfiguration der Fremdsoftware. Eigene Implementierungen und zugehörige Tests sind in diesem Fall nicht erforderlich.

2. **Entwicklung einer Eigenlösung**

   Fremdsoftware: **0 %**, Eigenimplementierung: **100 %**  
   Für die Problemstellung existiert keine geeignete Fremdlösung. Die benötigte Funktionalität wird vollständig selbst implementiert. Damit geht zwingend ein entsprechender Testaufwand einher (z. B. Unit- oder Komponententests). Im hier betrachteten Anwendungsfall wird vereinfacht von einer einzelnen Funktionalität ausgegangen.

3. **Kombination aus Fremd- und Eigenlösung**

   Fremdsoftware: **partiell**, Eigenimplementierung: **partiell**  
   Dieser Fall tritt in der Praxis am häufigsten auf: Ein Teil der Funktionalität wird durch Fremdsoftware abgedeckt, während fehlende oder projektspezifische Aspekte selbst implementiert werden. Neben den Tests der eigenen Komponenten entsteht zusätzlicher Aufwand durch Integration und Integrationstests.

   
Im Folgenden spielen wir die Fälle (1) und (2) anhand des Praxisbeispiels durch. Das Praxisbeispiel ist entsprechend so gestaltet, dass beide Pfade exemplarisch durchlaufen werden können.

```{admonition} Hinweis: SBOM (Software Bill of Materials)
:class: remark

Sobald Sie im „Buy“-Pfad Bibliotheken oder Frameworks einbinden, wird Ihre Software zu einem **Produkt aus eigenen und fremden Bausteinen**. Eine *Software Bill of Materials* (SBOM) ist eine Art „Stückliste“ dieser Bausteine: Sie dokumentiert u. a. verwendete Komponenten (und häufig deren Versionen/Lizenzen). Das hilft insbesondere bei **Bewertung und Wartung**: Welche Abhängigkeiten stecken im Produkt? Welche Updates sind relevant? Welche Risiken oder Lizenzpflichten könnten entstehen? (vgl. {cite}`bsi:cra:2024`).
```