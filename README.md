# ILG Drehteile – Karriereseite

Recruiting-Landingpage / Ad-Funnel für die **ILG Drehteile GmbH** (Wellendingen).
Aktuell gesucht (einzige offene Stelle auf der Seite): **Mitarbeiter
Qualitätssicherung (m/w/d)**.

Aufbau 1:1 an der ALWA-Karriereseite orientiert – im ILG-Corporate-Design (Blau).

## Inhalt

- `index.html` – die komplette Seite (self-contained, keine Build-Schritte nötig)
- `supabase-bewerbungen.sql` – legt/prüft den Storage-Bucket für den optionalen Lebenslauf-Upload
- `creatives/` – META-/Instagram-Ad-Creatives (4:5 Feed + 9:16 Story) je Stelle
- `bilder/` – hier Logo & Hero-Fotos ablegen (siehe `bilder/HIER-BILDER-ABLEGEN.txt`)
- `.nojekyll` – sorgt dafür, dass GitHub Pages die Dateien 1:1 ausliefert

## LeadTable-Anbindung (aktiv)

Jede abgeschlossene Bewerbung wird per Webhook an die **LeadTable-Kachel**
übergeben:

> https://portal.lead-table.com/customer/6a9e883851985db22f0468db/table/6a9e88443f84499505e63f81/leads

Der Generic-Webhook-Link ist in `index.html` in der Variable `WEBHOOK_URL`
**hinterlegt und aktiv** (Host `api-v2.lead-table.com`). Zum Wechseln der
Ziel-Tabelle in LeadTable einen neuen „Generic Webhook"-Link erzeugen und dort
ersetzen.

Übergebene Felder u. a.: `vorname`, `nachname`, `name`, `email`, `telefon`,
`stelle`, `erfahrung`, `lebenslauf`, `datenschutz`, `quelle`, `seite`.

## Ad-Deeplink

Es gibt nur eine offene Stelle. Für die Anzeige empfiehlt sich der Deeplink
`…/?stelle=qualitaetssicherung` – er setzt Hero-Headline und Hero-Foto auf die
QS-Stelle (das Formular startet ohnehin direkt bei der ersten Frage). Ohne
Parameter zeigt der Hero das allgemeine Firmen-Motiv.

## Screening / Vorfilterung (Punktesystem)

Der Funnel stellt **3 Qualifizierungsfragen** (je 0–3 Punkte, max. 9):

1. **Qualifikation** (Ausbildung/Erfahrung) – A/B = 3, C = 2, D („weder …") = 0
2. **Technische Zeichnungen & Messmittel** – A = 3, B = 2, C = 1, D = 0
3. **Deutschkenntnisse** (Prüfpläne/Doku) – A = 3, B = 2, C = 1, D = 0

Ausgewertet wird **nach der letzten Frage** (vor den Kontaktdaten). Abgelehnt
wird freundlich (kein Lead an LeadTable), wenn

- die **Gesamtpunktzahl < 4** ist (jemand füllt alles maximal schlecht aus), **oder**
- bei Frage 1 „**Weder Ausbildung noch Erfahrung**" gewählt wurde (harte Grenze).

Andernfalls geht die Bewerbung durch; im Lead landen zusätzlich die Felder
`messmittel`, `deutsch` und `qualifikation_score` (z. B. „6 / 9") – so lassen
sich Bewerbungen in LeadTable nach Qualität sortieren.

Schwelle anpassen: in `index.html` die Variable **`SCORE_MIN`** ändern
(höher = strenger). Ein Seiten-Neuladen startet frisch – keine dauerhafte Sperre.

## Lebenslauf-Upload (optional)

Nutzt Supabase Storage (Bucket `bewerbungen`, gemeinsames Agentur-Projekt).

**Wichtig:** Der Upload ist bewusst **nicht blockierend**. Klappt er nicht
(z. B. Bucket/Policy im Supabase-Projekt noch nicht angelegt oder Projekt
pausiert), wird die Bewerbung **trotzdem** normal gesendet – der Bewerber sieht
„Bewerbung eingegangen", und im LeadTable-Feld `lebenslauf` steht dann
`Upload fehlgeschlagen (<Dateiname>) – Bewerber ggf. per E-Mail nachfassen`.

Damit der Upload wirklich funktioniert (öffenbarer Link im Feld `lebenslauf`):
einmalig `supabase-bewerbungen.sql` im Supabase-SQL-Editor des Projekts
ausführen (legt Bucket + Anon-Insert-Policy an). Ist er von einer anderen
Karriereseite bereits angelegt, genügt es zu prüfen, dass das Projekt aktiv ist.

## Bilder & Logo

Fotos/Logo gehören in `bilder/` (exakte Dateinamen siehe
`bilder/HIER-BILDER-ABLEGEN.txt`). Fehlt ein Hero-Foto, bleibt der
ILG-Farbverlauf stehen – nichts geht kaputt.

## Ad-Creatives & Werbetexte

Im Ordner `creatives/` liegen fertige META-Motive je Stelle – jeweils in zwei
Formaten **und** zwei Stilen (zum A/B-Testen):

- `creative-<stelle>-4x5.png` / `-story.png` – **Foto-Version** (echtes ILG-Foto)
- `creative-<stelle>-clean-4x5.png` / `-clean-story.png` – **Clean-/Grafik-Version**

Formate: 4x5 = 1080 × 1350 px (Feed), story = 1080 × 1920 px (Story/Reels).

Die passenden **Anzeigentexte** (Primärtext, Überschriften, Beschreibung,
Targeting, Kampagnen-Setup) stehen in **`WERBETEXTE.md`**.

Empfohlene Ziel-URL der Ad je Motiv: der passende Deeplink oben
(z. B. QS-Motiv → `…/?stelle=qualitaetssicherung`).

## Live schalten (GitHub Pages)

1. Repo-Settings → **Pages** → Source: **Deploy from a branch**, Branch: `main` / `/ (root)`.
2. Nach ein paar Minuten ist die Seite unter
   `https://<user>.github.io/ilg-drehteile/` erreichbar (bzw. unter der
   hinterlegten Custom-Domain).

## Noch prüfen / anpassen (Kunde)

- **Rechts-Links** im Footer & Formular: `…/impressum/` und `…/datenschutz/`
  auf die tatsächlichen ILG-URLs prüfen (Pfad ggf. anpassen).
- **Kontakt-E-Mail** `info@ilg-drehteile.de` ggf. durch eine dedizierte
  Bewerbungs-Adresse ersetzen.
- **Nur eine Stelle**: Auf der Seite ist ausschließlich die Qualitätssicherung
  ausgeschrieben. Creatives/Werbetexte für Einrichter & Zerspanung liegen weiter
  in `creatives/` bzw. `WERBETEXTE.md`, werden aber nicht verwendet.
