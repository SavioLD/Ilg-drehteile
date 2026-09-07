# ILG Drehteile – Karriereseite

Recruiting-Landingpage / Ad-Funnel für die **ILG Drehteile GmbH** (Wellendingen).
Aktuell gesucht: **Mitarbeiter Qualitätssicherung (m/w/d)**. Weitere Stellen:
Einrichter CNC-Langdrehen und Zerspanungsmechaniker / CNC-Dreher (m/w/d).

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

## Stellen-Deeplinks für die Ad

Die Anzeige kann direkt auf eine Stelle verlinken; die Seite wählt sie vor,
setzt die Hero-Headline und startet beim Erfahrungs-Schritt:

- `…/?stelle=qualitaetssicherung`  ← **aktuelle Kampagne (QS)**
- `…/?stelle=einrichter`
- `…/?stelle=zerspanung`

## Screening / Vorfilterung

Wer bei der Erfahrungsfrage „**Weder Ausbildung noch Erfahrung im Bereich**"
wählt, wird höflich aus dem Prozess genommen (kein Lead an LeadTable). So kommen
qualifiziertere Bewerbungen an. Ein Seiten-Neuladen startet frisch – es gibt
keine dauerhafte Sperre.

## Lebenslauf-Upload (optional)

Nutzt Supabase Storage (Bucket `bewerbungen`, gemeinsames Agentur-Projekt).
Ist der Bucket bereits von einer anderen Karriereseite angelegt, ist nichts zu
tun. Andernfalls einmalig `supabase-bewerbungen.sql` im Supabase-SQL-Editor
ausführen – danach landet im LeadTable-Feld `lebenslauf` ein direkt öffenbarer
Link.

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
- **Stellenauswahl**: QS ist das aktuelle Ziel-Motiv. Einrichter & Zerspanung
  sind als weitere passende Positionen angelegt – bei Bedarf entfernen/ändern.
