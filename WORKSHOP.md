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

Die folgenden Befehle legen in deinem Benutzerordner einen Ordner `Workshop` an, laden das Projekt dort hinein und wechseln in den Projektordner:

```powershell
mkdir $HOME\Workshop
cd $HOME\Workshop
git clone https://github.com/codedevote/sqlite-utils.git
cd sqlite-utils
uv sync --locked
uv run pytest -q
```

Erwartetes Ergebnis der letzten Zeile: `1496 passed, 17 skipped, 32 warnings`. Die Warnungen darüber (`DeprecationWarning` zu `isolated_filesystem`) sind normal und kein Fehler deiner Einrichtung. Danach zeigt `uv run sqlite-utils --help` die Befehle des Werkzeugs.

**Wichtig: Alle Befehle laufen im Projektordner.** Ein neues PowerShell-Fenster startet aber in deinem Benutzerordner. Wechsle dann immer zuerst zurück:

```powershell
cd $HOME\Workshop\sqlite-utils
```

Du bist richtig, wenn die Zeile vor deiner Eingabe mit `\Workshop\sqlite-utils>` endet.

Hast du das Projekt schon woanders hin geklont, ist das auch in Ordnung. Wechsle dann in deinen Ordner `sqlite-utils`.

## 3. Claude Code starten

Im Projektordner:

```powershell
claude
```

Beim ersten Start mit dem Firmenkonto anmelden. Unten im Fenster muss `manual mode on` stehen – die Projekteinstellung in `.claude/settings.json` sorgt dafür, dass Claude Code vor jeder Änderung und jedem Befehl nachfragt.

Bitte noch **keine** `CLAUDE.md` anlegen und nichts committen: Beides ist Teil der Übungen.

## 4. Wenn etwas nicht klappt

**`uv`, `git` oder `claude` wird nicht gefunden** („… wurde nicht als Name eines Cmdlet … erkannt“): Ein neues PowerShell-Fenster öffnen. Die Installationen tragen sich erst für neue Fenster in den Suchpfad ein.

**`uv sync` meldet `No pyproject.toml found`:** Du bist nicht im Projektordner. Erst `cd $HOME\Workshop\sqlite-utils`.

**`uv sync` meldet einen Zertifikatsfehler** (etwa `invalid peer certificate: UnknownIssuer` oder eine andere Meldung mit „certificate“): Das Firmennetz prüft verschlüsselte Verbindungen mit einem eigenen Zertifikat. uv soll dann den Zertifikatsspeicher von Windows verwenden:

```powershell
$env:UV_SYSTEM_CERTS = "true"
uv sync --locked
```

Hilft das, die Einstellung dauerhaft setzen und danach ein neues Fenster öffnen:

```powershell
[Environment]::SetEnvironmentVariable("UV_SYSTEM_CERTS", "true", "User")
```

**Ein Download bricht ab oder hängt:** Wahrscheinlich sperrt das Firmennetz eine Adresse. uv lädt Python von `github.com` und Pakete von `pypi.org` und `files.pythonhosted.org`, Claude Code braucht `claude.ai` und `api.anthropic.com`. Bitte die IT, diese Adressen freizugeben, oder frag nach der Proxy-Adresse.

**`uv sync` meldet `Multiple top-level packages discovered`:** Du hast vor dem 15.10.2026 geklont. Im Projektordner `git pull` ausführen, dann `uv sync --locked` wiederholen.

**Die Anmeldung bei Claude Code klappt nicht:** Deinem Firmenkonto ist wahrscheinlich noch kein Platz zugewiesen. Das kann nur die Admin-Person eures Claude-Kontos freischalten.

**Statt `manual mode on` steht ein anderer Modus:** Firmenvorgaben gehen vor die Projekteinstellung. Für die Vorbereitung ist das kein Problem, bitte melde es trotzdem.

Wenn ein Schritt fehlschlägt, schick die Fehlermeldung vorab per Microsoft Teams an die Workshopleitung.
