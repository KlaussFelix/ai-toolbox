---
name: git-workflow
description: 'Geführter Git-Workflow für Feature-Entwicklung. Verwenden wenn: neuer Branch benötigt wird, Code-Änderungen commitet werden sollen, Branch-Naming-Convention geprüft werden soll, Merge-Approval eingeholt werden soll. Deckt ab: Branch erstellen, feature/fix/chore/docs/refactor Präfixe, automatische Commits zu sinnvollen Zeitpunkten, Merge-Schutz mit Bestätigung.'
argument-hint: 'Beschreibe die Aufgabe, z.B. "neues Feature: Login-Seite"'
---

# Git Workflow und Branch-Management

## Wann verwenden
- Bei jeder neuen Aufgabe, die Code-Änderungen erfordert
- Wenn ein neuer Feature-Branch erstellt werden soll
- Wenn Änderungen commitet werden sollen (automatisch zu sinnvollen Zeitpunkten)
- Wenn ein Branch in `main` gemergt werden soll (Bestätigung erforderlich)



## Schritt 1 — Branch evaluieren und erstellen

Prüfe, ob die Aufgabe einen neuen Branch erfordert. Wähle das passende Präfix:

| Typ | Präfix | Beispiel |
|-----|--------|---------|
| Neue Funktion / Erweiterung | `feature/` | `feature/login-page` |
| Fehlerbehebung | `fix/` | `fix/null-pointer-crash` |
| Wartung, Abhängigkeiten | `chore/` | `chore/update-dependencies` |
| Dokumentation | `docs/` | `docs/api-reference` |
| Refactoring | `refactor/` | `refactor/extract-service-layer` |

**Regeln:**
- Immer Kleinbuchstaben
- Wörter mit Bindestrichen (`-`) trennen
- Branch **vor** jeder Code-Änderung vorschlagen

**Aktion:** Branch-Namen vorschlagen und dem Nutzer mitteilen, bevor Code angefasst wird.



## Schritt 2 — Aufgabe ausführen

- Alle Änderungen **ausschließlich** im Kontext des neu erstellten Branches durchführen
- Keine Änderungen auf `main` / `master` direkt vornehmen



## Schritt 3 — Automatisch commiten zu sinnvollen Zeitpunkten

Commits erfolgen **automatisch ohne Rückfrage**, sobald ein sinnvoller Zeitpunkt erreicht ist. Gute Zeitpunkte sind z. B.:

- Eine logisch abgeschlossene Teilaufgabe / Einheit ist fertig (eine Funktion, ein Modul, ein Bugfix)
- Tests / Build laufen grün, bevor die nächste Teilaufgabe beginnt
- Bevor ein größerer oder riskanter Umbau begonnen wird (sauberer Zwischenstand)
- Der Arbeitsstand ist konsistent und würde für sich genommen Sinn ergeben

**Regeln für automatische Commits:**

1. Nur auf dem dafür vorgesehenen Branch commiten — **niemals** direkt auf `main` / `master`
2. Commit-Message nach Conventional Commits formulieren (z. B. `feat: add login page`)
3. Pro Commit eine zusammenhängende, in sich abgeschlossene Änderung (keine riesigen Sammel-Commits)
4. Vor dem Commit kurz prüfen (`git status` / `git diff`), dass nur beabsichtigte Dateien enthalten sind
5. Keine kaputten Zwischenstände commiten, wenn vermeidbar (Code soll baubar/lauffähig sein)

**Hinweis:** Es ist **keine** Rückfrage vor dem Commit nötig. Die Bestätigungspflicht gilt ausschließlich für Merges (siehe Schritt 4).



## Schritt 4 — Merge-Schutz

- **NIEMALS** automatisch in `main` / `master` mergen
- Nach Abschluss der Arbeit den Nutzer informieren und explizit fragen:
   > „Die Arbeit auf Branch `[branch-name]` ist abgeschlossen. Soll ich einen Merge / Pull Request vorbereiten? Bitte bestätige mit 'ok'."
- Erst nach explizitem „ok" oder Bestätigung fortfahren



## Entscheidungsbaum

```
Aufgabe erhalten
    │
    ▼
Neuer Branch nötig?
    ├── Ja → Branch-Namen bestimmen (Präfix + Beschreibung)
    │         → Branch vorschlagen / erstellen
    │         → Aufgabe auf Branch umsetzen
    └── Nein → Auf bestehendem Branch weiterarbeiten
                        │
                        ▼
              Sinnvoller Commit-Zeitpunkt erreicht?
                        │
                        ▼
              Automatisch commiten (ohne Rückfrage, nur auf Branch)
                        │
                        ▼
              Merge gewünscht? → Explizites "ok" abwarten (Pflicht)
```
