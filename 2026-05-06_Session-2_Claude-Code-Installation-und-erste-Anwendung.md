# Synclaro KI-Coaching — Session 2: Claude Code — Installation und erste Anwendung
**Datum:** Mittwoch, 6. Mai 2026
**Format:** Online-Gruppencoaching (Video-Call)
**Coach:** Marco Heer (Synclaro)
**Dauer:** 124 Minuten
**Quelle:** AssemblyAI-Transkript (de, Speaker Labels)

---

## Sprecherzuordnung (aus Kontext abgeleitet)

| Kürzel | Person | Hinweise aus Transkript |
|---|---|---|
| **Speaker A** | Marco Heer (Coach) | Hauptsprecher, gibt alle Anweisungen |
| **Speaker B** | Marvin (ZFG/HWK) | Erwähnt Schachdatenbanken, Windows-10-Problem |
| **Speaker C** | Marco (Fortsetzung) | Transkriptions-Artefakt, gehört oft zu Speaker A |
| **Speaker D** | Tobias | „Mein Englisch ist wirklich eine Katastrophe", Firmenrechner |
| **Speaker E** | Andreas | Bautagebücher/Bautagesberichte, zwei Bildschirme |
| **Speaker F** | Fabian | Kein zweiter Bildschirm, fragt nach Outlook |

---

## Rückblick: Hausaufgaben aus Session 1

### Whisper Flow
- **Andreas:** Angetestet, funktioniert gut, aber noch ungewohnt frei zu diktieren
- **Tobias:** Wegen Englisch-Oberfläche nicht genutzt; hat Protokoll-Funktion von ChatGPT-Spracheingabe genutzt (5 Seiten Notizen → Protokoll in 10 Minuten)
- **Fabian:** Flow installiert, nutzt es für WhatsApp/E-Mails; noch befremdlich als „Schreiber"
- **Marvin:** Wird heute noch gelöst (Kopier-Problem in Eingabeaufforderung)

### Claude AI / erste KI-Nutzung
- **Andreas:** Bautagebücher via Excel-Tabelle schreiben lassen → sehr gut funktioniert
- **Tobias:** Weiter mit ChatGPT, aber: theoretisches Wissen aus Session 1 hat Ergebnisse deutlich verbessert

> **Marco dazu:**
> „Selbst wenn man nur die erste Stunde mitnimmt, die sehr theorielastig war, hilft das beim Autofahren: Man kennt die Ursache, wenn es nicht läuft, und kann an seinem Verhalten arbeiten."

---

## Themenblock 1 — Wichtiger Tipp: Recherche bei veralteten Infos

### Problem (von Tobias/Janine beschrieben):
KI nennt Buttons oder Einstellungen, die es in einem Programm gar nicht gibt.

### Erklärung (Janines Antwort, bestätigt von Marco):
> „Das liegt daran, dass das Programm nicht bekannt ist — oder sich seit dem Training verändert hat."

### Marco's Lösung:
> „Immer recherchieren lassen. Sag ihm: Hier ist ein Screenshot von Whisper Flow, ich suche die Einstellung für Deutsch. Bedenke: Es ist der 6. Mai 2026. Recherchier mal kurz."

Das Modell wurde zu einem bestimmten Zeitpunkt trainiert — es ist wie ein Mensch, den man 2024 in den Keller gesperrt und jetzt wieder rausgelassen hat. Intelligent wie eh und je, aber die letzten zwei Jahre fehlen.

**Standard-Vorgehen bei verändernden Oberflächen/Dashboards:**
1. Screenshot machen (Windows: `Win + Shift + S`)
2. In die KI einfügen
3. Sagen: Hilf mir, hier ist was ich suche — und bitte recherchier, ob sich was geändert hat

### ✅ Learning
- KI hat einen Trainingsstichtag — bei Software-Fragen immer recherchieren lassen
- Das Datum im Prompt mitnennen hilft der KI, frische Infos zu suchen
- `Win + Shift + S` = Windows-Snipping-Tool für Screenshots → direkt in Zwischenablage

---

## Themenblock 2 — Prompt-Qualität: Was wirklich zählt

> **Marco:**
> „90 Prozent der Qualität hängt von der Vollständigkeit des Prompts ab. Nur 10 Prozent von der Ordnung innerhalb des Prompts."

**Was das bedeutet für Whisper Flow / Diktat:**
- Einfach drauf losreden, auch wenn man sich verhaspelt, korrigiert oder Pausen macht
- KI hat damit kein Problem — sie versteht trotzdem
- Perfekte Formulierung ist weniger wichtig als vollständige Information

> „Dann irgendwann übt man das und merkt, OK, ich habe so ein bisschen eine Ordnung in meinen Prompts angewöhnt. Aber gelernt wird es nur durch reinballern."

### ✅ Learning
- Reihenfolge im Prompt fast egal; Vollständigkeit entscheidend
- Whisper Flow: Einfach losreden, alles raus, nicht perfektionieren

---

## Themenblock 3 — Claude Code: Was ist das?

### Der Unterschied zur normalen Claude-App

| | Claude AI (App / claude.ai) | Claude Code |
|---|---|---|
| Was es ist | Chat-Interface für das Modell | Harness + Modell auf dem eigenen Computer |
| Metapher | Fiat Punto zum Einkaufen | Rennstreckenauto |
| Werkzeuge | Sehr begrenzt (nur im Browser) | Voller Zugriff auf Dateien, Terminal, Netzwerk |
| Stärke | Schnell Fragen stellen | Dinge TUN — Dateien erstellen, lesen, Programme ausführen |

> „Das hier ist der Rennwagen, der kann alles. Ihr sitzt jetzt darin."

### Was Claude Code technisch ist:
- Ein **Harness** (Rüstung/Anzug), der auf eurem Computer läuft
- Die KI läuft **innerhalb** dieser Rüstung
- Der Harness stellt der KI **Werkzeuge** zur Verfügung: Dateien lesen, Dateien schreiben, Terminal-Befehle ausführen, Netzwerk durchmessen, Programme öffnen, Websites lesen...
- Claude Code läuft in der **Eingabeaufforderung / Terminal** (CMD) — dem schwarzen Fenster

> „Wir haben jetzt eine KI innerhalb dieser Eingabeaufforderung installiert. Damit kann die KI Befehle ausführen — und das sind sehr viele Befehle."

### Warum die Eingabeaufforderung?
- Überbleibsel aus DOS-Zeiten (vor grafischen Oberflächen)
- KI kann leichter Befehle ausführen als Maus-Klicks simulieren
- Sehr mächtig: Fast alles, was man per Maus macht, geht auch als Befehl

### ✅ Learning
- Claude Code ≠ Claude App — es ist ein komplett anderes Werkzeug
- Harness = der Anzug, der dem Modell Werkzeuge gibt
- Die Eingabeaufforderung ist hässlich, aber die Basis für alles

---

## Themenblock 4 — Installation von Claude Code (Schritt für Schritt)

### Voraussetzungen:
- Windows-Rechner
- Claude Pro Abo (mind. 18–20 €/Monat bei Anthropic)
- Internetverbindung

### Installationsprozess (wie durchgeführt):

1. **Browser öffnen** → Google: „Claude Code Windows Installation"
   → Erste Suchergebnis-Seite öffnen (offizielle Anthropic-Dokumentation)

2. **Befehl kopieren** (Windows CMD-Version)
   → Kopier-Button neben dem Befehl drücken

3. **Eingabeaufforderung öffnen**
   → Windows-Suche: „Eingabeaufforderung" eingeben → öffnen
   → Synonyme: Terminal, CMD — alles dasselbe

4. **Befehl einfügen und ausführen**
   → Rechtsklick → Einfügen (oder Strg+V in neueren Windows-Versionen)
   → Enter drücken → kann 2–3 Minuten dauern
   → Bei Fehlermeldung: Fehlermeldung zu Claude AI kopieren und fragen lassen

5. **Umgebungsvariable setzen**
   → Nach Installation erscheint ein „Setup Note"
   → Zu Claude AI gehen: „Gib mir das bitte als CMD-Befehl"
   → Befehl in Eingabeaufforderung einfügen → Enter

6. **Eingabeaufforderung neu starten**
   → Schließen und neu öffnen → damit Änderungen wirksam werden

7. **Claude Code starten**
   → `claude` eintippen → Enter

8. **Mit Claude-Konto verbinden**
   → Option 1 wählen (Subscription/Abo)
   → Browser öffnet sich → Verbindung bestätigen
   → Zurück in Eingabeaufforderung → Enter

> **Wenn etwas nicht klappt:** Fehlermeldung kopieren → zu Claude AI → „Ich will Claude Code installieren, kriege diesen Fehler, was soll ich machen?"

### ✅ Learning
- Bei KI-Installationsproblemen: immer die KI selbst um Hilfe bitten
- KI erklärt den nächsten Schritt — man muss nicht alles verstehen, nur ausführen
- Das ist „Hilfe zur Selbsthilfe" — Claude Code hilft bei der eigenen Installation

---

## Themenblock 5 — Erste Schritte in Claude Code: Tool-Nutzung verstehen

### Grundanzeige verstehen:

| Zeichen | Bedeutung |
|---|---|
| **Weißer Punkt** ● | Nachricht der KI an dich — das willst du lesen |
| **Grüner Punkt** ● | Tool-Aufruf — die KI hat ein Werkzeug benutzt |
| `Strg + O` | Erweiterte Ansicht: zeigt genaue Tool-Details und Ergebnisse |
| `Strg + O` nochmal | Zurück zur normalen Ansicht |
| `Escape` | Aktuelle Aktion abbrechen / Warteschlange unterbrechen |

### Demo 1: Dateien auf dem Desktop anzeigen

**Prompt:** „Welche Dateien liegen auf meinem Desktop?"

**Was passiert (intern):**
1. KI erkennt: Ich brauche ein Werkzeug → ruft `search` auf
2. Harness führt die Suche aus: `C:\Users\[Name]\Desktop\*`
3. Suchergebnisse gehen zurück in das **Context Window** der KI
4. KI antwortet auf Basis dieser Informationen

> „Der Harness hat der KI die Information zugeliefert. Das ist Kontext Engineering."

### Demo 2: Netzwerk durchmessen (Janines Rechner)

**Prompt:** „Miss mal das Netzwerk durch und prüfe die Geschwindigkeit."

**Was passiert:**
- KI ruft mehrere Terminal-Befehle auf: `GetNetAdapter`, Ping-Tests, etc.
- Manche werden durch Sicherheitsrichtlinien blockiert (Cisco AnyConnect)
- Ergebnis: Netzwerkinfo, installierte Adapter, Speed-Test teilweise blockiert

> „Wenn unser Internet langsam ist, sage ich: Miss mal durch, was ist da los? Und dann antwortet Claude: Schau mal, da ist was und da ist was."

> „Das ist wie wenn unser IT-Dienstleister ins Haus kommt und das Netzwerk durchmisst. Claude kann das auch — manchmal sogar besser."

### ✅ Learning
- Claude Code kann Dinge TUN — nicht nur antworten
- Jeder grüne Punkt = ein Werkzeug wurde eingesetzt
- Mit `Strg+O` kann man nachschauen, was genau gemacht wurde
- Das ist der Übergang von „KI als Sparringspartner" zu „KI als ITler"

---

## Themenblock 6 — Praxis: Coaching-Ordner anlegen und Transkript speichern

### Was gemacht wurde (Andreas / alle):

**Schritt 1: Ordner anlegen**

Prompt (diktiert):
> „Ich möchte mit Hilfe von KI Wissen speichern, das ich im Rahmen eines Gruppen-Coachings bei Synclaro akquiriere. Bitte lege auf meinem Desktop einen Ordner namens Coaching an. Dort werden wir künftig alle Transkripte ablegen."

→ Claude legt Ordner an (Tool: `write`/`mkdir`)
→ Muss einmal bestätigt werden

**Schritt 2: Transkript einfügen**

- Portal öffnen → Aufzeichnungen → Transkript kopieren
- Zu Claude Code → „Hier ist das erste Transkript, bitte speicher es in einem Unterordner"
- Text einfügen → Enter → Claude schreibt Datei

> „Wenn eine KI weiß, wie man programmiert, Dateien lesen und schreiben kann — dann haben wir alles, was wir brauchen, um ab jetzt programmieren zu lassen."

### ✅ Learning
- Claude Code kann Ordner und Dateien auf dem eigenen Rechner erstellen
- Transkripte lokal speichern = Wissensbasis für spätere Abfragen
- Das Ziel: KI hat alle Informationen auf dem Rechner → kann Wissen dauerhaft nutzen

---

## Themenblock 7 — HTML-Datei aus Transkript erstellen

### Was ist HTML?
> „HTML ist die Sprache der Webseiten. Bis jetzt ist es nur eine Datei, die der Browser anzeigt — noch keine Seite im Web. Aber es ist der erste Schritt in Richtung Website-Entwicklung."

### Was gemacht wurde (Janine):

**Prompt (via Whisper Flow diktiert):**
> „Die KI soll mir aus der TXT-Datei mit der Zusammenfassung von der ersten Coaching-Einheit eine HTML-Seite erstellen, die möglichst schön ist und mir hilft, das gesamte Wissen vom letzten Mal noch mal durchzugehen und die wichtigsten Punkte abzuarbeiten."

**Ergebnis:**
1. Claude erstellt HTML-Datei im Coaching-Ordner (Unterordner)
2. Browser öffnet die Datei und rendert sie schön
3. Auf Wunsch: Claude überarbeitet Design (mehr Farben, Verläufe, 2025-Design)
4. Klickbare Navigation, strukturierter Lernstoff

> „Wer smart arbeiten will, lässt sich eine HTML bauen. Viel besser als eine zweistündige Aufzeichnung nochmal anzuschauen."

### Technischer Ablauf (grün/rot im Tool-View):
- Grüne Linien = hinzugefügter Code
- Rote Linien = entfernter Code
- 944 Zeilen hinzugefügt, 928 entfernt (Redesign)

> „Das interessiert den Geschäftsführer oder Anwender weniger — das interessiert den Programmierer. Wir interessieren uns für das Ergebnis."

### ✅ Learning
- HTML ist einfach Text mit Struktur-Tags — der Browser macht das Schöne draus
- Claude Code kann HTML-Dateien generieren und verändern, ohne dass wir HTML kennen müssen
- Das ist der erste Schritt zu eigenem Website-Bau mit KI

---

## Themenblock 8 — Website-Analyse und Neugestaltung (Demo Mirco Mold)

### Prompt (von Marco diktiert, Vorlage für alle):
> „Vielen Dank, lieber Claude. Ich habe einen zweiten Wunsch. Gefällt mir die Website von unserer Firma nicht so gut. [Firmenname] heißt unsere Firma. Würdest du bitte mal recherchieren und dir unsere Seite anschauen? Versteh mal, was da für Inhalte drauf sind, wie die aussieht, was da für Bilder sind. Und starte einen ersten Versuch, die Startseite hübscher darzustellen, als unsere eigene Firma das bisher macht. Überleg dir, was diese Webseite alt macht. Wo sind Best Practices 2026, die diese Seite nicht eingehalten hat? Nutze auch gern ein Tool, das Bilder generieren kann. Ich verlange, dass du recherchierst, die Firma verstehst und wirklich dir Gedanken machst. Ich erwarte Exzellenz von dir."

**Was Claude macht:**
1. Tool `fetch` → liest Website aus
2. Analysiert Inhalte, Design, Struktur
3. Generiert neue HTML-Startseite
4. Öffnet Ergebnis im Browser

**Ergebnis:** Erster Entwurf in ~4 Minuten — ohne Bilder, aber inhaltlich korrekt

> „Ein Mensch hätte hier trotzdem wahrscheinlich drei, vier Stunden dran gesessen. Mindestens. Claude hat es in vier Minuten gemacht."

### ✅ Learning
- `fetch` ist ein Tool, mit dem Claude Websites lesen kann
- KI kann Websites analysieren und neu gestalten — als Startpunkt für echte Weiterentwicklung
- Der erste Entwurf ist noch nicht perfekt — aber der Prozess (Feedbackschleife) macht ihn besser

---

## Themenblock 9 — Context Window und Auto-Compacting

### Was ist das Context Window?

Befehl in Claude Code: `/context` → zeigt grafisch die Befüllung des Context Windows

**Was man sieht:**
- **Graue Kästchen** = System Prompts (Anbieter + Harness + eigene)
- **Lila Kästchen** = bisherige Nachrichten (User + Claude)
- **Token-Anzeige**: z.B. „X von Y Tokens verbraucht"
- **Aktuelles Modell**: Sonnet 4.6 (= claude-sonnet-4-6)

### Was passiert, wenn das Context Window voll ist?

| ChatGPT | Claude Code |
|---|---|
| Schneidet still ab — User weiß es nicht | Compact: schreibt automatisch eine Zusammenfassung |
| Alles vor dem Limit wird ignoriert | Neues, sauberes Kontext-Fenster wird geöffnet |
| Führt zu „Vergessen" mitten im Chat | Zusammenfassung wird als Startpunkt eingefügt |

**Der Prozess heißt: Compacting**
> „Da steht dann: Compacting, please wait. Dann wisst ihr: der schreibt jetzt kurz eine Zusammenfassung, öffnet einen neuen Chat, da kommt die Zusammenfassung rein — und dann geht es weiter."

### Nutzungslimits beim 20€-Abo:
- 5-Stunden-Kontingent (rollt alle 5 Stunden zurück)
- Plus Wochenlimit
- Bei professioneller Nutzung: 100€ oder 200€ Abo empfohlen

> „Wenn ihr mit dem Teil ernsthaft Arbeit verrichtet und sagt, jetzt machen wir wirklich professionelles Zeug — dann habe ich nicht die Muse zu warten. Dann geht man auf das größere Abo."

### ✅ Learning
- Claude vergisst nicht absichtlich — es ist das Context Window
- Auto-Compacting = Claudes Lösung, um mit dem Limit umzugehen
- `/context` = Kontrollbefehl, der Harness zeigt Befüllung an

---

## Themenblock 10 — Wichtige Befehle und Steuerung

### Slash-Befehle (gehen an den Harness, nicht an die KI):

| Befehl | Funktion |
|---|---|
| `/context` | Zeigt Context Window Befüllung grafisch |
| `/usage` | Zeigt verbleibende Nutzungslimits |
| Alle Slash-Befehle | Steuern den Harness, nicht den Transformer |

> „Alles was mit Slash beginnt, ist kein Prompt. Das schicken wir nicht an die KI — wir geben dem Anzug direkt einen Befehl."

### Keyboard-Shortcuts:

| Taste | Funktion |
|---|---|
| `Strg + O` | Erweiterte Tool-Ansicht ein/aus |
| `Escape` | Aktuelle Aktion abbrechen ODER Warteschlange bevorzugt behandeln |
| `Enter` | Prompt abschicken / Bestätigen |
| `Strg + V` | Einfügen (manchmal Rechtsklick → Bearbeiten → Einfügen nötig) |

### Genehmigungen:
- Claude Code fragt bei Tool-Nutzung oft nach Bestätigung
- Option 1 = einmalig genehmigen
- Option 2 = dauerhaft genehmigen (empfohlen für Komfort)

---

## Themenblock 11 — Wichtigster Prompt-Tipp der Session

> **Marco:**
> „Jeder von euch hat es heute schon mal gehört. Bitte nehmt diesen Tipp mit raus."

**Das Problem:**
Claude schlägt immer einen Weg vor — aber nicht unbedingt den besten.

**Die Lösung:**

Immer fragen:
> „Ich will nicht nur irgendeine Lösung. Ich will die einfachste und beste Lösung. Recherchier, wie andere das machen. Schlag mir mehrere Wege vor und erkläre, warum Weg A, Weg B, Weg C."

**Warum das wichtig ist:**
- Claude kennt alte und neue Wege
- Ohne Nachfragen wählt er oft einen, der funktioniert, aber nicht optimal ist
- Mit dieser Formulierung im ersten Prompt spart man sich viel Schmerz

### ✅ Learning
- Claude nie nur nach „irgendeiner" Lösung fragen
- Immer nach dem besten Weg fragen + Begründung verlangen
- Recherche immer mitanfordern bei Technologie-Fragen

---

## Weitere Beobachtungen / Sonstiges

**Janines Antivirus-Meldung beim Netzwerkscan:**
> „Das Virenprogramm soll es ja auch nicht mögen, wenn irgendwer das Netzwerk durchleuchtet — es weiß nicht, dass wir es selbst in Auftrag gegeben haben."

**Zu Verarbeitungsgeschwindigkeit:**
- Hängt hauptsächlich von der Menge der Arbeit ab
- Wenig von der Internetverbindung
- Manchmal von Serverauslastung beim Anbieter (Anthropic)
- Lokale Rechenleistung spielt kaum eine Rolle (500 MB RAM)

**Zu Firmenrechnern (Tobias):**
> „Outlook auf dem Rechner des Chefs und Claude auf deinem Rechner — die müssen irgendwie zusammenkommen. Entweder du gehst auf dem Rechner des Chefs in Outlook, oder du bringst Claude auf seinen Rechner."

---

## Hausaufgaben bis Session 3

1. **Mit Claude Code warm werden** — Claude Code statt ChatGPT benutzen, auch wenn die Oberfläche ungewohnt ist
2. **Etwas bauen lassen** — Taschenrechner, Tetris, Kalkulationsprogramm für die Firma — einfach ausprobieren
3. **Unzufrieden sein üben** — Wenn Ergebnis nicht passt: mitteilen, Feedbackschleife nutzen
4. **Claude fragen, was er kann** — „Was kannst du auf meinem Rechner alles machen?" — erkunden
5. **Immer nach dem besten Weg fragen** — Nicht nur „wie geht das?", sondern „was ist der einfachste und beste Weg?"

---

## Ausblick: Session 3

- **System Prompting praktisch** — Claude beibringen, wer wir sind: Name, Firma, Dateipfade, Ziele
- **Wissen festhalten** — Claude soll sich Infos über uns merken → „er kennt uns mit der Zeit"
- **Konkrete Use Cases** — Weg von Demo-Aufgaben, hin zu echten betrieblichen Anwendungen
- Ziel: „Nicht mehr jedes Mal mit einer KI sprechen, die frisch ist und uns gar nicht kennt"

---

## Schlüsselzitate

> *„Claude Code ist der Rennwagen, nicht der Fiat Punto zum Einkaufen."*
— Marco

> *„Vier andere Gruppen-Coaching-Teilnehmer berichten, dass sie mit ihrer Ehefrau weniger sprechen als mit dem Teil hier."*
— Marco

> *„Wir haben keine Ahnung, was wir hier tun, wir haben keine Ahnung, wofür wir es tun — aber wir lassen uns von KI helfen und kommen trotzdem zum Ziel."*
— Marco (zur Installation)

> *„90 Prozent der Qualität hängt von der Vollständigkeit des Prompts ab. Nur 10 Prozent von der Ordnung."*
— Marco

> *„Es gibt nichts, was verboten ist. Wenn ihr Schiss habt: Stellt wann immer ihr wollt die KI selbst — die ist sehr gut informiert."*
— Marco
