# Workshop: Claude Code – Einrichtung

Dieser Fork von [simonw/sqlite-utils](https://github.com/simonw/sqlite-utils) ist das Übungsprojekt der Workshop-Reihe. Bitte richte ihn **vor dem ersten Termin** ein; die Schritte dauern etwa 10 Minuten.

## 1. Werkzeuge installieren (Windows, PowerShell)

1. **Git for Windows**: https://git-scm.com/downloads/win
2. **uv** (Python-Umgebung und Paketverwaltung; lädt Python bei Bedarf selbst):

   ```powershell
   powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
   ```

3. **Claude Code**:

   ```powershell
   irm https://claude.ai/install.ps1 | iex
   ```

Danach ein neues PowerShell-Fenster öffnen.

## 2. Projekt klonen und prüfen

```powershell
git clone https://github.com/codedevote/sqlite-utils.git
cd sqlite-utils
uv sync --locked
uv run pytest -q
```

Erwartetes Ergebnis der letzten Zeile: `1496 passed, 17 skipped, 32 warnings`. Die Warnungen darüber (`DeprecationWarning` zu `isolated_filesystem`) sind normal und kein Fehler deiner Einrichtung. Danach zeigt `uv run sqlite-utils --help` die Befehle des Werkzeugs.

## 3. Claude Code starten

```powershell
claude
```

Beim ersten Start mit dem Firmenkonto anmelden. Unten im Fenster muss `manual mode on` stehen – die Projekteinstellung in `.claude/settings.json` sorgt dafür, dass Claude Code vor jeder Änderung und jedem Befehl nachfragt.

Bitte noch **keine** `CLAUDE.md` anlegen und nichts committen: Beides ist Teil der Übungen.

Wenn ein Schritt fehlschlägt, schick die Fehlermeldung vorab in den Team-Kanal.
