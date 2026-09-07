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

## ⚠️ Vor dem Livegang: LeadTable-Webhook eintragen

Die Bewerbungen werden per Webhook an die **LeadTable-Kachel** übergeben:

> https://portal.lead-table.com/customer/6a9e883851985db22f0468db/table/6a9e88443f84499505e63f81/leads

In `index.html` steht dafür die Variable `WEBHOOK_URL` – aktuell mit
Platzhalter `DEIN_WEBHOOK_TOKEN_HIER`. **So den echten Link einsetzen:**

1. LeadTable öffnen → diese Tabelle (ILG Drehteile) auswählen.
2. Integrationen / **„Generic Webhook"** öffnen und den generierten Link kopieren
   (Format: `https://api.lead-table.com/api/webhook/generic/<TOKEN>`).
3. In `index.html` bei `var WEBHOOK_URL = "…"` einsetzen und pushen.

Der Token ist signiert (JWT) und lässt sich nur in LeadTable erzeugen – deshalb
kann er hier nicht vorab hinterlegt werden. Solange der Platzhalter steht,
erscheint in der Browser-Konsole eine Warnung und es wird **kein** Lead
zuverlässig übergeben.

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

## Ad-Creatives

Im Ordner `creatives/` liegen fertige META-Motive je Stelle in zwei Formaten:

- `creative-<stelle>-4x5.png`   – 1080 × 1350 px (Feed / Beitrag)
- `creative-<stelle>-story.png` – 1080 × 1920 px (Story / Reels)

Empfohlene Ziel-URL der Ad je Motiv: der passende Deeplink oben
(z. B. QS-Motiv → `…/?stelle=qualitaetssicherung`).

## Live schalten (GitHub Pages)

1. Repo-Settings → **Pages** → Source: **Deploy from a branch**, Branch: `main` / `/ (root)`.
2. Nach ein paar Minuten ist die Seite unter
   `https://<user>.github.io/ilg-drehteile/` erreichbar (bzw. unter der
   hinterlegten Custom-Domain).

## Noch prüfen / anpassen (Kunde)

- **LeadTable-Webhook** eintragen (siehe oben) – Pflicht vor Livegang.
- **Rechts-Links** im Footer & Formular: `…/impressum/` und `…/datenschutz/`
  auf die tatsächlichen ILG-URLs prüfen (Pfad ggf. anpassen).
- **Kontakt-E-Mail** `info@ilg-drehteile.de` ggf. durch eine dedizierte
  Bewerbungs-Adresse ersetzen.
- **Stellenauswahl**: QS ist das aktuelle Ziel-Motiv. Einrichter & Zerspanung
  sind als weitere passende Positionen angelegt – bei Bedarf entfernen/ändern.
