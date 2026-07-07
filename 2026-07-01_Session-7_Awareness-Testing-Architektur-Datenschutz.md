# Session 7 — 1. Juli 2026
## Awareness-Testing, App-Architektur (Edge Functions) & Datenschutz-Entscheidungsbaum

**Coaching:** Synclaro KI-Gruppencoaching (Marco Heer)
**Datum:** 1. Juli 2026
**Teilnehmer:** Marvin (ZFG), Tobias, Andreas, Fabian (Fabi), Janine (neu/wieder dabei)

---

## PERSÖNLICHE NOTIZEN (ZFG)

- Schachcoach: Partieeinlesen/Formulare-Erkennung über Mistral OCR geplant
- Idee: Datenbank mit eigenen Schachpartien digitalisieren (OCR + Engine + Eröffnungsdatenbank)
- Fuhrparkmanager erfolgreich auf Supabase/SQL umgestellt
- **Offenes To-do:** Mailerinnerung (Alarmierung bei Datum < 60 Tage entfernt)
- **Kernproblem, das die Session ausgelöst hat:** Fehleranalyse — obwohl gesagt wurde "prüfe alles auf 100%iger Vollständigkeit", werden Fehler trotzdem übersehen → Frage nach dem "richtigen Prompt für richtiges Awareness-Testing"

**Der von Marco Heer in der Session diktierte Workflow (Notiz-Fassung):**
1. NICHT fragen: "Jetzt schau noch mal, ob alles in Ordnung ist und gut läuft."
2. `/post`
3. `/compact`
4. Codebase-Analyse: jede Funktionalität, jeden Datenspeicherort, jeden Datenfluss, jede Datenverarbeitung, jede User-Interaktion im Frontend sichtbar machen
5. Autonome Testung mittels Browser-Usage (Chrome oder Playwright) — alle Konsequenzen messen (Datenbank-Einträge, Weiterleitungen, Erwartungshaltungen); umfangreiches Testing-Szenario wie von einem professionellen Softwarehaus; Ergebnis an einen Subagenten zur Verifikation geben
6. Reasoning Effort auf Ultracode stellen

**Weitere Stichpunkte aus den Notizen:**
- Hörbücher-Erklärung vom letzten Mal genutzt (DMS mit Mistral-OCR)
- Themen für 1. Juli: Remote Control, Ordnerwechsel über "cd", Kontextverhalten ab 300.000/500.000 Token, `/compact` oder `/clear`, Edge Functions (Telegram, Spracheingabe, monatliche Auswertung), Subagenten
- Merksatz: "Anwendung, Anwendung, Anwendung — ganz wichtig, sonst geht alles verloren"
- Aufgabe/Ziel der Session: Lernwebsite auf Architektur konzentrieren, insbesondere Edge Functions; Subagenten ausprobieren

**To-Do-Liste (Marvin):**
- [ ] Mailerinnerung für Fuhrparkmanager bauen (< 60 Tage-Alarm)
- [ ] Awareness-Testing-Workflow (Prompt-Kette unten) bei eigenen Projekten anwenden
- [ ] Architekturdiagramm des eigenen Projekts selbst zeichnen können (Hausaufgabe)
- [ ] Reasoning-Effort-Regler bewusst vor jedem Prompt einstellen

---

## 1. STATUS-RUNDE — WAS HAT DIE GRUPPE UMGESETZT?

### Fabian (Fabi)
- DMS-Hausaufgabe angegangen, aber hängengeblieben: Mistral kann keine PDFs, nur Bilder
- Ursache (im Gespräch geklärt): Es wurde das **Pixtral-Modell** (Bildanalyse) statt **Mistral OCR / OCR Latest** (echtes OCR-Modell) verwendet — Namensverwechslung, weil Mistral mehrere Modelle anbietet
- DMS ansonsten fertig: PDF-Upload funktioniert, Testdaten hochgeladen
- DMS lief bisher nur als reine HTML-Seite ohne Backend (kein Localhost/Programm) — wurde in der Session korrigiert (siehe Abschnitt 5)

### Andreas
- Kein expliziter Fortschrittsbericht in dieser Session (Fokus lag auf Fragen zu Cloud-MD-Struktur und Architektur); hat mehrere MD-Dateien angelegt: eine übergeordnete Struktur + je Projekt eine eigene, inkl. "Versuchsprojekte"

### Tobias
- War im Urlaub, wenig Zeit gehabt
- Hat trotzdem eine Wissensdatenbank für ein neues Programm ("Bautask") gebaut: HTML-Dashboard, passwortgeschützt, im Betrieb verteilt — reine Frage-Antwort/Schulungsvideo-Sammlung, **keine API-Aufrufe aus dem HTML heraus** (daher aktuell unkritisch bzgl. API-Key-Sicherheit)

### Marvin (ZFG)
- **Fuhrparkmanager:** Von Google Sheets erfolgreich auf SQL/Supabase umgestellt
- **Problem entdeckt:** Trotz Prompt "prüf nochmal alles auf Richtigkeit" hat Claude Fehler übersehen — neues Auto wurde im Frontend angezeigt, tauchte aber nicht in der SQL-Datenbank auf. Korrektur kostete ca. eine halbe Stunde und zwei Anläufe
- Dieses Erlebnis war der Auslöser für den Haupt-Coaching-Punkt der Session (Awareness-Testing, siehe Abschnitt 2)
- DMS mit Mistral-OCR ebenfalls fertiggestellt und funktionsfähig
- Hörbücher zu Inhalten der Vorwoche (u.a. MCP-Server) nachgehört, um Verständnis zu vertiefen

### Janine (neu/wieder dabei)
- War letzte Session nicht vollständig dabei
- Grundsatzdiskussion mit ihrem Mann: beide nutzen Claude, viele berufliche/private Überschneidungen (u.a. Geodaten/QGIS) → Frage, wie man ein gemeinsames System aufbaut, statt drei getrennte (privat, Arbeit, Partner)
- Sehr aktiv im Datenschutz-Exkurs (Abschnitt 6): eigene DSGVO-Bedenken bei GitHub/US-Servern, Frage nach AVV/DPA

---

## 2. HAUPTTHEMA: AWARENESS-TESTING — WARUM "PRÜF NOCHMAL ALLES" NICHT FUNKTIONIERT

### Das Problem
KI hat in der Regel kein Qualitätsproblem bei dem, was sie sich ansieht — sie findet und behebt Fehler dort zuverlässig. Das eigentliche Problem ist ein **Awareness-Problem**: Es gibt Stellen im Code/System, an die die KI schlicht nicht hinschaut. Der Prompt "Schau nochmal, ob alles in Ordnung ist" liefert der KI keine Anleitung, WOHIN sie schauen soll — deshalb bleibt der Fehler unentdeckt.

> Dieser Prompt ist verboten: **"Jetzt schau noch mal, ob alles in Ordnung ist und gut läuft."**

### Der empfohlene Workflow (6 Schritte)

**Schritt 1 — Nicht fragen:** "Jetzt schau noch mal, ob alles passt" (siehe oben, verboten)

**Schritt 2 — `/post`**
Vor Beginn der Testphase alles bisher Gebaute/Gelernte ins Wissensmanagement einbacken, damit kein Wissen verloren geht (idealerweise inkl. Kartografie/IT-Landkarte).

**Schritt 3 — `/compact`**
Danach das Kontextfenster verdichten: Claude soll "frisch im Kopf" sein (Kontext-Window leer), aber trotzdem noch wissen, worum es geht. Der Compact fasst alles auf ca. wenige tausend Token zusammen — ideal als Briefing für einen Tester, der frisch in seine Schicht kommt.

**Schritt 4 — Codebase-Analyse (reine Awareness-Herstellung)**

```
Führe jetzt nochmal eine Codebase-Analyse durch, in der du dir nochmal
jede Funktionalität auf den Schirm rufst, die es gibt. Dazu gehört:
jeder Datenspeicherort
jeder Datenfluss
jede Datenverarbeitung
jede User-Interaktion im Frontend (also alle Knöpfe, alle Eingabefenster,
alle Links, alles, was irgendwie testbar ist)
```

**Schritt 5 — Autonome Testung mittels Browser-Usage** (der zentrale Prompt der Session)

```
Autonome Testung mittels Browser-Usage von Frontend: Sämtliche
Funktionalitäten, die geklickt werden können oder getippt werden können,
müssen entweder über Chrome oder über Playwright komplett autonom
getestet werden. Außerdem müssen dann alle Konsequenzen gemessen werden:
Datenbank-Einträge, Weiterleitungen, Erwartungshaltungen, die man eben
einfach haben darf, wenn man im Frontend irgendetwas macht. Außerdem
müssen alle weiteren Features, die dieses Programm bzw. diese Anwendung,
die wir gemacht haben, hat, getestet werden. Erstelle ein umfangreiches
Testing-Szenario, wie es von einem professionellen Softwarehaus
erschaffen würde, um sowohl Datensicherheit als auch User Experience und
Datenflüsse komplett autonom durchzutesten. Teste das komplett autonom
durch, gib das Testing-Protokoll dann noch mal an einen Subagenten, um
zu überprüfen, ob wirklich alles gut gelaufen ist.
```

Wichtiges Funktionsprinzip: Claude öffnet dabei selbst einen Browser, klickt jeden möglichen Klick durch, prüft danach die Konsequenzen — z. B. bei einem Klick, der einen Datensatz anlegen soll, wird per MCP-Tool-Use direkt in Supabase nachgeschaut, ob der Datensatz wirklich angekommen ist. Zusätzlich liest Claude die Entwicklerkonsole des Browsers aus und erkennt darüber serverseitige oder frontendseitige Fehlermeldungen sofort — und behebt sie in der Regel direkt.

Das Tool-Use-Muster lautet also: **Browser Usage → MCP Supabase-Check → ggf. Fehlerbehebung.**

Diese Testung dauert länger (man kann "einen Kaffee trinken gehen"), ersetzt aber laut Marco Heer ca. 95 % des eigenen manuellen Testings.

**Schritt 6 — Reasoning Effort auf Ultracode stellen**
(siehe Abschnitt 3)

Wichtig: Diese Prompt-Kette soll man sich nicht einfach 1:1 abspeichern und blind wiederverwenden, sondern selbst nachprompten — das trainiert den Transfer auf eigene Situationen.

---

## 3. REASONING EFFORT & ULTRACODE — SUBAGENTEN-KONZEPT

Der Reasoning-Effort-Regler (Pfeiltasten unten links/rechts im neuen Interface) hat mehrere Stufen:

| Stufe | Verhalten |
|---|---|
| Niedrig | Für "Pümpelaufgaben" — schnelle, unwichtige Anfragen, Antwort oft in ca. 5 Sekunden |
| Mittel | Standard-Denkaufwand |
| Max | Denkt sehr lange nach (bis zu ca. 20 Minuten), sinnvoll bei komplexen Sachverhalten |
| **Ultracode** | Standardmäßig hoher Denkaufwand PLUS die Möglichkeit, dass Claude **Subagenten autonom ausschwärmen lässt** |

### Warum Subagenten?
Wenn Claude z. B. herausfinden soll, was überhaupt getestet werden muss (Codebase-Analyse), würde das im Hauptkontext viele Tokens verbrauchen, bevor man überhaupt beim eigentlichen Testen ankommt. Stattdessen delegiert Claude diese Aufgabe an Subagenten, die autonom arbeiten und nur ein knappes, verdichtetes Ergebnis zurückliefern.

> "Und das hat dann halt nur ein paar tausend Token gekostet statt ein paar hunderttausend." — Marco Heer (sinngemäß)

Dadurch kann Claude wie ein Koordinator/Vorarbeiter agieren: ein Subagent kümmert sich um Informationsbeschaffung, ein anderer um Testung usw. — im Team-Effort bessere Ergebnisse, kontextschonend.

Wichtiger technischer Hinweis: **Der Reasoning-Effort-Regler kann nur an der "Quelle" der eigentlichen Konversation geändert werden** — also nur direkt im Terminal/in der Session, die wirklich in der Claude-App (nicht als Remote-Control-Fernsteuerung) läuft. Solange eine Session über Remote Control aus der Ferne gesteuert wird, lässt sich der Regler in der Fernsteuerungs-Oberfläche nicht bedienen.

Praxisbeispiel: kleine Wartungsaufgabe (Session-Nummerierung auf der Coaching-Plattform war fehlerhaft) — Prompt-Muster für solche Aufgaben:

```
Hey, uns ist aufgefallen, dass in den Aufzeichnungen von Kohorte 3 im
Synclaro-Academy-Portal die Nummerierung irgendwie nicht passt. [...]
Ist auch gar nicht so wichtig. Finde bitte selbst raus, was das Problem
ist. Schildere ganz kurz und gib mir dann zur Absegnung deinen
Lösungsvorschlag. Dann segne ich es ab und dann darfst du es umsetzen.
```
→ Für solche Routine-/Pümpelaufgaben reicht ein niedriger bis mittlerer Reasoning Effort.

---

## 4. REMOTE CONTROL & DAS NEUE CLAUDE-INTERFACE

### Remote Control (RC)
- Befehl in der Session: `/RC` (oder einfach "RC" eintippen)
- Schaltet die aktuelle Claude-Code-Session auf "fernsteuerbar" — erkennbar an einem kleinen grünen Hinweis unten im Terminal
- Danach erscheint diese Session in jeder Claude-App (Desktop, Web, Handy), verknüpft über den eigenen Anthropic-Account
- Man kann die Session dann von jedem Gerät aus weitersteuern — der ursprüngliche Rechner, auf dem Claude läuft, **muss dabei durchgehend eingeschaltet bleiben** (Terminal offen, kein Screensaver/Auto-Logout, der den Zugriff blockiert)
- Praktischer Nutzen: Ortsunabhängigkeit — z. B. abends im Bett am Handy noch eine große Testaufgabe ("autonome Testung") über Nacht anstoßen, während der Rechner zuhause weiterläuft
- Empfehlung von Marco Heer: alle Sessions, die man potenziell später braucht, direkt auf RC schalten

### Das neue Claude-Interface (Cloud-/Claude-App) als Ersatz fürs Terminal
- Man kann komplett auf das klassische schwarze Terminal-Fenster verzichten und stattdessen die Claude-App (lokal installiert oder im Browser) nutzen
- Neue Sitzung direkt in der App starten: "Ordner öffnen" statt manuellem `cd` im Terminal
- Sobald eine Session so gestartet wird, ist es KEINE Remote-Control-Fernsteuerung mehr, sondern eine eigenständige, voll funktionsfähige Sitzung mit allen Fähigkeiten (inkl. einstellbarem Reasoning Effort)
- Bis zu 99 parallele Claude-Code-Sitzungen möglich; typisches "Chat-Multitasking" — verschiedene Chats für Programmieren, Automatisieren, einfache Arbeiten parallel
- Transkriptansicht einstellbar: "ausführlich" (zeigt jeden Diff/Arbeitsschritt) vs. "normal" (nur Frage/Antwort)
- Berechtigungsstufen (statt nur `--dangerously-skip-permissions`):

| Modus | Verhalten |
|---|---|
| Änderungen akzeptieren | Darf nichts neu anlegen, aber kleinere Änderungen ohne Rückfrage |
| Planmodus | Reines Schreibverbot, nur Planung — nützlich bei größeren Softwareprojekten für Vorab-Planung |
| Auto-Modus | Fast alles erlaubt, nur wirklich kritische Aktionen müssen abgesegnet werden — **von Marco Heer als Dauereinstellung empfohlen** |
| (weitere Stufe, bei manchen Nutzern ausgegraut, evtl. abostufenabhängig) | Alles ohne jede Genehmigung erlaubt — nutzt Marco Heer persönlich |

- Modellauswahl direkt im Interface (zum Zeitpunkt der Session: Sonnet 5 neu erschienen, Fable 5 angekündigt)
- Kontextfenster-Auslastung wird unten sichtbar angezeigt (wichtig zur Einschätzung, wann `/compact` oder `/clear` nötig wird)
- Kontingentnutzung des Abos ebenfalls einsehbar

---

## 5. CLAUDE.MD — GLOBALE VS. LOKALE PROJEKTDATEIEN

### Technischer Kernpunkt
Claude sucht bei Sessionstart **immer und ausschließlich** nach einer Datei mit exakt dem Namen `CLAUDE.md` (Groß-/Kleinschreibung/Variationen wie "Claudius.md" werden NICHT automatisch gelesen). Beim Start werden automatisch eingelesen:
1. Die globale `CLAUDE.md` (z. B. im Nutzerverzeichnis)
2. Alle lokalen `CLAUDE.md`-Dateien entlang des Pfades zum Projektordner (sofern vorhanden — liegt keine dort, wird auch nichts gelesen, das ist kein Fehler)

### Was gehört wohin?
- **Globale CLAUDE.md:** übergeordnete Regeln, die für ALLES gelten (Verhaltensregeln, allgemeine Prinzipien)
- **Lokale/projektspezifische CLAUDE.md:** spezielle Informationen nur für dieses eine Projekt (z. B. "hier liegt Supabase", DSGVO-Verweis für dieses konkrete Projekt)

### Marco Heers eigene globale CLAUDE.md als Vorbild (live gezeigt)
Enthält u. a.:
- **"Vier Prinzipien für jede technische Aufgabe"** (Konzept von "Karpathy" — gemeint ist vermutlich Andrej Karpathy, ehemals OpenAI):
  1. Annahmen offenlegen (gegen Halluzination)
  2. Bei Mehrdeutigkeit immer Optionen nennen
  3. Minimaler Code, der das Problem löst (KI tendiert dazu, mehr zu bauen als nötig)
  4. Bei Skript-Änderungen nur gezielt an der Stelle eingreifen, nicht das ganze Skript löschen/neu schreiben
- Umlaut-Anweisung (Ä, Ö, Ü korrekt verwenden)
- **Drei-Agenten-Architektur:** bei komplexeren Aufgaben automatisch einen Bauenden, einen ständig Kritisierenden und einen für externes Quality Assessment starten (uralte IT-Technik, jetzt durch Subagenten abgebildet)
- **Multi-Model-Cross-Check über OpenRouter:** Beim Programmieren lässt Marco Heer automatisch zusätzlich andere KIs mitschauen (genannt: GPT-5.4, Kimi K2.6, Qwen 3.6) — nicht nur ein einzelner Claude-Agent arbeitet, sondern ein ganzes Team verschiedener Modelle
- Vollständiges persönliches Knowledge-Management-Regelwerk (für die Gruppe noch "zu groß und komplex")
- Liste bevorzugter/abgelehnter KI-Modelle für bestimmte Zwecke
- Eigene Skills, z. B. eine Anweisung, dass Antworten per Sprachausgabe vorgelesen werden, wenn er sagt "sprich mit mir, ich kann gerade nicht lesen, sitze im Auto"
- Bildgenerierungs-Vorlieben als Inspiration

**Praxis-Hausaufgabe aus der Session:** Modell-Liste in der eigenen CLAUDE.md per Recherche-Auftrag aktualisieren lassen:
```
Bitte führe eine Recherche über alle KI-Modelle durch, vor allem diese
Liste mit den ganzen Anbietern. Da stehen einige veraltete Modelle drin.
Ich hätte gerne, dass das komplett upgedatet wird und auch im Rest der
Claude.md überall jeweils aufs neueste Modell umgestiegen wird.
```

### Empfehlung zu DSGVO-Hinweisen in der CLAUDE.md
DSGVO-Anweisungen NICHT in die globale CLAUDE.md schreiben, weil das den Fokus sprengt ("danach ist der ganze Fokus nur noch auf DSGVO und das Ding vergisst, ordentlich zu bauen"). Stattdessen: in die **lokale/projektspezifische** CLAUDE.md nur einen kurzen Verweis auf DSGVO aufnehmen. DSGVO ist an zwei Stellen relevant:
1. Bei der Architekturplanung (grobe Machbarkeitsprüfung)
2. Am Ende des Projekts als eigener Schritt "DSGVO-Adaption" — dafür einen eigenen Subagenten launchen, der das fertige Programm gegen die vollständige DSGVO-PDF prüft (nicht die ganze Zeit im Hauptkontext mitschleppen, sonst wird das Kontextfenster unnötig belastet)

```
Launch einen Subagenten. Das war alles, was wir hier gemacht haben,
DSGVO-kritisch beleuchten und sofort Bescheid geben, wie wir das zu tun
haben, damit es jetzt nicht nur technisch gut gedacht ist, sondern auch
DSGVO-technisch gut gedacht ist.
```

---

## 6. DATENSCHUTZ-EXKURS: DER ENTSCHEIDUNGSBAUM (PI, AVV, DPA)

Ausgelöst durch Janines Bedenken zu GitHub/US-Servern und Kundendaten.

### Grundbegriff PII
**PII = Personally Identifiable Information** — alles, was einen Rückschluss auf eine konkrete Person zulässt (Name, Geburtsdatum, Ausweisnummer usw.). Generische Zusatzinfos (z. B. Lieblingsessen, Kundennummer) sind für sich genommen unproblematisch, solange sie nicht mit identifizierenden Daten verknüpft sind.

### Die zwei relevanten Vertragswerke
| Kürzel | Bedeutung | Regelt |
|---|---|---|
| **AVV** | Auftragsverarbeitungsvertrag | Speicherung von Daten |
| **DPA** | Data Privacy Agreement | Verarbeitung von Daten |

Beide sind bei seriösen Anbietern meist direkt im Portal/Dashboard abrufbar und unterschreibbar (z. B. bei Supabase). Wichtig: **Sobald Daten in den USA gespeichert/verarbeitet werden, wird die Wirksamkeit eines AVV nach aktueller DSGVO-Linie faktisch ausgehebelt** — im Streitfall wird oft so behandelt, als hätte es den AVV nicht gegeben.

### Der Entscheidungsbaum (vereinfacht)
1. **Dürfen wir die Daten so verarbeiten/speichern?**
   - Ja → weitermachen
   - Nein → weiter zu 2.
2. **Können wir AVV/DPA (oder Sonstiges) abschließen, um es zu dürfen?**
   - Ja, jetzt dürfen wir → weitermachen (Ausnahmen: z. B. Gesundheitsdaten, bei denen selbst AVV/DPA oft nicht reicht)
   - Immer noch nein → weiter zu 3.
3. **Verarbeitung/Speicherung auf konforme Lösung umstellen:**
   - Lokal hosten (z. B. lokal gehostete Supabase-Instanz, lokal laufendes KI-Modell/OCR)
   - Alternativ: Datensatz vorher bereinigen (Anonymisierung/Pseudonymisierung — identifizierende Merkmale wie Name/Ausweisnummer entfernen, unkritische Restdaten wie Geburtsdatum/Kundennummer behalten)
   - Alternativ: Proxy-Modell einsetzen — ein lokales Modell prüft jeden Prompt vorab auf sensible Informationen; unkritische Prompts gehen an die öffentliche/US-KI (z. B. Anthropic), kritische werden lokal verarbeitet

### Praktische Konsequenzen für die Gruppe
- Beim Bauen von Software/Programmieren an sich entstehen noch keine Datenschutzprobleme — relevant wird es erst, sobald echte (Kunden-)Daten eingespeist werden
- Für rein private Nutzung/Testdaten (eigene Daten) spielt DSGVO praktisch keine Rolle ("das sind eure Daten, damit dürft ihr machen, was ihr wollt")
- Bei Firmeneinsatz für eigene Mitarbeiter: beginnt Relevanz
- Bei Verkauf an Dritte: deutlich kritischer (dafür ist diese Ausbildung laut Marco Heer explizit nicht ausgelegt)
- Mistral ist EU-ansässig → sobald ein AVV mit Mistral besteht, ist die OCR-Verarbeitung weitgehend datenschutzkonform nutzbar
- Anonymisierte Nutzungsstatistiken (z. B. Website-Klicks ohne IP/Namen-Speicherung) sind unproblematisch — deshalb gibt es Cookie-Banner nur, wenn IP-Adressen (rückführbar auf ein Gerät/eine Person) gespeichert werden
- Empfehlung zur Priorisierung: technischen Aufwand und Datenschutz-Aufwand jeweils einschätzen → daraus Priorisierungsreihenfolge für Features ableiten
- Ergänzender Hinweis: Bei Verwendung personenbezogener Daten sollte in den eigenen AGBs/Kooperationsverträgen eine passende Klausel stehen (z. B. "Zu Qualitätszwecken werden Ihre persönlichen Daten hausintern nur zu diesen Zwecken verarbeitet, gespeichert und von lokal betriebener KI verarbeitet") — Marco Heer betont ausdrücklich, keine Rechtsberatung zu leisten, sondern nur technisches Grundverständnis zu vermitteln

### API-Keys niemals im HTML/Frontend
Sobald ein HTML-Frontend direkt eine KI/API anspricht, muss der API-Key irgendwo im Code hinterlegt werden — wird das HTML weitergegeben, "fliegt der Schlüssel mit durch die Gegend". Lösung: API-Calls nicht aus dem HTML/Frontend heraus, sondern über eine **Edge Function** (Backend) ausführen, wo der Schlüssel serverseitig verschlüsselt hinterlegt ist. Alternativ: Umgebungsvariablen nutzen. Empfehlung an die Teilnehmer: Es reicht zu wissen, DASS es dieses Sicherheitsthema gibt — die technische Umsetzung liefert Claude, wenn man es explizit danach fragt ("Marco hat gemeint, HTML mit API-Schlüssel einfach rumreichen ist nicht gut, wie macht man das elegant?").

---

## 7. VON HTML-SEITE ZU RICHTIGEM PROGRAMM: FRONTEND VS. BACKEND

Anhand von Fabians DMS demonstriert: Eine reine HTML-Datei (erkennbar an der URL-Zeile, die eine lokale Datei zeigt) ist ein **reines Frontend** — Eingaben werden meist nur lokal im Browser gespeichert, es gibt keine Kollaboration/Mehrgerätenutzung. Für ein "richtiges", produktives Programm braucht es immer **Frontend UND Backend**, gehostet auf einem Port (Localhost als Zwischenschritt, später live).

Praxis-Prompt für den Umbau (an Fabian gegeben):

```
Wir möchten das Ganze gerne jetzt zu einem ordentlichen Programm umbauen.
Würdest du dafür bitte einmal zunächst ein auf Localhost gehostetes
Programm daraus machen? Mach gerne eine Sicherheitskopie des Programms
vorher (idealerweise über Versionskontrolle/GitHub für Disaster Recovery).
```

Danach: neue Session in einem definierten Projektordner starten, mit Einstiegs-Prompt:

```
Wir arbeiten an einem Dokumentenmanagement-System, kurz DMS. Ich lege dir
die HTML bei, an der du gut rausfinden solltest, was wir bisher gebaut
haben. Wichtig ist für mich auch, dass du einmal kurz eine Analyse machst
und genau siehst, was an Datenbankstruktur da ist, wie das Programm bis
jetzt funktioniert und so weiter.
```

**Warum immer in einem bestimmten Ordner starten?** Zwei Gründe wurden gemeinsam erarbeitet:
1. Sonst wird Claude mit Informationen überhäuft und verliert grundlegenden Kontext
2. Nur im richtigen Ordner werden automatisch die relevanten CLAUDE.md-Dateien eingelesen (globale + lokale)

---

## 8. VOLLSTÄNDIGE DMS-ARCHITEKTUR (gemeinsam am iPad/Whiteboard erarbeitet)

Ziel der Übung: Die Teilnehmer sollen ihre Architektur selbst erklären können ("Ziel dieses Coachings muss es sein, dass ihr diese Architekturdiagramme selber zeichnen könntet").

### Die Bausteine und ihre Reihenfolge

```
1. PROGRAMMIERER: Claude Code
   → programmiert das Frontend UND richtet die Datenbank ein

2. FRONTEND: HTML-Anwendung, gehostet z.B. über Netlify
   → zeigt Daten an, die aus Supabase gezogen werden
   → Drag & Drop-Fenster für Dokumente

3. Beim Drag & Drop: Datei landet NICHT direkt in der Datenbank,
   sondern im DATEISPEICHER (Supabase Storage)
   → neue Datei im Speicher triggert eine EDGE FUNCTION

4. EDGE FUNCTION (liegt bei Supabase, ist im Grunde ein Skript/Codebasis):
   Schritt 1 — OCR: Datei wird an Mistral OCR (OCR Latest, NICHT Pixtral!)
               geschickt → OCR liefert Rohtext zurück
   Schritt 2 — DSGVO-Prüfung: Enthält der Text sensible Daten?
               → einfache Programmversion: "nein, mache ich nicht"
               → komplexere Version: an DSGVO-konforme Verarbeitung routen
   Schritt 3 — Kategorisierung: KI-Aufruf (z.B. OpenAI, oder
               datenschutzkonformer: Mistral AI-Modelle oder
               Microsoft Azure/OpenAI als Enterprise-Lösung)
               → erkennt Dokumenttyp (Rechnung, Angebot, Lieferschein...)
   Schritt 4 — Handlungsbedarf auslösen (Beispiel Marco Heer):
               Rechnung < 50 € → Plausibilitätscheck, automatische Zahlung
               Rechnung > 50 € → geht an Telegram-Bot zur Freigabe,
                                   danach automatische Zahlung

5. Edge Function schreibt Ergebnis zurück in die DATENBANK (Supabase):
   Dokument, Kategorie, OCR-Text, Typ, etc.

6. CLAUDE ↔ SUPABASE: über MCP-Server (pro Projekt einmalig eingerichtet)
   kann Claude direkt in die Datenbank lesen/schreiben, ohne dass der
   Mensch manuell etwas kopieren muss

7. Optional: Edge Function kann auch einen API-Call an TELEGRAM auslösen
   Beispiel "Monatliche Auswertung an Marvin senden"-Knopf:
   Knopf → Edge Function → KI-Aufruf über API (KI erhält relevante Daten
   + Dateien aus Supabase per Prompt mitgeliefert) → KI liefert Auswertung
   zurück an Edge Function → Edge Function schickt Ergebnis an Telegram-Kanal
```

### Wichtige Klarstellung zu Edge Functions
Eine Edge Function ist kein fertiges Produkt eines Anbieters, sondern **selbst geschriebener Code** (vergleichbar mit einem Python-/JavaScript-Skript), der bei Supabase gehostet wird. Man lässt sich den Code von Claude schreiben ("Du schreibst eine Edge Function. Im Rahmen dieser Edge Function soll Mistral OCR über API angesprochen werden... dann soll OpenAI angesprochen werden...") — Claude programmiert die nötigen API-Calls direkt hinein. Eine Edge Function kann beliebig viele Anweisungen nacheinander enthalten und auch andere Edge Functions aufrufen (sauberere Trennung der Zuständigkeiten).

**Vorteil, Edge Functions bei Supabase statt lokal zu hosten:** Sie liegen direkt dort, wo die Daten sind, sind unabhängig von der eigenen Hardware und unterliegen zugleich dem mit Supabase geschlossenen AVV.

### Vibe-Coding vs. professionelle Architektur
> "Datenspeicherung hat in einer Datenbank zu erfolgen, Dateispeicherung hat in einem Dateispeicher zu erfolgen. [...] KI-Calls haben nicht aus dem HTML heraus zu erfolgen, sondern aus einer Edge Function heraus. Dann ist es nämlich ortsunabhängig sicher [...]. Das ist der Unterschied zwischen Vibe-Coding und professionalisierter Architektur." — Marco Heer (sinngemäß)

Die Teilnehmer sollen bei Abweichungen von diesem Muster (z. B. wenn Claude vorschlägt, Dateien einfach in einen Desktop-Ordner zu speichern) sofort "Alarmglocken" hören und gegensteuern.

---

## 9. AUSBLICK — NÄCHSTE THEMEN

- **RAG / Vektordatenbanken:** Für sehr große Dateimengen (z. B. komplette DSGVO als PDF, große Dokumentenmengen im DMS) reicht es nicht, dass Claude bei jeder Anfrage alles komplett neu durchliest (Gefahr des Übersehens). RAG (Retrieval-Augmented Generation, Synonym Vektordatenbank) macht große Dateimengen performant durchsuchbar. Wird als "wahrscheinlich das Komplexeste, was ich euch jemals beibringen werde" angekündigt — Detailverständnis optional, wichtig ist die Anwendung.
- **Andere KI-Modelle neben Anthropic** als Critic/Qualitätsprüfer einsetzen (siehe Multi-Model-Cross-Check in Marco Heers CLAUDE.md, Abschnitt 5)
- **Subagenten im Detail** (bisher nur angerissen)
- Marco Heer erwägt eine Pause oder den Wechsel zu individueller **Umsetzungsbegleitung** statt wöchentlicher Gruppensessions, da die Themen inzwischen so komplex sind, dass ohne ausreichend Übungszeit zwischen den Sessions kein weiterer Wissenszuwachs mehr sinnvoll ist ("jedes Hinzufügen ist nur schädlich, solange das bisherige nicht sitzt"). Entscheidung wird in der Folgewoche mit der Gruppe abgestimmt.
- Hausaufgabe: eigenes Architekturdiagramm (Bausteine: Frontend, Backend/Edge Functions, Datenbank, Dateispeicher, externe Dienste) selbst zeichnen bzw. anhand des in der Session gezeigten Screenshots ("Architekturübung") nacharbeiten.

---

## KERNAUSSAGEN DER SESSION

> **"KI hat nicht das Problem, dass das, was sie auf dem Schirm hat, irgendwie schlecht gebaut ist. KI hat das Problem, dass irgendwo Fehlerchen sind, wo sie gar nicht erst hingeguckt hat. Hätte sie hingeguckt, hätte sie den Fehler entdeckt und behoben. [...] Das ist ein Awareness-Problem."** — Marco Heer

> **"Diese ganze Testung, die ihr sonst eigentlich mit Klicken und Machen tun müsstet, kann man von KI abverlangen. Dauert halt ein Weilchen länger, dann geht ihr halt einen Kaffee trinken."** — Marco Heer

> **"Ultracode bedeutet, dass standardmäßig auf hoch gestellt wird, aber dass die Möglichkeit besteht, Subagenten autonom ausschwärmen zu lassen."** — Marco Heer

> **"Ich bediene das Reasoning-Effort-Ding ungefähr so viel wie die Kupplung beim Autofahren."** — Marco Heer

> **"Datenspeicherung hat in einer Datenbank zu erfolgen, Dateispeicherung hat in einem Dateispeicher zu erfolgen. KI-Calls haben nicht aus dem HTML raus zu erfolgen, sondern aus einer Edge Function heraus. Das ist der Unterschied zwischen Vibe-Coding und professionalisierter Architektur."** — Marco Heer

> **"Wenn ihr wollt. Wenn ihr noch nie ein Lego-Haus gebaut habt, werdet ihr davon keine Ahnung haben. Das ist einfach so."** — Marco Heer (zur Notwendigkeit von Anwendung statt reiner Theorie)

> **"Ohne Anwendung müssen wir das jede drei Wochen wiederholen und dann geht es wieder verloren. [...] Das geht nur mit anderen [Üben]."** — Marco Heer

> **"Im programmierten Code haben Variablen niemals irgendwas verloren. [...] Keys sind eben schon Variablen — auf dem Computer, auf dem du ausgeführt wirst, liegt irgendwo verschlüsselt eine Variable. Das geht dann schon."** — Marco Heer

---

## WICHTIGE WERKZEUGE

| Werkzeug | Zweck |
|---|---|
| `/post` | Wissensstand vor Testphase sichern (Wissensmanagement) |
| `/compact` | Kontextfenster verdichten, Claude "frisch" für Testphase machen |
| `/clear` | Kontext vollständig zurücksetzen |
| Reasoning-Effort-Regler (niedrig/mittel/Max/Ultracode) | Denkaufwand pro Prompt einstellen |
| Ultracode | Höchste Stufe inkl. autonomem Subagenten-Ausschwärmen |
| Subagenten | Kontextschonende, autonome Delegation von Teilaufgaben (Analyse, Testung, DSGVO-Check) |
| Browser-Usage (Chrome-Steuerung / Playwright) | Autonomes End-to-End-Testen des Frontends durch Claude |
| MCP-Server (Supabase) | Direktzugriff von Claude auf Datenbank zur Verifikation von Testergebnissen |
| Remote Control (`/RC`) | Session ortsunabhängig fernsteuerbar machen (Handy, anderer Rechner) |
| Claude-App (statt Terminal) | Neues Interface: Sitzungen starten, Reasoning Effort einstellen, Berechtigungsstufen wählen, Kontextauslastung sehen |
| Mistral OCR / OCR Latest | Echtes Dokumenten-OCR-Modell (Achtung: nicht mit Pixtral verwechseln!) |
| Pixtral | Bilderkennungsmodell von Mistral — KEIN OCR, erkennt nur PNG/JPG |
| Edge Functions (Supabase) | Backend-Logik/API-Orchestrierung, Ort für sichere API-Key-Nutzung |
| AVV (Auftragsverarbeitungsvertrag) | Vertragliche Grundlage für Datenspeicherung |
| DPA (Data Privacy Agreement) | Vertragliche Grundlage für Datenverarbeitung |
| CLAUDE.md (global/lokal) | Systemanweisungen, die Claude automatisch bei Sessionstart einliest |
| OpenRouter | Zugang zu mehreren KI-Modellen (Cross-Check/Multi-Model-Ansatz) |
| RAG / Vektordatenbank (angekündigt) | Performantes Durchsuchen sehr großer Dokumentmengen |

---

*Aufbereitet aus dem Transkript der Session vom 1. Juli 2026 | Synclaro KI-Gruppencoaching*
