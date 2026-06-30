# Session 6 — 17. Juni 2026
## Datenbanken, Supabase, SQL & Dokumentenmanagementsystem

**Coaching:** Synclaro KI-Gruppencoaching (Marco Heer)  
**Datum:** 17. Juni 2026  
**Teilnehmer:** Marvin (ZFG), Tobias, Andreas, Fabian  

---

## PERSÖNLICHE NOTIZEN (ZFG)

- OpenAI Endpunkte: Video, Bilder (Sora), Text, Sprache
- Supabase als Datenbankbetreiber
- SQL als Datenbanksprache
- SQL-Tabellen via ChatGPT programmieren → kopieren → in Supabase SQL-Editor einfügen
- **Zukunftsvision:** Claude baut Architektur für Sprachnachricht an Telegram → neues Mitglied (Name, Vorname, E-Mail, Geb.datum) → OpenAI extrahiert Daten strukturiert → SQL INSERT → GitHub-Script löst Geburtstags-Mail aus
- Programme laufen als HTML + localhost; Claude holt sich Daten via Supabase aus SQL-Datenbank

**To-Do-Liste:**
- [ ] Supabase-Konto anlegen
- [ ] SQL-Tabelle für DMS anlegen (SQL Editor oder Tabellen-Editor)
- [ ] DMS-Programm als HTML erstellen lassen
- [ ] OCR + Drag & Drop über Mistral-API-OCR einbauen
- [ ] MCP-Server anlegen und Supabase mit Claude verbinden
- 📺 Video ab 11:40 Uhr nachspielen (Supabase-MCP-Demo)

---

## 1. STATUS-RUNDE — WAS HAT DIE GRUPPE UMGESETZT?

### Marvin (ZFG)
- **Firmendossier:** Vor Betriebsbesuch ein Dossier per KI erstellt und als Hörbuch auf dem Weg dorthin gehört → anders vorbereitet, sehr nützlich
- **HeyGen.com API:** Avatar-Video-Generator angebunden, Video erstellt — Ergebnis weniger zufriedenstellend (kein KI-Problem, sondern Erwartungsproblem)
- **Schach-Coach App:** HTML-Anwendung mit Lichess-API (größter Open-Source-Schachanbieter) — live auf GitHub/Netlify; Chatbot für Schachpartienanalyse: welche Motive, welche Pläne? Läuft auf schachlich gutem Niveau für Vereinsspieler
- **Telegram Gegneranalyse:** Lichess-Nutzernamen eingeben → KI-Analyse erstellen lassen → als Hörbuch per Telegram empfangen

### Tobias
- Krank gewesen, kaum Zeit; Urlaub beginnt morgen
- ChatGPT-Erklärung von Endpoints gut verstanden (Restaurant-Metapher)
- **Projekt 1 (geplant):** E-Rechnungen aus Rechnungspostfach automatisch → richtiger DATEV-Mandant → Projektordner auf dem Laufwerk
- **Projekt 2 (geplant):** 5 Ausschreibungsportale automatisch überwachen → KI sucht nach vorgegebenen Begriffen → Ergebnisse werden wöchentlich geliefert (gut geeignet für Browser-Automatisierung)

### Andreas
- Mehrere kleine Tools ohne Verknüpfung untereinander gebaut
- **Bautagesbericht-Tool:** Wetterdaten via API abrufen + Excel-Baudokumentation in Ordner legen → Word-Dateien automatisch erstellen (ordnerbasiert, manuelle Befüllung); nächster Schritt: Datenbankanbindung

### Fabian
- Telegram-Bot nachgeholt (Vortag): funktioniert, aber nur wenn Claude lokal läuft → benötigt Online-Hosting (Render.com oder GitHub Actions)
- Planauskünfte-Portal-Integration teilweise gebaut: ein Portal funktioniert, ein weiteres noch nicht
- Generell: Viele kleine angefangene Projekte, die noch zusammenwachsen müssen

---

## 2. HAUPTTHEMA: DATENBANKEN

### Warum brauchen Programme Datenbanken?

**Das Problem:** Alle Teilnehmer haben Programme gebaut, die mit Daten arbeiten — aber die Daten lagen in Excel, Ordnern oder Google Sheets. Diese sind für Menschen gebaut, nicht für Maschinen.

**Das "Datenherz" eines Programms besteht aus drei Bausteinen:**
1. **Datenbank** — strukturierte, maschinenlesbare Datenhaltung
2. **Dateispeicher** — für PDFs, Bilder, Dokumente
3. **Ausführende Funktionen** — Automatismen (z.B. OCR, E-Mail-Trigger)

| Excel / Ordner | Datenbank (Supabase) |
|---|---|
| Für Menschen gebaut | Für Maschinen gebaut |
| Formeln per Hand eingegeben | SQL-Befehle per KI generiert |
| Langsam bei großen Datenmengen | Blitzschnell und skalierbar |
| Schwer für Programme anzuzapfen | Direkte API-Schnittstellen |
| Kein Echtzeit-Mehrgerätezugriff | Immer aktuell, von überall |

### Warum Supabase?
- Günstig (kostenlos startbar)
- Besonders gut von KI bedienbar
- DSGVO-konform betreibbar
- Direkt von Claude Code via MCP-Server steuerbar
- SQL-Datenbank + Dateispeicher + Edge Functions (= APIs) in einem

---

## 3. SQL — DIE SPRACHE DER DATENBANKEN

> **"Das sind Excel-Tabellen auf Koks."** — Marco Heer

SQL = Structured Query Language — die Programmiersprache für Datenbanken. Man schreibt es nicht selbst: KI generiert SQL auf Anfrage.

### Die drei Grundbefehle

**`CREATE TABLE`** — Tabelle erstellen

```sql
CREATE TABLE dms_documents (
  id             UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  typ            TEXT,        -- Rechnung, Angebot, Lieferschein...
  status         TEXT,        -- eingegangen, verarbeitet, archiviert
  eingang        TIMESTAMP DEFAULT now(),
  quelle         TEXT,        -- E-Mail, Scanner, Portal...
  email_absender TEXT,
  ocr_text       TEXT,
  mitarbeiter    TEXT,
  prioritaet     TEXT         -- normal, hoch, dringend
);
```

**`INSERT INTO`** — Daten einfügen

```sql
INSERT INTO dms_documents (typ, status, quelle, email_absender, mitarbeiter)
VALUES ('Rechnung', 'eingegangen', 'E-Mail', 'lieferant@firma.de', 'Nina');
```

**`SELECT`** — Daten abfragen und auswerten

```sql
-- Wer hängt hinterher?
SELECT mitarbeiter,
       COUNT(*) AS gesamt,
       SUM(CASE WHEN status = 'offen' THEN 1 ELSE 0 END) AS unerledigt,
       ROUND(100.0 * SUM(CASE WHEN status != 'offen' THEN 1 ELSE 0 END) / COUNT(*), 0) AS erledigungsquote
FROM dms_documents
GROUP BY mitarbeiter;

-- An welchen Tagen gibt es Überlast?
SELECT DATE(eingang) AS datum, COUNT(*) AS anzahl
FROM dms_documents
GROUP BY DATE(eingang)
ORDER BY anzahl DESC;
```

### Live in der Session: DMS-Tabelle wurde erstellt

1. ChatGPT generiert CREATE-Statement für `dms_documents`
2. Statement in Supabase SQL-Editor einfügen → Ausführen → Erfolg
3. KI generiert 150 realistische Testdatensätze (Rechnungen, Angebote, Lieferscheine, Stundenzettel...)
4. INSERT ausgeführt → **151 Einträge** in der Tabelle
5. Fehlerhafte SQL-Statements einfach zurück an KI → automatisch korrigiert

---

## 4. CLAUDE + SUPABASE VIA MCP-SERVER

### Was ist ein MCP-Server?

MCP (Model Context Protocol) = eine für KI optimierte API-Schnittstelle.

Claude versteht die Schnittstelle direkt — ohne extra Erklärung werden Datenbankoperationen als verfügbare "Tools" angeboten.

### Einrichtung (einmalig im Projektordner)

```bash
cd [projektordner]
# MCP-Server für Supabase installieren (via Claude Code)
# Supabase-Projekt-URL + API-Key eingeben (im Settings-Bereich von Supabase)
```

Nach der Einrichtung:
- Claude hat direkten Lese- und Schreibzugriff auf die Supabase-Datenbank
- Kein manuelles SQL-Kopieren und -Einfügen mehr
- Claude führt SQL autonom aus — als Aktion, nicht nur als Code-Vorschlag

### Vorher vs. Nachher

| Vorher (ohne MCP) | Nachher (mit MCP) |
|---|---|
| KI schreibt SQL | KI schreibt SQL |
| Mensch kopiert SQL | — |
| Mensch führt SQL aus | KI führt SQL direkt aus |
| Mensch prüft Ergebnis | Claude meldet Ergebnis |

---

## 5. DMS — DOKUMENTENMANAGEMENTSYSTEM

Das DMS wurde als gemeinsames Beispielprojekt für alle Teilnehmer gewählt, weil:
- Jeder Handwerksbetrieb kann es brauchen
- Es alle Bausteine demonstriert (DB, OCR, API, Weboberfläche)
- Es reale Geschäftsprozesse abbildet

### Vollständige Prozesskette (Ziel)

```
EINGANG (automatisch):
E-Mail empfangen → PDF-Anhang erkannt
→ OCR (Mistral-API) liest Dokumententext aus
→ KI kategorisiert: Rechnung / Angebot / Lieferschein / ...
→ SQL INSERT → Eintrag in dms_documents

VERWALTUNG (Weboberfläche als HTML):
HTML-App → Supabase SELECT → Tabelle anzeigen
Filter: Typ, Status, Datum, Mitarbeiter, Absender
Drag & Drop: PDF direkt hochladen

HANDLUNG (Automatismen):
Rechnung erkannt → Prüfaufgabe erzeugen
Rückstand > 10 Dokumente → Alarm
Genehmigt → PDF automatisch weiterleiten
```

### Mögliche Erweiterungen
- **Mitarbeiterauslastung:** Wer hat wie viel auf dem Tisch? Erledigungsquote in %
- **ODAV-Anbindung** (Handwerkskammern): Statt 5 Querfelder und 20 Minuten Wartezeit → sekundenschnelle SQL-Abfragen
- **Sprachinput:** "Neue Mitglieder" per Telegram-Sprachnachricht → OpenAI extrahiert Daten → SQL INSERT → Geburtstags-Mail

---

## 6. KERNAUSSAGEN DER SESSION

> **"Datenbanken sind Excel-Tabellen auf Koks."** — Marco Heer

> **"Früher haben Programmierer Datenbanken von Hand programmiert, von Hand befüllt, von Hand abgefragt. Jetzt schreibt KI das SQL — und via MCP führt sie es auch direkt aus."** — Marco Heer

> **"Es gibt 100 verschiedene Wege, wie Daten reinkommen — Webformular, Sprachnachricht, E-Mail, API. Welchen wähle ich?"** — Marco Heer

> **"Claude baut nur die Infrastruktur. Die ist DSGVO-konform eingerichtet, weshalb Claude hier wunderbar zum Einsatz kommen kann."** — Marco Heer

---

## 7. WICHTIGE WERKZEUGE

| Werkzeug | Zweck |
|---|---|
| supabase.com | Datenbank (PostgreSQL) + Storage + Edge Functions |
| SQL Editor (Supabase) | SQL-Befehle direkt ausführen |
| Tabellen-Editor (Supabase) | Tabellen visuell befüllen/prüfen |
| MCP-Server (Supabase) | Claude Code ↔ Supabase Direktverbindung |
| Mistral-API | OCR — Dokumente maschinell auslesen |
| Render.com | Telegram-Bot online hosten (ohne laufenden Claude) |
| ChatGPT / Claude | SQL-Statements generieren lassen |

---

## 8. DIE KOMPLETTE APP-ARCHITEKTUR (nach Session 6)

```
FRONTEND:   HTML-App (Netlify)
               ↕ API-Calls
BACKEND:    Supabase (Datenbank + Dateispeicher + Edge Functions)
               ↕ MCP
KI-STEUERUNG: Claude Code
               ↕ API
EXTERNE:    OpenAI (LLM, TTS, OCR) · Telegram · Wetter · etc.
               ↕ GitHub
VERSIONIERUNG: GitHub Repository (Auto-Deploy zu Netlify)
```

---

*Aufbereitet aus dem Transkript der Session vom 17. Juni 2026 | Synclaro KI-Gruppencoaching*
