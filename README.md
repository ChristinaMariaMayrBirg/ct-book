# Ingenieurinformatik 1 - Computational Thinking

Dieses Repository enthält die Inhalte für eine interaktive Lern-Website, die auf Jupyter Book basiert. Studierende können sich selbstständig durch die Lehrinhalte arbeiten und **Python-Befehle direkt im Browser ausführen**.

## Website

Die Website wird automatisch über **GitLab LRZ Pages** bereitgestellt:

** [Zur Website](https://ingenieurinformatik-buch-fcbc5c.pages.gitlab.lrz.de/intro.html)**

Die Website basiert auf Jupyter Notebooks und ermöglicht es Studierenden, interaktiv mit den Lehrinhalten zu arbeiten und Python-Code direkt im Browser auszuführen.

## 📄 PDF-Version

Zusätzlich zur Website kann aus den Inhalten ein **PDF-Buch** generiert werden. Dies wird über die GitLab CI/CD Pipeline erstellt.

## 🤝 Beitragen

### Workflow

1. Repository klonen
2. Änderungen durchführen
3. Änderungen committen und pushen

### CI/CD Pipeline

Das Projekt nutzt eine **Continuous Integration Pipeline**, mit der sowohl die Website als auch das PDF-Buch gebaut werden können. Die Pipeline wird auf einem GitLab Runner ausgeführt, der von Christina Mayr auf dem HM Kubernetes Cluster eingerichtet wurde.

**Weitere Informationen:** [How-To: Get a local Docker Image into Kubernetes](https://collab.dvb.bayern/spaces/~ebke/pages/1494030620/How-To+Get+a+local+Docker+Image+into+Kubernetes)

**Wichtig:**
- Das **PDF-Buch** muss manuell getriggert werden (Job: `build_book_pdf`)
- Das **Update der Website** muss ebenfalls manuell getriggert werden (Job: `update_website`)
- Der Build der Website (`build_website_html`) läuft automatisch bei jedem Push

### Lokales Bauen

Um die Website oder das PDF lokal zu bauen, schauen Sie am besten in die CI-Konfiguration (`.gitlab-ci.yml`). Hier sind alle verwendeten Befehle enthalten.

**Voraussetzungen:**
- Docker muss installiert sein, um den Docker-Container lokal auszuführen
- Das verwendete Docker-Image: `gitlab.lrz.de:5005/fk03ingenieurinformatik/ingenieurinformatik-buch:latest`

**Beispiel für lokalen Build:**

```bash
# Zuerst ins geklonte Repository-Verzeichnis wechseln
cd /path/to/ingenieurinformatik-buch
# Docker-Container starten und in die Bash wechseln
# -v "$PWD":/home/jovyan/work mountet das aktuelle Verzeichnis in den Container
docker run --rm -it -v "$PWD":/home/jovyan/work -w /home/jovyan/work \
  gitlab.lrz.de:5005/fk03ingenieurinformatik/ingenieurinformatik-buch:latest \
  bash
```

Innerhalb des Containers können Sie dann die Befehle aus der CI-Konfiguration ausführen (`.gitlab-ci.yml`).

**HTML-Website bauen:**
```bash
jupyter-book build . --path-output _website_html
```

**PDF-Buch bauen:**
```bash
# Zuerst GIF-Dateien zu PNG konvertieren (falls nötig)
find figs -name "*.gif" -print0 | while IFS= read -r -d "" gif; do
  png="${gif%.gif}.png"
  if [ ! -f "$png" ]; then
    convert "${gif}[0]" "$png" && echo "generated: $png"
  fi
done

# PDF-Buch bauen
export LATEXMKOPTS='-interaction=nonstopmode'
jupyter-book build . --builder pdflatex --path-output _book_as_pdf
```



