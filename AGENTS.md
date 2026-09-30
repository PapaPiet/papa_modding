# AGENTS.md - papa_modding

Regeln für jeden KI-Agenten (Claude Code, Cursor, Codex, Windsurf, ...) in diesem Repo.
`CLAUDE.md` bindet diese Datei nur ein. Sprache: Deutsch, Code-Bezeichner: Englisch.

## 1. Zuerst das Second Brain
Piets Second Brain (MCP-Server `second-brain`) enthält die verbindlichen Regeln.
Zu Beginn jeder Sitzung:
1. `brain_context("papa_modding: <Aufgabe>")` - Kern (Profil, Prinzipien, Aktuelles). Hat Vorrang vor Annahmen.
2. `brain_rules()` - aktuelle globale Regel (`_system/Rules/GLOBAL.md`) mit Fassungsnummer. Befolgen,
   nicht in dieses Repo kopieren, immer frisch abrufen.
3. `brain_claim("papa_modding", "<woran>")` vor der Arbeit, `brain_release("papa_modding")` am Ende.
4. Nach der Arbeit: Changelog und Modulnotiz im Brain, `brain_pruefung(...)` für Piets Abnahme.
5. **Rollen:** Sagt Piet „Du bist jetzt FiveM Coder" (oder `/fivem`), sofort `brain_skill("fivem-coder")` laden und dessen Schritte ausführen
   (alle Papa-Modding-Repos holen, Regeln, `bridge.md`, `exports.MD`, `versions.json`). Weitere Rollen: GLOBAL.md, Abschnitt „Rollen".

## 2. Git-Ablauf (verbindlich, Piet 30.09.2026)
Auslieferungs-Branch dieses Repos: **`main`**. Piet pullt und mergt nie selbst.
1. Während der Arbeit immer auf einem eigenen Branch arbeiten (z. B. `claude/<thema>`, `cursor/<thema>`), nie direkt auf `main`.
2. **Nach jeder Aufgabe selbst mergen und pushen, ohne Rückfrage:**
   `git fetch origin` → `git checkout main` → `git pull --rebase origin main` →
   `git merge --no-ff <arbeits-branch>` → prüfen → `git push origin main`.
3. Erzwingt die Umgebung einen Pull Request, mergt der Agent ihn selbst. Kein PR bleibt offen liegen.
4. Selbst prüfen: `git fetch origin && git merge-base --is-ancestor HEAD origin/main`.
5. Geht der Merge nicht (Rechte, Konflikt mit fremder Logik): in der Abschlussantwort im Klartext sagen, warum, und welcher Branch offen ist.

## 3. Pflicht-Werkzeuge
- **Codegraph:** Vor jedem Lesen, Suchen oder Ändern von Code zuerst `codegraph_explore` aufrufen
  (`projectPath` = Repo-Wurzel). Grep und Datei-Lesen nur, wenn Codegraph nichts findet.
  Fehlt der Index: `codegraph init`. `.codegraph/` steht in `.gitignore`, nie committen.
- **Caveman:** Knappe Chat-Antworten (Plugin `caveman@caveman`, Stufe `full`). Keine Füllwörter, keine Einleitung.
  Commits, PR-Texte, Code-Kommentare und Doku in normaler Sprache. Agenten ohne Plugin halten den Stil von Hand ein.
- Nie das Zeichen „—" benutzen, stattdessen „-".

## 4. Projekt
- Öffentliches Repo mit `versions.json`: veröffentlichte Versionen aller Papa-Modding-Scripts.
- Maßgeblich für die Versionierung in den Script-Repos (siehe dort, Abschnitt „Versionierung bei jeder Änderung").
- Öffentlich: keine internen Adressen, Zugänge oder Brain-Inhalte hier ablegen.
