# Features

## Meta

Dieses Dokument definiert, **was das Produkt tun soll**.

Es enthält:
- Feature-Definitionen (`featXX`)
- gewünschtes Verhalten und Akzeptanzkriterien
- Produktentscheidungen
- Releases (`relXX`)

Dieses Dokument ist die **Quelle der Wahrheit für gewünschtes Verhalten**.

---

## Verwendung

### Für Menschen

Nutze dieses Dokument, um:
- neue Features vor der Implementierung zu definieren
- Verhalten während der Entwicklung zu klären
- Entscheidungen und Constraints festzuhalten
- ein gemeinsames Produktverständnis sicherzustellen

Hier wird gedacht: **Was soll das Produkt tun und warum?**

---

### Für KI

- Behandle dieses Dokument als **Quelle der Wahrheit für erwartetes Verhalten**.
- Erfinde kein Verhalten, das hier nicht definiert ist.
- Bei Unklarheit → **keine Annahme**, sondern Klärung als `qXX` in `04-tasks.md`.
- Implementierung und Doku müssen mit diesem Dokument konsistent sein.

---

## Was gehört hierher

- Feature-Definitionen (`featXX`)
- Ziele und Zweck
- erwartetes Verhalten inklusive Edge Cases
- **Akzeptanzkriterien** (Given/When/Then)
- Non-Goals (explizite Ausschlüsse)
- Design-Entscheidungen
- Releases (`relXX`) als Bündel von Features

## Was gehört NICHT hierher

- Tasks → `04-tasks.md`
- Implementierungsdetails → `03-dev-doc.md`
- Bugs / Test-Ergebnisse → `05-quality.md`
- Bedienungsanleitungen → `02-user-doc.md`
- Architektur-Entscheidungen → `00-master.md` §10 (ADR)

---

## Produkt-Übersicht

### Zweck
Beschreibt das übergreifende Ziel des Systems.

### Kernkonzepte
Die zentralen Bausteine.

### Hauptfunktionen
High-Level-Übersicht und ihre Beziehungen zueinander.

### Constraints
Technische, geschäftliche oder konzeptionelle Grenzen.

---

## Features

---

### featXX [Feature-Name]

**Ziel**
Warum existiert dieses Feature? Welches Problem löst es?

---

**Verhalten**
Was genau soll passieren?

- Hauptfluss beschreiben
- Edge Cases einschließen
- erwartete System-Reaktionen definieren

---

**Akzeptanzkriterien**

Format: Given / When / Then. Jedes Kriterium hat eine ID `featXX.ACyy` und wird in `05-quality.md` von `testXX` referenziert.

```
- featXX.AC01
  Given:  <Ausgangszustand>
  When:   <Aktion>
  Then:   <erwartetes Ergebnis>

- featXX.AC02
  Given:  ...
  When:   ...
  Then:   ...
```

Faustregel: Ein Akzeptanzkriterium ist erfüllt, wenn ein Außenstehender mit der Beschreibung allein verifizieren kann, ob das System es erfüllt.

---

**Non-Goals**

- explizit ausgeschlossen
- verhindert Scope Creep

---

**Entscheidungen**

Wichtige produktbezogene Design-Entscheidungen:
- gewählter Ansatz und Begründung
- verworfene Alternativen (optional)

(Architektur-Entscheidungen → ADR im Master-Dokument.)

---

**Offene Fragen** (optional)

Nur eintragen, wenn Klärung nötig ist. Verweis auf `qXX` in `04-tasks.md`.

---

## Regeln

- Jedes Feature hat eine eindeutige ID (`featXX`).
- Beschreibungen präzise und unzweideutig halten.
- Keine Implementierungsdetails.
- Bei Verhaltensänderung dieses Dokument aktualisieren — sonst ist das Feature nicht „done".

---

## Grundprinzip

> Dieses Dokument definiert, **was passieren soll** — nicht **wie es implementiert ist**.

---

## 📦 Releases

Releases bündeln eine Menge fertiger Features zu einem versionierten Stand.

### Konvention

- ID-Format: `relXX` (oder semantisch `R1.2`, `R1.3`, …)
- Ein Release ist erst freigegeben, wenn **alle enthaltenen Features den Done-Kriterien aus `00-master.md` §6** entsprechen.
- Release-Freigabe ist eine Mensch-only-Befugnis (PO).
- Nach Freigabe: Tag im Repo (`vX.Y`), Eintrag im jeweiligen `Playbooks/`-Dokument für Release-Mechanik.

### Release-Vorlage

```
### relXX RX.Y

- **Datum:** YYYY-MM-DD
- **Status:** geplant | in Arbeit | freigegeben
- **Enthaltene Features:** featAA, featBB, featCC
- **Bekannte Einschränkungen:** offene bugXX (Severity ≤ S3, dokumentiert in 05-quality.md)
- **Migrations-Hinweis:** falls Schema-/Konfig-Änderung
- **Release-Notes:** kurzer Klartext für Anwender (verlinkt nach 02-user-doc.md)
```

### Aktive Releases

(noch keine — sobald das erste konkrete Projekt darauf läuft, wandert es hierher.)

---
