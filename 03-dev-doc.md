# Entwickler-Dokumentation

## Meta

Dieses Dokument beschreibt, **wie das System tatsächlich implementiert ist**.

Es hat zwei Aufgaben:
1. die technische Struktur des Produkts dokumentieren
2. die Implementierung einzelner Features (`featXX`) festhalten

Dieses Dokument ist die **Quelle der Wahrheit für die Realität (Ist-Zustand)**.

---

## Verwendung

### Für Menschen

Nutze dieses Dokument, um:
- die interne Funktionsweise zu verstehen
- Architektur und Komponenten zu navigieren
- neue Entwickler:innen zu onboarden
- Debugging und Erweiterungen zu unterstützen

Denke: **Wie ist das System aufgebaut und wie funktioniert es wirklich?**

---

### Für KI

- Behandle dieses Dokument als **Quelle der Wahrheit für die Implementierung**.
- Erfinde kein Verhalten, das nicht implementiert ist.
- Beschreibe keine Wunsch-Implementierung — dafür ist `01-features.md` zuständig.
- Konsistenz prüfen mit:
  - `01-features.md` (gewünschtes Verhalten)
  - `02-user-doc.md` (sichtbares Verhalten)
- Bei Mismatch → Inkonsistenz flaggen, ggf. `qXX` anlegen.

---

## Was gehört hierher

- Architektur
- Komponenten und Module
- Datenfluss
- Komponenten-Interaktionen
- technische Constraints
- bekannte Einschränkungen

## Was gehört NICHT hierher

- Feature-Planung / Ideen → `01-features.md`
- Tasks / Work-Tracking → `04-tasks.md`
- Bugs / Test-Logs → `05-quality.md`
- Benutzererklärungen → `02-user-doc.md`
- Architektur-Entscheidungen → `00-master.md` §10 (ADR)

---

# 🧭 System-Übersicht

## Architektur

- Systemtyp (z. B. Client-only, Client-Server, Plugin in Host-System)
- Hauptebenen
- Kommunikationsmuster

---

## Kernkomponenten

- Komponente 1 → Zweck
- Komponente 2 → Zweck

---

## Datenfluss

- Eingabe → Verarbeitung → Ausgabe
- Komponenten-Interaktionen
- Event-Fluss

---

## Externe Abhängigkeiten

- Libraries (mit Versionen)
- APIs
- Services

---

## Technische Constraints

- Performance
- architektonische Grenzen
- bekannte Trade-offs

---

# 🧩 Feature-Implementierung

Pro Feature die tatsächliche Implementierung.

Alle Einträge:
- referenzieren ein `featXX`
- beschreiben den **Ist-Zustand**
- spekulieren nicht

---

## Feature-Vorlage

---

### [Feature-Name] (`featXX`)

**Überblick**
Kurze Beschreibung der Implementierung.

---

**Architektur**
Wie das Feature im System sitzt:
- beteiligte Komponenten
- Kommunikationsmuster

---

**Komponenten**

- Komponente A → Rolle
- Komponente B → Rolle

---

**Datenfluss**

- Trigger → Verarbeitung → Ergebnis

---

**State Management** (falls relevant)

- wo der Zustand liegt
- wie er sich ändert

---

**Abhängigkeiten**

- intern (andere Features, Module)
- extern (APIs, Libraries)

---

**Constraints / Einschränkungen**

- bekannte Probleme
- technische Grenzen
- Edge-Case-Verhalten

---

**Notizen** (optional)

- erwähnenswerte Implementierungsdetails
- ungewöhnliche Entscheidungen (Verweis auf `adrXX`, falls relevant)

---

# 📏 Regeln

- Beschreibe immer den **Ist-Zustand**, nicht den Soll-Zustand.
- Präzise und technisch.
- Feature-Beschreibungen nicht duplizieren — dafür ist `01-features.md` da.
- Aktualisieren, sobald sich die Implementierung ändert (sonst nicht „done").

---

# 🔑 Grundprinzip

> Dieses Dokument erklärt, **wie das System gebaut ist** — nicht **wie es sich verhalten soll**.
