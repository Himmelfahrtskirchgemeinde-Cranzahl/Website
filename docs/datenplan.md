# Datenplan

Dieses Dokument legt fest, **welche Seiten** die Website hat und **woher jeder Inhalt kommt**.
Es wird nichts eingebaut, was hier nicht freigegeben ist.

Legende Status: ⬜ offen · ✅ freigegeben · ❌ nicht benötigt

---

## 1. Seiten (aus Figma, Seite „🎨 Design")

| Seite | Figma-Frame | Status |
|---|---|---|
| Startseite | 🏠 Home V3 | ⬜ |
| Über uns | 📝 About | ⬜ |
| Veranstaltungen / Termine | ⭐️ Events | ⬜ |
| Gruppen (Übersicht) | 💼 Ministries | ⬜ |
| Gruppe (Detail) | 📋 Ministry Single | ⬜ |
| Spenden | 💵 Donate | ⬜ |
| Kontakt | 📩 Contact V1 | ⬜ |
| Blog / Aktuelles (Übersicht) | 🖋️ Blog | ⬜ |
| Blog-Beitrag | 📑 Blog Post | ⬜ |
| Kirchenvorstand | 🏷️ Kirchenvorstandsseite | ⬜ |
| Ausschüsse | 🏷️ Ausschussseite | ⬜ |
| Audiothek | 🎶 Audiothek | ⬜ |
| Audiothek – Archiv | 🎶 Audiothek - Archiv | ⬜ |
| Geschützter Bereich | 🔐 Passwort geschützt (allgemein / v1 / v2) | ⬜ |
| 404 | 🔎 404 v2 | ⬜ |

**Seiten ohne Figma-Frame** (würden aus Figma-Bausteinen gebaut — jeweils einzeln entscheiden):

| Seite | Status |
|---|---|
| Impressum (Pflicht) | ⬜ |
| Datenschutz (Pflicht) | ⬜ |
| Chronik / Geschichte der Kirche | ⬜ |
| Gemeindebrief | ⬜ |
| Weitere: ______ | ⬜ |

---

## 2. Datenquellen

### 2.1 ChurchTools (live, nichts wird kopiert)

| Daten | Verwendet auf | Status |
|---|---|---|
| Termine / Kalender | Termine, Startseite | ⬜ |
| Gruppen (öffentliche Gruppen-Homepage) | Gruppen, Startseite | ⬜ |
| Gruppen-Anmeldung | Gruppe (Detail) | ⬜ |
| Beiträge (Posts) | Blog / Aktuelles | ⬜ |
| Personen / Kirchenvorstand | Kirchenvorstand, Ausschüsse | ⬜ |
| Login für geschützte Bereiche (OAuth) | Geschützter Bereich | ⬜ |

### 2.2 Eigene Datenbank (Strato, MySQL/MariaDB)

Für Inhalte, die es in ChurchTools nicht gibt. Gepflegt über die ChurchTools-Extension.

| Daten | Verwendet auf | Status |
|---|---|---|
| Spendenziel / Spendenzwecke | Spenden | ⬜ |
| Seitentexte (Über uns, Impressum, Datenschutz …) | diverse | ⬜ |
| Audiothek (Aufnahmen, Metadaten) | Audiothek | ⬜ |
| Gemeindebrief-Ausgaben (PDF) | Gemeindebrief | ⬜ |
| Kontaktanfragen | Kontakt | ⬜ |
| Newsletter-Anmeldungen | Footer | ⬜ |

### 2.3 Bisherige Website kirche-cranzahl.de (nur nach Freigabe)

Die alte WordPress-Seite hat eine öffentliche Schnittstelle. Verfügbar wären
(Stand der Abfrage): **31 Seiten, 262 Beiträge** (Kategorien Aktuelles, Kirchennachrichten,
Bilder, Veranstaltungen) und **1.040 Mediendateien**.
Standard: **nichts übernehmen.** Einzelne Inhalte nur, wenn sie hier freigegeben werden:

| Inhalt | Status |
|---|---|
| ______ | ⬜ |

### 2.4 Jahreslosung (für CTA V2 oberhalb des Footers)

| Quelle | Status |
|---|---|
| Tabelle im Code, jährlicher automatischer Wechsel | ⬜ |

---

## 3. Verwaltung (ChurchTools-Extension)

Redakteure pflegen die Inhalte aus 2.2 direkt in ChurchTools. Geplanter Aufbau:

```
ChurchTools-Extension (Oberfläche in ChurchTools)
        │  HTTPS, Anmeldung über ChurchTools
        ▼
Website-API (Next.js auf Hostinger)
        │
        ▼
MySQL-Datenbank (Strato)
```

Offene Punkte:
- Welche Personen/Gruppen in ChurchTools dürfen die Website-Inhalte bearbeiten?

---

## 4. Offene technische Punkte

### Ist die Strato-Datenbank von Hostinger aus erreichbar?

Bei Strato-Webhosting-Paketen ist die MySQL-Datenbank häufig **nur von Strato-Servern**
aus erreichbar. Prüfen:

1. Strato-Kundenlogin → Paket → **Datenbankverwaltung**.
2. Hostnamen der Datenbank notieren (z. B. `rdbms.strato.de` oder ähnlich).
3. Nachsehen, ob es eine Option für **externen Zugriff / Remote-Zugriff** gibt.

Je nach Ergebnis:

| Fall | Lösung |
|---|---|
| Externer Zugriff möglich | Website verbindet sich direkt (verschlüsselt) mit Strato |
| Nur intern | kleine Schnittstelle (API) auf dem Strato-Webspace, oder Datenbank bei Hostinger |

Die Datenanbindung wird deshalb **austauschbar** gebaut (eine Datei für den Zugriff).
