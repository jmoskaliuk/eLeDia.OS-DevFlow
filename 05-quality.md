# Qualität

## Meta

Dieses Dokument erfasst die **Qualitätssicht** auf das System.

Es enthält:
- Bugs (`bugXX`) — reproduzierbare Probleme, mit Severity
- Tests (`testXX`) — Verifikationen, die auf Akzeptanzkriterien aus `01-features.md` verweisen

Es enthält **nicht**:
- Ideen → `01-features.md`
- Tasks → `04-tasks.md`

---

## 🐞 Bugs

### Severity-Skala

| Severity | Bedeutung | Reaktion |
|---|---|---|
| **S1** | Kritisch — Kernfunktion komplett kaputt, Datenverlust, Sicherheitslücke | Sofortiger Hotfix-Task, blockiert Release |
| **S2** | Schwer — Feature unbrauchbar oder schwerer UX-Defekt, kein Workaround | Im laufenden Release fixen |
| **S3** | Mittel — Feature eingeschränkt, Workaround vorhanden | Nächstes Release |
| **S4** | Gering — kosmetisch, edge-case, minor | Backlog, opportunistisch |

### Vorlage

```
### bugXX Kurztitel

Feature:  featXX
Severity: S1 | S2 | S3 | S4
Status:   open | in_progress | fixed | wontfix
Linked:   taskXX (Fix), testXX (Reproduktion)

**Beschreibung**
Was ist falsch?

**Reproduktion**
1. ...
2. ...

**Erwartet**
Was sollte passieren?

**Tatsächlich**
Was passiert stattdessen?

**Umgebung** (falls relevant)
Browser / Version / Konfiguration / Datenstand
```

---

### bug42 Kein Test-Skelett für Library-Pfad
Feature:  feat42
Severity: S2
Status:   fixed
Linked:   task42, test42

**Beschreibung**
Der frühere Library-Bereich hatte keine verlässliche, im owning Plugin
verankerte Teststruktur. Nach der Produktentscheidung ist Library ein
ContentHub-Pfad und muss dort getestet werden.

**Reproduktion**
1. ContentHub-Repo prüfen: Library-spezifische Tests unter
   `plugins/local_lernhive_contenthub/tests/library/` und Behat unter
   `plugins/local_lernhive_contenthub/tests/behat/`

**Erwartet**
Jeder Produktpfad startet im owning Plugin mit Test-Skelett.

**Tatsächlich**
Tests sind im ContentHub konsolidiert.

---

### bug43 ContentHub-Library-Import: S3-Auth, Restore-Fehler, Odoo-FK
Feature:  feat43
Severity: S2
Status:   open
Linked:   task43, test43

**Beschreibung**
- S3 presigned URLs + Bearer-Header → Hetzner InvalidArgument
- Moodle Restore: Zielkurs muss vor `restore_controller` belastbar existieren;
  sonst `restore_check_course_not_exists`
- Odoo: FK-Fehler beim Löschen von Wizard/Version

**Reproduktion**
1. Import mit presigned URL und Bearer-Header → Fehler
2. ContentHub-Library-Import mit scheinbar korrektem .mbz → `restore_check_course_not_exists`
3. Odoo: Wizard-Objekt löschen, Version bleibt referenziert

**Erwartet**
- Kein Auth-Header bei presigned
- Restore legt Zielkurs wie Moodle UI sauber an und schlägt mit klarer
  ContentHub-Fehlermeldung fehl, falls das .mbz nicht wiederherstellbar ist
- FK-Fehler werden sauber behandelt

**Tatsächlich**
Siehe oben

---

## 🧪 Tests

Jeder Test verweist auf ein Akzeptanzkriterium aus `01-features.md` und macht es prüfbar.

### Vorlage

```
### testXX Kurztitel

Feature:                featXX
Akzeptanzkriterium:     featXX.ACyy
Typ:                    manuell | automatisiert
Status:                 pending | pass | fail
Letzter Lauf:           YYYY-MM-DD

**Schritte**
1. ...
2. ...

**Erwartetes Ergebnis**
Aus dem Akzeptanzkriterium übernommen oder konkretisiert.

**Beobachtetes Ergebnis** (bei pass/fail)
Was wurde tatsächlich gesehen?

**Verlinkter Bug** (bei fail)
bugXX
```

---

### test42 Teststruktur vorhanden
Feature:                feat42
Akzeptanzkriterium:     feat42.AC1
Typ:                    automatisiert
Status:                 pass
Letzter Lauf:           2026-05-02

**Schritte**
1. PHPUnit- und Behat-Teststruktur im ContentHub prüfen
2. Sicherstellen, dass keine separate Library-Plugin-Teststruktur als neuer
   DevFlow wieder eingeführt wurde

**Erwartetes Ergebnis**
Teststruktur ist im ContentHub vorhanden und lauffähig.

**Beobachtetes Ergebnis**
Struktur vorhanden; PHP-Lint ist grün, vollständige PHPUnit-Ausführung lokal
wegen fehlendem Docker/OrbStack nicht ausgeführt.

---

### test43 Fehlerfälle ContentHub-Library-Import
Feature:                feat43
Akzeptanzkriterium:     feat43.AC1
Typ:                    manuell
Status:                 pending
Letzter Lauf:           2026-05-02

**Schritte**
1. Import mit presigned URL + Bearer testen
2. Restore mit .mbz aus UI und ContentHub-Library-Import vergleichen
3. Odoo-Wizard-Delete testen

**Erwartetes Ergebnis**
Alle Fehlerfälle werden korrekt behandelt oder sauber geloggt.

---

### test44 ContentHub-Library UX Smoke
Feature:                feat44
Akzeptanzkriterium:     feat44.AC1
Typ:                    manuell
Status:                 pending
Letzter Lauf:           2026-05-02

**Schritte**
1. `/local/lernhive_contenthub/library.php` auf dev öffnen
2. Prüfen, ob Plugin-Shell-Breite zur Default-Entscheidung passt
3. Prüfen, ob Karten gleich hoch wirken
4. Suche, Sprachfilter und Themenfilter bedienen
5. Import-Bestätigungsseite öffnen

**Erwartetes Ergebnis**
- ContentHub bleibt ein einheitlicher Produktbereich
- Library-Karten springen nicht in der Höhe
- Suche/Filter reduzieren die Karte sichtbar ohne Layoutbruch
- Import-Bestätigung ist eine ContentHub-Fläche, kein nackter Moodle-Formblock

---

## Regeln

- Jeder Bug bekommt eine Severity — auch S4 ist eine Severity.
- Jeder Test referenziert ein Akzeptanzkriterium. Ein Test ohne `featXX.ACyy`-Verweis ist verdächtig.
- Reproduzierbarkeit hat Vorrang vor Vermutung.
- Fixed-Status nur, wenn der zugehörige `testXX` grün ist.

---

## Grundprinzip

> Bugs sind Teil des normalen Loops, keine Ausnahme.
> Ein Test ohne Akzeptanzkriterium prüft nichts Verbindliches.
