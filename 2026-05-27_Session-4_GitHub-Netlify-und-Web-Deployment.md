# Session 4 — GitHub, Netlify & Web-Deployment
**Datum:** 27. Mai 2026  
**Thema:** Von der lokalen HTML-Datei zur live Web-App  
**Hinweis:** Session 5 fällt aus — Marco Heer spricht als Guest-Speaker bei der Handwerkskammer Koblenz.

---

## Teilnehmer

| Person | Rolle | Status |
|--------|-------|--------|
| Marco Heer | Coach / Speaker (Speaker B) | Synclaro |
| Marvin (ZFG) | Teilnehmer (Speaker D) | HWK-Berater, heute Testproband |
| Fabian | Teilnehmer (Speaker A) | Plant Ausschreibungsportal-Automatisierung |
| Tobias | Teilnehmer (Speaker C) | KMS-Reset, Neuinstallation via Betriebsanleitung |
| Andreas | Teilnehmer (Speaker E) | Netlify-Deploy live, Firmenwebsite in CI umgestaltet |
| Janine | Teilnehmer (Speaker F) | 40 Dateien auf GitHub, plant Dokumentenmanagement-System |

---

## Der Tobias-Moment — KMS von Null neu einrichten

Tobias hatte frustriert alles gelöscht — nach ~25 erfolglosen Versuchen, dasselbe wie Fabian hinzubekommen. Marco's Reaktion: Kein Debuggen, sondern sauberer Neustart mit der **Betriebsanleitung** (MD-Datei im Synclaro-Portal).

**Der Ergänzungsprompt von Marco:**
> "Ich möchte, dass du die in dieser Betriebsanleitung niedergeschriebene Systematik bei mir installierst. Dinge, die du explizit NICHT tun sollst: GitHub und Vektoren. Ich möchte nur Logbuch, Decisions, Learnings, Wissensordner und den /post-Skill."

**Ergebnis:** Tobias hatte in wenigen Minuten ein funktionsfähiges KMS.

**Kern-Learning:** LLMs auf verschiedenen Computern liefern bei gleichem Prompt unterschiedliche Ergebnisse — wie Menschen. Ursachenanalyse ist manchmal weniger wertvoll als ein sauberer Neustart mit besserem Prompt.

---

## Haupt-Thema: GitHub — Warum es der Kern von allem ist

### Die Geschichte von Git

2004 hat ein Entwickler "auf die Schnauze gefallen", weil er keine Speicherstände hatte. Er erfand **Git** — ein Versionierungssystem mit Speicherständen, zu denen man zurückkehren kann. Daraus entstand später **GitHub**: ein Marketplace für Developer, wo Code geteilt und kollaborativ entwickelt wird.

### Die drei Kern-Bedürfnisse, die GitHub löst

1. **Rückgängig machen:** "Scheiße gebaut? Zurück zum alten Stand." Wie Speicherpunkt beim Zocken.
2. **Zusammenarbeiten:** Fabian und Andreas an derselben Code-Basis gleichzeitig arbeiten können.
3. **Single Source of Truth:** "Wo ist der neueste Stand?" → Immer auf GitHub. Einmal drauf zeigen können.

### GitHub CLI — Installation in der Praxis

```bash
# Claude Code installiert die GitHub CLI automatisch
gh                     # GitHub CLI — Claude bedient alles für dich

# Einmalig selbst einloggen (aus Sicherheitsgründen)
! gh auth login        # ! = Befehl direkt ans Terminal, nicht an Claude

# Danach erledigt Claude alles automatisch:
gh repo create zeiterfassung    # Repo anlegen
git add . && git commit -m "…"  # Committen
git push -u origin main         # Hochladen
```

Das Ausrufezeichen `!` ist ein Claude-Code-Feature: Es leitet Befehle direkt ans Terminal — für `gh auth login` nötig, weil der User sich persönlich im Browser verifizieren muss.

---

## Netlify — Der moderne Hoster

Netlify bietet eine **API** (Programmierschnittstelle), über die Claude Code alles automatisch erledigen kann. Kein manuelles Hochladen, kein Öffnen der Oberfläche.

**GitHub-Netlify-Brücke:** Einmal verbinden → jeder `git push` deployt automatisch eine neue Version auf Netlify. Der vollständige Workflow:

```
Dein Prompt (1 Satz)
  → Claude Code baut die App
  → git push zu GitHub
  → Netlify erkennt die Änderung automatisch
  → Deployt die neue Version
  → Live-URL bereit
```

**Staging vs. Production:**
- **Production:** Die echte Live-URL — nur wenn alles fertig ist
- **Staging:** Eine zweite Netlify-Domain, nur für dich zum Testen

---

## API-Schlüssel — Die wichtigste Erkenntnis dieser Session

> *"Was wir heute eigentlich gelernt haben, ist nicht GitHub und Netlify. Die wahre Message war: Ein API-Schlüssel ermöglicht es, dass Claude Code für euch Programme bedient."* — Marco Heer

**Netlify Personal Access Token erstellen:**
1. Netlify → Profilbild → User Settings → OAuth → Personal Access Token
2. Name: `Claude Code`, Expiration: kein Ablauf
3. Token an Claude geben: "Hinterlege diesen Schlüssel permanent"
4. Als Windows-Umgebungsvariable: `NETLIFY_AUTH_TOKEN`

Ab jetzt kann Claude: Neue Sites anlegen · Updates deployen · Domains konfigurieren · Logs prüfen — **ohne dass die Netlify-Oberfläche je wieder manuell geöffnet werden muss.**

---

## Der One-Prompt-Website-Builder

Marco's Demo-Prompt (live vor der Gruppe vorgetragen):

> *"Erstelle eine neue Webseite für die Kfz-Meisterwerkstatt Max Müller von nebenan. Recherchiere diese kurz, hol dir die Inhalte und überleg, wie du die Website deutlich moderner gestalten kannst. Gestalte die Website dann von vorn bis hinten durch und hör nicht auf zu arbeiten, bevor du nicht fertig bist. Das ganze Projekt speicherst du bitte auf GitHub und legst dann in Netlify eine neue Webseite an, die du mit dem GitHub Repository verknüpfst und bringst alles direkt live. Ich gehe jetzt Kaffee trinken."*

**Marco's Remote-Control Setup:** Er fernsteuert Claude Code per Handy über einen Apple-Server zu Hause. Bei HWK-Vorträgen: Prompt per Whisper Flow (Sprache) → 5 Minuten → Live-Website.

**Marco ist Speaker bei 32 Handwerkskammern deutschlandweit.** Der One-Prompt-Builder ist sein Showstopper.

---

## Bonus-Demo: Meta Trimodal Brain Encoder

Meta hat **700 Probanden** über 1 Jahr MRT-Daten während Videokonsum gesammelt und daraus ein KI-Modell gebaut, das mit **75% Genauigkeit** vorhersagt, wie ein Gehirn auf bestimmten Content reagiert.

- **Open Source:** Ja — Antrag bei Meta stellen
- **Drei Modalitäten:** Bild, Audio, Sprache
- **Zeigt:** Welche Gehirnbereiche durch welche Szene getriggert werden
- **Bedeutung:** Was nur Konzerne mit echtem MRT konnten, kann jeder mit Claude Code nachbauen

> *"Netflix-Filme werden in 2 Jahren vorab ausgewertet. Werbung läuft heute schon so bei Konzernen. Was nur Konzerne konnten, kann Marco jetzt mit seinem MacBook."*

---

## Hausaufgaben

- [ ] GitHub CLI auf eigenem Rechner einrichten (falls nicht in Session gemacht)
- [ ] Eine eigene HTML-Datei auf GitHub hochladen und auf Netlify deployen
- [ ] `NETLIFY_AUTH_TOKEN` als Windows-Umgebungsvariable hinterlegen
- [ ] In der globalen CLAUDE.md verankern: GitHub-Nutzung ist erwünscht

---

## Glossar

| Begriff | Bedeutung |
|---------|-----------|
| `gh` | GitHub CLI — Claude kann GitHub damit bedienen |
| `gh auth login` | Einmalige Authentifizierung (im Browser) |
| `git push` | Code zu GitHub hochladen |
| **Deploy** | Dateien online bringen, sodass Menschen darauf zugreifen können |
| **API** | Programmierschnittstelle — ermöglicht Claude, Tools für dich zu bedienen |
| **Personal Access Token** | API-Schlüssel für Netlify (= `NETLIFY_AUTH_TOKEN`) |
| **Single Source of Truth** | Eine einzige verlässliche Quelle für den aktuellen Stand — immer GitHub |
| **Staging** | Test-Umgebung (private URL), bevor etwas live geht |
| **Production** | Die echte Live-Umgebung, die alle Nutzer sehen |
| **One-Prompt-Builder** | Ein einziger Prompt → fertige App → GitHub → Netlify → Live-URL |

---

## Schlüsselzitate

> *"GitHub ist wie eine OneDrive, die von eurem Claude Code bedient wird. Single Source of Truth — immer."*

> *"Wenn Claude 322 Log-Einträge hat, wo er sieht — der Marvin macht hier krassen Scheiß — dann wird Claude solche dummen Vorschläge nicht mehr machen."*

> *"Wir sind heute in Woche 4 von 26. Ihr habt noch nicht mal einen Kopf unter Wasser gesteckt."*

> *"Selbst wenn jetzt irgendein Fuzzi daherkommt und euch eine neue Website verkaufen will — jetzt wisst ihr, was ihr dem antworten könnt."*

---

## Ausblick auf nächste Sessions

- Session 5 fällt aus (HWK Koblenz Vortrag)
- **Nächste Themen:** Supabase-Datenbank, komplexere Web-Applikationen, Automatisierungen
- **Langfristig:** MCP-Server, Vektordatenbanken, Company-GPT bauen, Multi-Agenten
