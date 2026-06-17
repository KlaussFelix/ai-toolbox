---
name: git-workflow
description: 'Geführter Git-Workflow für Feature-Entwicklung. Verwenden wenn: neuer Branch benötigt wird, Code-Änderungen commitet werden sollen, Branch-Naming-Convention geprüft werden soll, Merge-Approval eingeholt werden soll. Deckt ab: Branch erstellen, feature/fix/chore/docs/refactor Präfixe, Commit-Bestätigung einholen, Merge-Schutz.'
argument-hint: 'Beschreibe die Aufgabe, z.B. "neues Feature: Login-Seite"'
---

# Git Workflow und Branch-Management

## Wann verwenden
- Bei jeder neuen Aufgabe, die Code-Änderungen erfordert
- Wenn ein neuer Feature-Branch erstellt werden soll
- Wenn Änderungen commitet werden sollen (Bestätigung erforderlich)
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



## Schritt 3 — Commit-Bestätigung einholen

Nach Abschluss der Code-Änderungen:

1. **NICHT** automatisch commiten
2. Den Nutzer mit dem `vscode_askQuestions`-Tool fragen:
   > „Ich habe die Änderungen auf dem Branch `[branch-name]` abgeschlossen. Möchtest du, dass ich die Änderungen committe?"
3. Nur bei **ausdrücklicher Zustimmung** den Commit durchführen
4. Commit-Message nach Conventional Commits formulieren (z. B. `feat: add login page`)



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
              Code-Änderungen abgeschlossen?
                        │
                        ▼
              Nutzer um Commit-Erlaubnis fragen (vscode_askQuestions)
                        │
                        ▼
              Merge gewünscht? → Explizites "ok" abwarten
```
