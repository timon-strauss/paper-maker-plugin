# Paper-Maker Plugin

> Entwickelt von Timon Strauß und Finn Roth — zwei duale Studenten bei SAP.

Paper-Maker ist ein Claude Code Plugin, das duale Studenten beim Schreiben wissenschaftlicher Arbeiten unterstützt. Es begleitet den gesamten Prozess von der ersten Idee bis zur fertigen Arbeit.

## Was das Plugin macht

Das Plugin unterstützt in drei Phasen:

- **Planung** — Themenfindung, Gliederung und Quellenrecherche
- **Schreiben** — Iteratives, kapitelweises Formulieren der Arbeit im Typst-Format inkl. korrekter Zitierweise
- **Überprüfung** — Bewertung und Optimierung der fertigen Arbeit

Quellen werden über NotebookLM verwaltet. Das Plugin kennt die Konventionen des DHBW-Typst-Templates und erzeugt direkt validen Typst-Code mit korrekten Zitaten und Belegen.

## Voraussetzungen

### 1. Claude Code

Claude Code CLI oder Desktop App: [claude.ai/code](https://claude.ai/code)

### 2. Typst

Typst muss lokal installiert sein.

```bash
# macOS
brew install typst
```

Weitere Installationsmethoden: [typst.app](https://typst.app)

### 3. clean-dhbw Typst-Template

Das Plugin ist auf das `clean-dhbw` Template ausgelegt.

Paket: [typst.app/universe/package/clean-dhbw](https://typst.app/universe/package/clean-dhbw/)

Das Template wird über den Typst-Paketmanager eingebunden — keine manuelle Installation nötig, solange Typst installiert ist.

### 4. NotebookLM MCP

Das Plugin nutzt NotebookLM zur Quellenverwaltung. Der MCP-Server muss installiert und konfiguriert sein.

Repository: [github.com/jacob-bd/notebooklm-mcp-cli](https://github.com/jacob-bd/notebooklm-mcp-cli)

Installation und Konfiguration sind in der dortigen README beschrieben. Nach der Einrichtung muss der MCP-Server in Claude Code unter dem Namen `notebooklm-mcp` registriert sein.

## Installation

### Schritt 1: Marketplace hinzufügen

```bash
/plugins marketplace add https://github.com/timon-strauss/paper-maker-plugin.git
```

### Schritt 2: Plugin installieren

> ⚠️ **Wichtig: Plugin im `local` oder `project` Scope installieren**
>
> Das Plugin lädt bei jeder Anfrage seinen gesamten Kontext (Rollen, Zitierregeln, Konventionen) ins Kontextfenster. Wird es im `global` Scope installiert, belastet dieser Kontext **jede** Claude Code Session — auch völlig unrelated Projekte. Das verschwendet Tokens und verlangsamt Claude spürbar.
>
> Immer mit `--scope local` oder `--scope project` installieren.

```bash
# Im Projektverzeichnis der wissenschaftlichen Arbeit ausführen:
/plugins install paper-maker --scope local
```

Das Plugin ist danach nur in diesem Projekt aktiv.

## Verwendung

Nach der Installation steht Paper-Maker automatisch in jeder neuen Session in diesem Verzeichnis zur Verfügung. Einfach loslegen:

- *"Hilf mir ein Thema zu finden"* → startet die Themenfindung
- *"Erstelle eine Gliederung"* → leitet durch den Gliederungsprozess
- *"Schreibe Kapitel 2"* → formuliert das Kapitel im Typst-Format
- *"Überprüfe meine Arbeit"* → bewertet und optimiert den Text
