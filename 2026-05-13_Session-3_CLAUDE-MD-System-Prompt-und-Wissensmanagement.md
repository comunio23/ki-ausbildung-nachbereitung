# Session 3 — 2026-05-13 — CLAUDE.md, System-Prompt-Strategie und Wissensmanagement-Aufbau

**Datum:** Mittwoch, 13. Mai 2026  
**Dauer:** ca. 126 Minuten (7.552 Sekunden)  
**Format:** Online-Session (Videokonferenz)  
**Reihe:** KI- und Automatisierungscoaching mit Marco Heer (Synclaro)  
**Datei:** `C:\Users\ZFG\Desktop\KI\Wissen aus Synclaro\2026-05-13_Session-3_CLAUDE-MD-System-Prompt-und-Wissensmanagement.md`

---

## Teilnehmer und Sprecher-Mapping

AssemblyAI (universal-2) vergab vier Speaker-Labels. Identifikation aus dem Kontext:

| Label     | Person                          | Hinweise im Transkript                                                                          |
|-----------|---------------------------------|-------------------------------------------------------------------------------------------------|
| Speaker A | Marco Heer + Tobias Zitzmann   | Marco: „hier spricht wieder Marco, der KI- und Automatisierungscoach." Tobias: Bericht über Homework-Woche (Hotels, Excel, Transkripte) — AssemblyAI hat beide Stimmen teilweise zusammengeführt |
| Speaker B | Janine                         | „Mein Mann ist Dozent an der Uni" — baut Lernwebsite für Universitätsvorlesung; Pac-Man-Projekt für Sohn |
| Speaker C | Marvin                         | Schachverein (80 Mitglieder), Geburtstags-Mail-Automation (Google Apps Script), Tetris für Kinder |
| Speaker D | Fabian Böhmer                  | „Ich war noch draußen auf der Baustelle"; Bagger-Bedienungsanleitung → HTML; Kaiserslautern      |

**Eingeschränkt dabei:** Andreas (unterwegs, konnte nicht aktiv teilnehmen — am Ende kurz zugeschaltet)

---

## Hausaufgaben-Runde: Was wurde in der Woche ausprobiert?

### Tobias (aus Speaker A rekonstruiert)
- Excel-Tabellen erstellen lassen
- Hotel-Anfragen mit KI-Auswertung erstellt (Hotel-Buchungen als häufige Aufgabe)
- Transkript-Arbeit aus Session 2 wiederholt
- E-Mail-Texte und Homepage überarbeiten lassen
- **Hinweis:** Das 20-Euro-Abo läuft bei intensiver Nutzung schnell ab

### Janine (Speaker B)
- **Lernwebsite für Universitätsvorlesung** gebaut: Ihr Mann ist Dozent und hält eine Grundlagenvorlesung. Janine hat die Inhalte in mehrere verknüpfte HTML-Dateien aufbereitet — inklusive interaktivem Quiz.
- Noch nicht für Studenten live, weil inhaltliche Gegenkontrolle durch den Dozenten fehlt.
- **Methodik für Feedback-Loop:** Sprachnachricht per WhatsApp vom Mann → transkribieren → in KI einspeisen.
- **Hausaufgabe (Programm bauen):** Entschieden für Pac-Man mit eigenen Leveln und Sound (Wunsch des Sohnes) — läuft bereits, die .exe fehlt noch.

### Marvin (Speaker C)
- **Google Sheet → HTML-Organisationstool**: Gemeinsam genutzte Familien-Google-Sheet als schönere HTML-Ansicht umgebaut.
- **Tetris-Spiel** gebaut → spielen die Kinder.
- **Präsentations-HTML** für Workshops: Inhalt als interaktive HTML-Seite → deutlicher Wow-Effekt beim Publikum, einfachere Zustimmung zu Vorhaben.
- **Geburtstags-Website**: 80 Vereinsmitglieder (Schachverein), täglich sichtbar, wer Geburtstag hat.
- **Geburtstags-Mail-Automation** (Google Apps Script + Gmail): Automatische Glückwunsch-Mails täglich zwischen 9 und 10 Uhr. Problem: ursprüngliche Excel-Datei statt Google Sheet → nach Konvertierung zu Google Sheet lief es. Neue Mitglieder einfach eintragen, automatisch im System.

### Fabian (Speaker D)
- **Bagger-Bedienungsanleitung → interaktive HTML-Website**: 180-seitiges PDF für spezielle Baggersteuerung → Claude analysiert und erstellt interaktive Zusammenfassung mit Fokus auf Ladungssicherung und Sondersteuerung.
- Problem: musste ca. 30 Mal auf „Ja" klicken → Anlass für heutiges Thema: Admin-Modus.

---

## Themenblock 1 — Admin-Modus: `--dangerously-skip-permissions`

### Was wurde besprochen?

Marco erklärt, warum er den Admin-Modus bewusst erst später vorstellt: Man soll den normalen Modus kennenlernen und Vertrauen aufbauen, bevor alle Rückfragen deaktiviert werden.

**Claude im Admin-Modus starten:**
```
claude --dangerously-skip-permissions
```

- Flags beginnen immer mit `--` (doppelter Bindestrich)
- Im Admin-Modus fragt Claude **nicht mehr** um Genehmigung für Aktionen
- Unten im Terminal erscheint: **„Bypass Permissions"**
- Beim ersten Start: einmalige Warnung/Bestätigung

**Weitere wichtige Flags:**

| Flag | Funktion |
|------|----------|
| `--dangerously-skip-permissions` | Admin-Modus — keine Rückfragen mehr |
| `--continue` | Letzten Chatverlauf im aktuellen Ordner fortsetzen |
| `--resume` | Liste aller Chatverläufe des aktuellen Ordners anzeigen und auswählen |

Flags lassen sich **beliebig kombinieren**:
```
claude --dangerously-skip-permissions --continue
claude --dangerously-skip-permissions --resume
```

**Pfeiltaste ↑** im Terminal: Letzte Befehle wiederholen (je nach Windows-Version verfügbar).

**Wann den Admin-Modus nutzen?**
> „Schaut genau hin, was er macht. Lasst euch erklären, was er macht und warum. Und so lernt ihr Vertrauen und Kontrolle. Bei mir darf die Kiste inzwischen im Admin-Modus die ganze Nacht durcharbeiten — aber ich weiß auch, wovon ich rede."

Marco empfiehlt: Wenn man bei normaler Nutzung nie auf „Nein" gedrückt hat, weiß man, dass Claude gute Entscheidungen trifft. Dann ist Admin-Modus sinnvoll.

### ✅ Learnings

- `--dangerously-skip-permissions` ist der exakte Flag-Name für den Admin-Modus — einmal notieren, dann immer per Pfeiltaste abrufbar.
- Mehrere Flags können in einer Zeile kombiniert werden.
- `--resume` zeigt Chatverläufe **pro Ordner**, nicht global — weil die Chathistorie in dem Ordner gespeichert wird, wo Claude läuft.
- Empfehlung: Admin-Modus erst nutzen, wenn man den normalen Modus versteht und einschätzen kann.

---

## Themenblock 2 — Terminal-Navigation: `cd`, `ls`, `cd ..`

### Was wurde besprochen?

**Ordner wechseln:**
```
cd Ordnername
```

**Tab-Autovervollständigung:**
- `Tab` nach ersten Buchstaben → automatische Vervollständigung des Ordnernamens
- Mehrfach `Tab` → durch alle passenden Optionen schalten

**Dateien und Ordner auflisten:**
```
ls
```

**Eine Ebene höher gehen:**
```
cd ..
```
(mehrfach hintereinander möglich)

**Praxis-Tipp von Marco — Navigation mit Teilnamen:**
```
cd pr[Tab]            →  cd privat/
cd privat/pro[Tab]    →  cd privat/programmierung/
```

**Chathistorie ist ordnergebunden:**  
`--resume` im Desktop-Ordner zeigt andere Chats als `--resume` im Synclaro-Ordner. Die Chathistorie liegt als Datei in dem Ordner, in dem Claude gestartet wurde.

> „Ihr müsst es quasi händisch bis zur KI schaffen — und dann kann sie euch weiterhelfen."

**Claude als Navigationshilfe nutzen:**
> „Ich frage einen laufenden Claude: ‚Gib mir den CD-Befehl, um in den Holzbau-März-Ordner reinzukommen.' Er sucht schnell und gibt mir den Befehl."

### ✅ Learnings

- `cd`, `ls` und `cd ..` sind die drei wichtigsten Terminal-Befehle für die Navigation.
- Tab-Autovervollständigung spart Tipparbeit erheblich — bereits die ersten 2–3 Buchstaben reichen.
- **Chathistorie ist ordnergebunden**: `--resume` zeigt immer nur die Chats des aktuellen Ordners.
- Claude selbst kann als Navigationshilfe dienen — bei unbekannten Pfaden einfach fragen.
- Schrägstriche in Pfaden: Mac nutzt `/`, Windows nutzt `\` — relevant bei Pfad-Angaben.

---

## Themenblock 3 — System Prompt und CLAUDE.md

### Was wurde besprochen?

**Die drei System-Prompt-Ebenen (Wiederholung und Vertiefung):**

| Ebene | Wer schreibt ihn? | Inhalt |
|-------|------------------|--------|
| Hersteller-System Prompt | Anthropic | Modellverhalten, Sicherheit, Ehrlichkeit |
| Harness-System Prompt | Claude Code (Anthropic) | Tool-Beschreibungen, Harness-Regeln, Zugriffsrechte |
| **User-System Prompt** | **Wir selbst** | Unsere Informationen und Verhaltensanweisungen |

**Was ist der User-System Prompt?**  
Der einzige System Prompt, den wir editieren können. Er wird **automatisch vor jedem Chat** an die KI übergeben — noch vor unserem ersten eigentlichen Prompt. Damit „weiß" Claude vom ersten Token an, wer wir sind und was er beachten soll.

**Wo liegt der User-System Prompt?**  
In einer Datei namens **`CLAUDE.md`**. Der Claude-Code-Harness sucht beim Start automatisch nach dieser Datei und lädt sie.

> „Eigentlich musst du nie mehr in irgendwelche Dateien irgendwas reinschreiben. Die Zeit ist vorbei. Du sagst Claude, was er da reinschreiben soll."

**Demo auf Fabians Rechner:**  
Fabian erstellt eine lokale CLAUDE.md, schreibt Namen und Alter rein, startet Claude neu → Claude weiß ohne Nachfragen, wer er ist.

---

### Die CLAUDE.md-Hierarchie

```
C:\                              ←  [1] Globale CLAUDE.md  (wird IMMER geladen)
  └─ Users\
       └─ FBöhmer\
            └─ Desktop\          ←  [2] Optionale CLAUDE.md
                 └─ KI\          ←  [3] Optionale CLAUDE.md  ← hier läuft Claude
```

**Ladereihenfolge:** Von oben (global) nach unten (lokal). Claude lädt **alle CLAUDE.md-Dateien entlang des Ordnerpfades** beim Start.

**Was wird NICHT geladen:**
- CLAUDE.md-Dateien in Unter-Ordnern (unterhalb des aktuellen Ordners)
- CLAUDE.md-Dateien in Nebenordnern (auf gleicher Ebene, aber anderer Pfad)

**Globale CLAUDE.md:**
- Liegt im Claude-Code-Konfigurationsverzeichnis (nicht im normalen Dateisystem-Pfad)
- Wird **immer** geladen, egal in welchem Ordner Claude gestartet wird
- „Die Mutter aller CLAUDE.mds" — ideal für Informationen, die immer gelten

**Strategische Einsatzmöglichkeiten:**

```
Einfach:    Nur globale CLAUDE.md — alles an einem Ort
Modular:    Globale CLAUDE.md für persönliche Daten
            + lokale CLAUDE.md je Themenordner (z. B. nur Bauvorhaben-Infos)
```

> „Ich habe einen Trostpflaster-Ordner — da steht im System Prompt, dass Claude besonders nett sein soll. Und einen Monthly-Review-Ordner für Firmenfinanzen — da ist nichts mit Zuspruch, da wird faktenbasiert gearbeitet."

**Empfehlung von Marco:** Maximal zwei KMS-Wissensmanagement-Systeme — eines für alles oder getrennt privat/beruflich.

### ✅ Learnings

- Der User-System Prompt = **CLAUDE.md** — der Name ist fest, andere Dateinamen werden nicht automatisch geladen.
- Alle anderen `.md`-Dateien müssen im Chat explizit referenziert werden; CLAUDE.md nicht.
- CLAUDE.md-Dateien entlang des Ordnerpfades werden **von global nach lokal** geladen.
- Globale CLAUDE.md wird **immer** geladen — ideal für persistente Basis-Informationen (Name, Kontext, KMS-Pfad).
- Lokale CLAUDE.md nur für kontext-spezifisches Wissen (z. B. Bauvorhaben-Infos nur im Bauvorhaben-Ordner).
- Formulierung in der CLAUDE.md: beliebig — Claude selbst schreiben lassen (auch per WhisperFlow einsprechen).

---

## Themenblock 4 — Markdown-Format

### Was wurde besprochen?

**Was ist Markdown?**  
Ein Textformat, das den Kompromiss zwischen **menschlicher Lesbarkeit** und **Maschinenlesbarkeit** darstellt.

| Format      | Menschlich lesbar | Maschinenlesbar    |
|-------------|:-----------------:|:------------------:|
| Word (.docx)| ✅                | ❌ (zu aufwendig)  |
| Plain Text (.txt) | ✅          | ⚠️ (keine Struktur)|
| **Markdown (.md)** | ✅         | ✅                 |
| Python/JavaScript | ❌        | ✅                 |

**Markdown-Grundsyntax:**

| Symbol | Bedeutung | Entspricht in Word |
|--------|-----------|--------------------|
| `# Text` | Überschrift 1 (größte) | Überschrift 1 |
| `## Text` | Überschrift 2 | Überschrift 2 |
| `### Text` | Überschrift 3 | Überschrift 3 |
| `**Text**` | Fettdruck | Fett |
| `*Text*` | Kursiv | Kursiv |
| ` ```code``` ` | Code-Block | Festbreitenschrift |
| `\| Spalte \| Spalte \|` | Tabelle | Tabelle |

> „Irgendwie muss KI damit klarkommen und irgendwie müssen wir damit klarkommen. Das ist der perfekte Kompromiss aus menschlicher und maschineller Lesbarkeit."

**Warum nicht .txt?**  
TXT hat keine Struktur — keine Überschriften, keine Tabellen, keine Hervorhebungen. Markdown kodiert diese Informationen als Zeichen (z. B. `#`), die eine Maschine auswerten kann.

**Warum nicht .docx?**  
Word-Dateien sind binär kodiert, komplex für Maschinen. KI kann sie verarbeiten, aber Markdown ist deutlich effizienter.

### ✅ Learnings

- **Markdown ist das Format der Wahl** für alles, was Mensch und KI gemeinsam lesen und schreiben sollen.
- `#` = Überschrift 1, `##` = Überschrift 2, `###` = Überschrift 3 — exakt wie Word's Überschrift-Ebenen, nur als Zeichen.
- KI hat keine Augen → optische Formatierung (fett, groß, kursiv) muss durch Zeichen ausgedrückt werden.
- CLAUDE.md und alle KMS-Dateien werden in Markdown geschrieben — der Harness versteht das nativ.
- `.md` als Dateiendung steht für Markdown.

---

## Themenblock 5 — Wissensmanagement Level 1: Logbuch mit Stempel-System

### Was wurde besprochen?

**Motivation — das Bordstein-Problem:**
> „Wir stellen alle gerade fest, dass wir mit Claude einen äußerst fähigen Arbeiter haben, den wir aber auf dem Bordstein vor unserer Firma getroffen haben. Super smartes Kerlchen mit tollen Tools. Aber er weiß über unsere Firma nichts."

Ziel: Claude von einem uneingearbeiteten Fremden zu einem **eingearbeiteten Mitarbeiter** machen, der unsere Fachterminologie kennt, unsere Abläufe versteht und aus Erfahrung lernt.

**KMS-Struktur Level 1:**
```
KI/
  └─ KMS/
       └─ logbuch.md
```

**Das Logbuch-Stempel-Format:**
```
[LOG-0001]
```
Jeder Logeintrag beantwortet diese 8 Fragen vollständig:

| Frage | Inhalt |
|-------|--------|
| Was? | Welche Aktion, welche Dateien, welches Thema? |
| Wie? | Tools, Befehle, Methoden, Vorgehensweise |
| Wo? | Verzeichnis, System, App, Kontext |
| Wann? | Datum und Uhrzeit |
| Warum? | Motivation, Auftrag, Ziel |
| Unter welchen Umständen? | Wer war dabei? Welcher Rahmen? |
| Was war vorher? | Relevante Ereignisse davor |
| Was war nachher? | Ergebnis, Folgezustand, offene Punkte |

> „Keine Token-Sparmaßnahmen — maximale Vollständigkeit hat Priorität."

**Globale CLAUDE.md-Eintrag:**  
Claude wird angewiesen: Auf diesem Computer wird ein KMS gepflegt. Wo es liegt. Und dass er proaktiv Log-Einträge schreiben soll.

**Der Mega-Prompt (von Marco diktiert, auf Fabians Rechner umgesetzt):**  
Marco's Initialisierungs-Prompt für das KMS enthält in einem einzigen Prompt:
- KMS-Ordner anlegen (`KI/KMS/`)
- `logbuch.md` erstellen mit Stempel-Format `[LOG-XXXX]`
- 8-Fragen-Schema für jeden Eintrag definieren
- Globale CLAUDE.md mit KMS-Hinweisen befüllen
- Ersten Log-Eintrag über die KMS-Einrichtung selbst schreiben

### ✅ Learnings

- Das KMS startet mit einem einzigen Ordner und einer einzigen Datei: `KI/KMS/logbuch.md`.
- Stempel `[LOG-XXXX]` sind stabiler als Seitenzahlen — sie verschieben sich nicht, wenn die Datei wächst.
- Maximale Vollständigkeit > Effizienz im Logbuch — das ist die Datei, in der buchstäblich alles drinstehen soll.
- Die globale CLAUDE.md als Träger der KMS-Anweisung sorgt dafür, dass jede zukünftige Claude-Session das KMS kennt.

---

## Themenblock 6 — Wissensmanagement Level 2: /post-Command

### Was wurde besprochen?

**Problem — nachlassende Konzentration bei langen Sessions:**
> „LLMs können, wie wir Menschen, bei langen Konversationen Anweisungen von vor 5 Stunden nicht mehr so konsequent befolgen. Das unterscheidet eine KI von einem deterministisch programmierten Skript."

Wenn das Context Window sich füllt, verliert die frühe System-Prompt-Anweisung (‚schreib immer Log-Einträge') an Gewicht.

**Lösung: Der `/post`-Command**
- Ein **Skill** (eingepackter, wiederverwendbarer Prompt) namens `post`
- Wird am Ende jeder Session manuell aufgerufen: `/post`
- Prüft rückblickend: Wurde alles Wichtige als Log-Eintrag festgehalten?
- Falls nicht: Fehlende Einträge werden sofort nachgeholt.
- Das „Feierabend-Ritual" vor dem Schließen von Claude Code.

**Was ist ein Skill?**
> „Ein Skill ist im Prinzip ein Platzhalter für eine Riesenlösung, die öfter vorkommt. Ihr verpackt die Anweisung einmal in einen Skill. Dieser Skill speichert sich Claude in einer Konfigurationsdatei — dann ist gut."

**Neustart nach Skill-Erstellung:** Wie ein neu installiertes Programm muss Claude einmal neu gestartet werden, damit ein neuer Skill wirksam wird.

**Die Kombination macht das System robust:**
```
CLAUDE.md  (passiv)  →  Claude erinnert sich proaktiv ans Logging
/post      (aktiv)   →  Manuelle zweite Sicherheitsstufe am Sitzungsende
```

### ✅ Learnings

- LLMs sind bei langen Kontexten unzuverlässig bezüglich früher Instruktionen — auch bei System-Prompt-Anweisungen (→ bereits in L-0001 dokumentiert).
- Der `/post`-Command schließt die Lücke, die CLAUDE.md allein lässt.
- Skills = wiederverwendbare Prompts, gespeichert in einer Konfigurationsdatei, erreichbar per `/skillname`.
- Skills werden erst nach einem Claude-Neustart wirksam.

---

## Themenblock 7 — Wissensmanagement Level 3: Indexierung

### Was wurde besprochen?

**Problem — wachsende Dateien:**  
Ein Logbuch mit hunderten Einträgen lässt sich nicht effizient vollständig laden. Jedes Mal alle Tokens zu verbrauchen würde das Context Window verschwenden und die Modellkonzentration belasten.

**Lösung: Index am Dateianfang**
```markdown
## INDEX
[LOG-0001] — KMS-Grundeinrichtung: Ordner und Logbuch angelegt
[LOG-0002] — /post-Command als zweite Sicherheitsstufe eingerichtet
[LOG-0003] — ...
---
[LOG-0001]
(vollständiger Eintrag)
---
[LOG-0002]
...
```

**Warum Stempel statt Seitenzahlen?**
> „In digitalen Dateien können wir theoretisch zwischen Einträgen etwas einfügen, was Zeilennummern verschiebt. Stempel sind unveränderlich — LOG-0236 bleibt immer LOG-0236, egal was sich um ihn herum verändert."

**Das Such-Protokoll (wie KI damit umgeht):**
1. Nur die ersten ~30 Zeilen laden (der Index)
2. Nach Stichwort suchen → passenden Stempel identifizieren
3. **Volltext-Suche** nach der Stempel-Nummer (z. B. `0236`) → findet **exakt 2 Treffer**: Index-Zeile + Eintragskopf
4. Alles zwischen `[LOG-0236]` und `[LOG-0237]` laden — das ist der relevante Inhalt

**Ergebnis:** Statt das gesamte Logbuch zu laden → 3 gezielte Operationen, minimaler Token-Verbrauch.

> „Das Stempel-System habe ich nach 1.000 fehlgeschlagenen Versuchen so entwickelt. Die Indexierung an sich ist kein neues Konzept — aber diese spezifische Umsetzung ist Marco Heer Erfahrung."

### ✅ Learnings

- **Indexierung** = IT-Äquivalent eines Buchverzeichnisses — aber mit Stempeln statt Seitenzahlen (→ bereits in L-0002 und L-0003 dokumentiert).
- Das Suchmuster: Index laden → Stempel identifizieren → Volltext-Suche nach Stempel-Zahl → exakt 2 Treffer.
- Dies ist **Context Engineering**: Nur die relevanten Informationen laden, nicht die ganze Datei.
- Index-Pflege gehört zur Logbuch-Routine: Jeder neue Eintrag bekommt auch eine neue Index-Zeile.

---

## Themenblock 8 — Wissensmanagement Level 4: learnings.md & decisions.md

### Was wurde besprochen?

**Motivation:**
> „Learnings und Entscheidungen sind lebensbestimmende Events in unserem Leben. Sie verdienen es, nochmal irgendwo anders separat festgehalten zu werden."

**Zwei neue Dateien:**
```
KI/
  └─ KMS/
       ├─ logbuch.md     ←  Alles, vollständig, [LOG-XXXX]
       ├─ learnings.md   ←  Erkenntnisse, kompakt, [L-XXXX]
       └─ decisions.md   ←  Entscheidungen, kompakt, [D-XXXX]
```

**Format learnings.md:**
```
[L-XXXX]
Datum    : YYYY-MM-DD
Kategorie: ...
Learning : 2–5 Sätze — vollständig verständlich ohne Logbuch
Kontext  : 1–3 Sätze — Wie/Wo/Warum gelernt?
→ Log-Referenz: [LOG-XXXX]   ← PFLICHT, ausnahmslos
```

**Format decisions.md:**
```
[D-XXXX]
Datum        : YYYY-MM-DD
Bereich      : ...
Entscheidung : 2–5 Sätze — klar und eindeutig formuliert
Begründung   : 1–3 Sätze
Auswirkung   : 1–3 Sätze
→ Log-Referenz: [LOG-XXXX]   ← PFLICHT, ausnahmslos
```

Beide Dateien haben **ebenfalls einen Index** am Dateianfang.

**Die Rollen im KMS:**
| Datei | Charakter | Frage die sie beantwortet |
|-------|-----------|---------------------------|
| logbuch.md | Vollständigkeit, „Warum und Wie" | „Was ist damals alles passiert?" |
| learnings.md | Schnellzugriff | „Was haben wir gelernt?" |
| decisions.md | Schnellzugriff | „Was haben wir beschlossen?" |

**Anwendungsbeispiel (Marco):**
> „In zwei Jahren entscheide ich mich, etwas zu machen. Claude sagt mir: ‚Laut Decision 534 wolltest du das eigentlich niemals mehr machen. Der Grund steht in Log-Eintrag 302 — wir sind damals auf die Schnauze gefallen.' Willst du das wirklich machen?"

**Erweiterung des /post-Commands:**  
Der Post-Skill wird so angepasst, dass er bei Sitzungsende auch prüft, ob alle Learnings und Decisions korrekt in die jeweiligen Dateien eingetragen wurden.

### ✅ Learnings

- **Learnings und Decisions verdienen separate Dateien** — nicht weil das Logbuch sie nicht enthält, sondern weil sie so häufig und gezielt gebraucht werden (→ bereits in L-0004 dokumentiert).
- **Jeder Eintrag hat eine Pflicht-Querreferenz** zurück zum Logbuch — ausnahmslos.
- Das Logbuch ist die Quelle der Vollständigkeit; die Spezial-Dateien sind die Quelle der Schnelligkeit.
- Vor jeder neuen Aufgabe: KI prüft erst Learnings- und Decisions-Index, bevor sie handelt.

---

## Themenblock 9 — KMS als gemeinsames System: Mensch und KI

### Was wurde besprochen?

**Abschluss-Anweisung in der globalen CLAUDE.md (Marcos letzter Prompt der Session):**

**Grundprinzip 1 — Gemeinsames Eigentum:**
- **Der Mensch trägt ein:** Persönliche Erkenntnisse, Entscheidungen, Erlebnisse aus dem Chat heraus.
- **Die KI trägt ein:** Aktionen, erkannte Fehler (mit Korrektur), Entscheidungen im Auftrag des Nutzers.
- Fehler im KMS festzuhalten ist kein Versagen — es ist der Kern des Lernprozesses:
  > „‚Ich habe einen Fehler gemacht' ist kein Versagen — es ist ein wertvoller Eintrag."

**Grundprinzip 2 — Aktive Nutzung:**
> „Das KMS ist kein Archiv, das verstaubt. Es ist aktives Arbeitswerkzeug."

Vor jeder neuen Aufgabe — immer zuerst:
1. **decisions.md-Index** prüfen: Haben wir zu diesem Thema etwas entschieden?
2. **learnings.md-Index** prüfen: Haben wir zu diesem Thema etwas gelernt oder Fehler gemacht?
3. Bei Treffern: vollständigen Eintrag laden, **dann erst** anfangen.

> „Bevor wir hier anfangen irgendwas zu machen, gucken wir erst — haben wir in der Vergangenheit in Sachen CRM, in Sachen Automatisierung irgendwelche Decisions gemacht? Haben wir Fehler gemacht, die wir nicht wiederholen wollen?"

**Die Verwandlung: Wissensmanagement → Erfahrungsmanagement:**
> „Ab dem Punkt, wo die KI Erfahrungen gespeichert hat und darauf zurückgreift — ab da sprechen wir nicht mehr von Wissensmanagement, sondern von Erfahrungsmanagement."

**Zukunftsperspektive:**
> „Was wir heute gemacht haben, ist noch ziemlich nubihaft — Dateien auf dem Computer. Das ist ehrlich gesagt ziemlich 2024, aber das ist okay. Wir werden das professionalisieren: Vektordatenbanken, Server, weltweit erreichbar, nur für uns. Alles fancy dancy."

> „Das Konzept — dass Dinge niedergeschrieben werden, dass Learnings separat aufgeschrieben werden — das ist State of the Art. Das ist, was moderne KI-Nutzung ausmacht. Das haben wir heute gemacht."

**Die 5 Ausbaustufen des Wissensmanagements:**  
Marco kündigt an, dass es 5 Ausbaustufen gibt. Heute: **Level 1 (Grundeinrichtung)**. Das Thema Wissensmanagement zieht sich durch alle weiteren Sessions — über die nächsten ~21 Wochen.

### ✅ Learnings

- **KMS = gemeinsames Eigentum** von Mensch und KI. Beide tragen bei, beide nutzen es.
- „Erst nachschlagen, dann handeln" — KI konsultiert KMS vor jeder neuen Aufgabe.
- Fehler-Dokumentation im KMS ist wertvoll, nicht peinlich — Wiederholungsfehler sind teuer.
- Das heutige System (Dateien auf dem PC) ist Stufe 1 von 5 — bewusst einfach gehalten, um die Konzepte zu verstehen.
- Studien: Mitarbeiter verbringen **40 Minuten pro Tag** mit Informationssuche — KMS kann das auf ein Zehntel reduzieren.

---

## Marvin's Frage: KMS im Handwerksunternehmen

Eine besonders relevante Frage aus dem Gruppenkontext:

**Marvin fragt:**
> „Wenn ich drei Kollegen habe, die sehr viel implizites Wissen angehäuft haben — durch Renteneintritt geht das verloren. Ich würde die Informationen (Interviews, Texte) in MD-Dateien packen und Claude damit befragen. Ist das die richtige Denke?"

**Marcos Antwort:**
> „Ja — technisch ein bisschen anders organisiert, aber genau die richtige Denke. Das ist das größte Thema, was wir hier im Gruppencoaching haben werden. Es fängt jetzt an und endet erst in 21 Wochen."

**Wichtige Klarstellung zur KMS-Struktur:**  
Es gibt **ein einziges KMS pro Computer** (maximal zwei: privat/beruflich). Claude findet es über die globale CLAUDE.md, egal in welchem Ordner Claude gerade läuft. Das KMS ist nicht ordnergebunden — nur die Chathistorie ist es.

---

## Glossar (neue Begriffe dieser Session)

| Begriff | Erklärung |
|---------|-----------|
| `--dangerously-skip-permissions` | Claude-Code-Flag für Admin-Modus: keine Rückfragen mehr |
| `--continue` | Flag: Letzten Chatverlauf des aktuellen Ordners fortsetzen |
| `--resume` | Flag: Alle Chatverläufe des aktuellen Ordners anzeigen und auswählen |
| Flag | Parameter beim Programmstart, beginnt mit `--`, steuert Verhalten des Programms |
| `cd` | Terminal-Befehl: Change Directory (Ordner wechseln) |
| `ls` | Terminal-Befehl: List (Dateien und Ordner auflisten) |
| `cd ..` | Terminal-Befehl: Eine Ordnerebene nach oben wechseln |
| Tab-Autovervollständigung | Tab-Taste vervollständigt Ordner- und Dateinamen automatisch |
| User-System Prompt | Der Teil des System Prompts, den wir selbst editieren können |
| CLAUDE.md | Dateiname für den User-System Prompt — vom Harness automatisch beim Start geladen |
| Globale CLAUDE.md | Die CLAUDE.md im Claude-Code-Konfigurationsverzeichnis — wird immer geladen, egal in welchem Ordner Claude startet |
| CLAUDE.md-Hierarchie | Alle CLAUDE.mds entlang des Ordnerpfades werden geladen (global → lokal) |
| Markdown (.md) | Textformat: Kompromiss zwischen menschlicher und maschineller Lesbarkeit |
| `#` / `##` / `###` | Markdown-Syntax für Überschriften (Größe 1/2/3) |
| KMS | Knowledge Management System — Ordner mit strukturierten Wissens-Markdown-Dateien |
| Skill | Eingepackter, wiederverwendbarer Prompt, erreichbar per `/skillname` |
| `/post` | Skill: Abschluss-Check nach einer Session — prüft und vervollständigt Log-Einträge |
| Indexierung | Index am Dateianfang mit Kurzbeschreibung pro Eintrag — für effizienten Suchzugriff |
| Log-Stempel | Format `[LOG-XXXX]` — eindeutige, unveränderliche Kennung pro Logeintrag |
| learnings.md | KMS-Datei: Kompakte Übersicht aller Erkenntnisse, Stempel `[L-XXXX]` |
| decisions.md | KMS-Datei: Kompakte Übersicht aller Entscheidungen, Stempel `[D-XXXX]` |
| Context Engineering | Gezieltes Laden von Informationen ins Context Window — nur was gebraucht wird |
| Erfahrungsmanagement | KMS auf dem nächsten Level: KI greift auf gespeicherte Erfahrungen zurück, bevor sie handelt |
| Vektordatenbank | Zukünftige Ausbaustufe des KMS: semantische Suche statt Volltextsuche |

---

## Hausaufgaben bis zur nächsten Session

> „Ich bitte euch, das wirklich zu pflegen. Wir brauchen nächstes Mal Wissensmanagement mit guten 20–30–40–50 Einträgen. Ein wohlgefülltes Wissensmanagement brauchen wir nächste Mal."

- [ ] KMS auf dem eigenen Rechner einrichten: Ordner `KI/KMS/`, Datei `logbuch.md`, globale CLAUDE.md befüllen
- [ ] `/post`-Skill einrichten (und nach Erstellung Claude einmal neu starten)
- [ ] Indexierung in `logbuch.md` einbauen
- [ ] `learnings.md` und `decisions.md` anlegen
- [ ] KMS aktiv nutzen: Mindestens 20–50 Einträge bis zur nächsten Session
- [ ] Marcos Prompts aus dem Chat sichern (per E-Mail erhalten oder selbst kopieren)

**Marcos Prompts für diese Session:** Als Markdown-Datei per E-Mail an Tobias Zitzmann und weitere Teilnehmer versendet.

---

## Ausblick nächste Session

- KMS-Review: Alle zeigen ihr befülltes Wissensmanagement
- Nächste Ausbaustufe(n) des Wissensmanagements
- Langfristig (über ~21 weitere Wochen): 5 Ausbaustufen bis hin zu Vektordatenbanken und Server-basiertem KMS
- Wissensmanagement für Handwerksbetriebe: implizites Wissen von Mitarbeitern persistieren (Marvin's Frage als roter Faden)

---

## Zitate dieser Session

> „Man muss es quasi händisch bis zur KI schaffen — und dann kann sie euch weiterhelfen."  
— Marco Heer, zur Terminal-Navigation

> „Die Zeit ist vorbei, dass ihr selbst in Dateien irgendwas reinschreiben müsst. Ihr sagt Claude, was er da reingeschreiben soll."  
— Marco Heer, zur CLAUDE.md-Befüllung

> „Wir haben einen äußerst fähigen Arbeiter, den wir auf dem Bordstein vor unserer Firma getroffen haben. Super smartes Kerlchen. Aber er weiß über unsere Firma nichts."  
— Marco Heer, zur KMS-Motivation

> „Die richtige Information, zum richtigen Ort, zum richtigen Zeitpunkt kann richtig viel wert sein."  
— Marco Heer, zum Wert von Wissensmanagement

> „Wenn wir in Zukunft irgendwas machen, sagt Claude mir: ‚Laut Decision 534 wolltest du das eigentlich niemals mehr machen. Willst du das wirklich tun?'"  
— Marco Heer, über KMS als Erfahrungsgedächtnis

> „Das Konzept, dass KI sich selbst Wissen speichert — das ist eines der mächtigsten Konzepte, die es auf der Welt gibt."  
— Marco Heer

> „Das ist State of the Art. Das ist, was moderne KI-Nutzung ausmacht. Und das haben wir heute gemacht."  
— Marco Heer, über das heute etablierte KMS-Konzept

> „Studien haben gezeigt, dass Mitarbeiter pro Tag 40 Minuten mit der Informationssuche beschäftigt sind. Wir können das locker zehnteln."  
— Marco Heer

> „‚Ich habe einen Fehler gemacht' ist kein Versagen — es ist ein wertvoller Eintrag."  
— Marco Heer, zur Fehlerkultur im KMS
