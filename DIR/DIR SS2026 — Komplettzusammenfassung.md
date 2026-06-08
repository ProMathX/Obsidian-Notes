# DIR SS2026 — Komplettzusammenfassung

Kurs: Daten und Informatikrecht · TU Wien · SS2026 Themen: Datenschutz · Digitale Barrierefreiheit · Lizenzen & Urheberrecht

---

# Teil 1: Datenschutz (DSGVO)

## Geschichte

- 400 BC: Hippokratischer Eid — erste Schweigepflicht
- 1215: Beichtgeheimnis (4. Laterankonzil) — absolut, selbst Beichtende können nicht entbinden
- 1867: Art. 15 Staatsgrundgesetz (Beichtgeheimnis AT), Art. 10 StGG (Briefgeheimnis)
- 1890: Brandeis & Warren, Harvard Law Review — Konzept moderner Datenschutz
- 1925: Art. 20 B-VG Amtsgeheimnis → abgelöst durch Informationsfreiheitsgesetz 01.09.2025
- 1970: Hessisches Datenschutzgesetz (erstes der Welt)
- 1973: Schwedisches Datenschutzgesetz
- 1977: Deutsches BDSG
- 1978: Österreichisches DSG
- 1995: EU-Datenschutzrichtlinie 95/46/EG
- 2018: DSGVO in Kraft

**Informationsfreiheitsgesetz (01.09.2025):** Informationen von allgemeinem Interesse müssen proaktiv veröffentlicht werden (Bund, Länder, Gemeinden >5.000). Beispiele: GE, Studien, Gutachten, Verträge. Ausnahme: nationale Sicherheit, Datenschutz. Frist: 4 Wochen (bzw. 8 Wochen).

## Grundbegriffe

**Personenbezogene Daten (Art. 3 Z 1 DSGVO):** Alle Informationen, die sich auf eine identifizierbare natürliche Person beziehen — direkt oder indirekt via Name, Kennnummer, Standortdaten, Online-Kennung oder besondere Merkmale (physisch, genetisch, psychisch, wirtschaftlich, kulturell, sozial).

**Verarbeitung (Art. 3 Z 2 DSGVO):** Jeder Vorgang mit personenbezogenen Daten: Erheben, Erfassen, Organisieren, Ordnen, Speichern, Anpassen, Auslesen, Abfragen, Verwenden, Übermitteln, Verbreiten, Abgleichen, Verknüpfen, Einschränken, Löschen, Vernichten.

**Sensible Datenkategorien:** rassische/ethnische Herkunft, politische Meinungen, religiöse/weltanschauliche Überzeugungen, Gewerkschaftszugehörigkeit, genetische Daten, biometrische Daten, Gesundheitsdaten, Sexualleben/Orientierung.

### Pseudonymisierung vs. Anonymisierung

||Pseudonymisierung|Anonymisierung|
|---|---|---|
|Wiederherstellung|leichter Aufwand (z.B. Look-Up-Table)|erheblicher Aufwand (z.B. K-Anonymity)|
|DSGVO-Pflicht|ja|nein|
|Geeignet für Löschantrag|nein|ja|
|Datenpanne|eventuell Vorteile|unbedenklich|

## Geltungsbereich

- Verantwortliche oder Auftragsverarbeiter mit Sitz in der EU
- **Marktortprinzip:** auch ohne EU-Sitz, wenn Waren/Dienstleistungen in EU angeboten ODER Verhalten von EU-Personen beobachtet wird

## 7 Grundprinzipien Art. 5 DSGVO

1. **Rechtmäßigkeit, Transparenz:** Verarbeitung rechtmäßig (Einwilligung oder Rechtsgrundlage), Betroffene kann von Verarbeitung erfahren
2. **Zweckbindung:** Zweck festgelegt, eindeutig, legitim. Ausnahme: Archiv, Forschung, Statistik
3. **Datenminimierung:** Dem Zweck angemessen, auf notwendiges Maß beschränkt → Minimal Data Set (MDS)
4. **Richtigkeit:** Sachlich richtig und aktuell, Recht auf Berichtigung/Löschung
5. **Speicherbegrenzung:** Speicherfrist auf Mindestmaß beschränkt, Pflicht zu Löschfristen
6. **Integrität und Vertraulichkeit:** CIA-Triad (Confidentiality, Integrity, Availability)
7. **Rechenschaftspflicht:** Verantwortlicher muss Einhaltung nachweisen können

## Betroffenenrechte

|Recht|Inhalt|
|---|---|
|Informationsrecht|Kenntnis, dass Daten verarbeitet werden|
|Auskunftsrecht|Daten, Zwecke, Quellen, Empfänger, Speicherfrist, Logik automatisierter Entscheidungen, internationale Transfergarantien|
|Recht auf Berichtigung|Änderung oder Vervollständigung|
|Recht auf Löschung|Daten nicht mehr notwendig oder Einwilligung widerrufen|
|Recht auf Einschränkung|Nur noch Speicherung erlaubt (z.B. während Prüfung der Richtigkeit)|
|Recht auf Datenübertragbarkeit|Strukturiertes, maschinenlesbares Format; Übertragung zu anderem Verantwortlichen|
|Widerspruchsrecht|Keine Weiterverarbeitung (Ausnahmen: Rechtsgrundlage, öffentliches Interesse)|

**Ablehnungsgründe Löschung:** freie Meinungsäußerung, rechtliche Verpflichtung (Aufbewahrungspflichten), öffentliche Gesundheit, Archiv/Forschung/Statistik, Rechtsansprüche.

**Fristen:** 1 Monat (verlängerbar auf 3 Monate) · kostenlos außer bei offenkundig unbegründeten/exzessiven Anträgen · Eskalation: binnen 1 Jahr bei DSb.

**Strafe bei Verletzung:** bis 20 Mio. EUR oder 4 % Jahresumsatz.

## Verantwortlicher

Natürliche oder juristische Person, die über Zwecke und Mittel der Verarbeitung entscheidet. Gesamtverantwortlich.

**Pflichten:**

- Datenschutzerklärung (Privacy Policy)
- Verarbeitungsverzeichnis
- Risikoanalyse / DSFA
- Datensicherheitsmaßnahmen (Privacy by Design, Privacy by Default, CIA-Triad)
- Ggf. Datenschutzbeauftragten bestellen
- Data Breach Meldung an DSb

**Datenschutzerklärung Pflichtinhalt:** Kontaktdaten Verantwortlicher + ggf. DSB · Datenkategorien · Quellen und Empfänger · Verarbeitungszwecke + Rechtsgrundlagen · Berechtigtes Interesse · Widerrufsmöglichkeit · Speicherdauer · Betroffenenrechte · Beschwerderecht DSb · Bestehen von Profiling/automatisierten Entscheidungen.

**Verarbeitungsverzeichnis Inhalt:** Kontaktdaten · DSB-Kontakt · Zwecke + Rechtsgrundlagen · Datenkategorien · Empfängerkategorien · Drittlandübermittlungen + Garantien · Löschfristen · Sicherheitsmaßnahmen.

**Verarbeitungsverzeichnis Ausnahmen (alle 4 Kriterien AND-verknüpft):** <250 Mitarbeiter + kein Risiko für Rechte + nur gelegentliche Verarbeitung + keine sensiblen Daten.

## Datenschutzfolgeabschätzung (DSFA)

**Erforderlich wenn:** voraussichtlich hohes Risiko für Rechte und Freiheiten natürlicher Personen.

**Klassische Fälle:** Profiling (systematische Bewertung persönlicher Aspekte) · umfangreiche Verarbeitung sensibler Daten · Videoüberwachung öffentlicher Bereiche.

**Kriterien (DSFA empfohlen bei ≥ 2 Kriterien OR „Rote Kategorie"):**

- Profiling
- Automatisierte Entscheidungsfindung
- Systematische Überwachung
- Sensible Daten
- Umfangreiche Verarbeitung
- Innovative Technologien (Biometrie, IoT, AI)
- Schutzbedürftige Betroffene (Kinder, Arbeitnehmer, Kranke)
- Verknüpfung von Datensätzen
- Auswirkung auf Vertragsabschluss

**Black-List (immer DSFA, gem. DSFA-V):** Profiling/Bewertung natürlicher Personen · automatisierte Entscheidungsfindung · systematische Überwachung öffentlicher Räume · innovative Technologien · unerwartete Datensatzverknüpfungen · höchstpersönlicher Bereich.

**White-List (keine DSFA, gem. DSFA-AV):** Kundenverwaltung, Rechnungswesen, Logistik · Personalverwaltung · Mitgliederverwaltung · Sach- und Inventarverwaltung · Register, Evidenzen · Zugriffsverwaltung EDV.

**DSFA-Inhalte:**

1. Beschreibung der Verarbeitungsvorgänge (Art, Umfang, Hardware, Software, Netzwerke)
2. Verarbeitungszweck + Rechtsgrundlage
3. Notwendigkeit und Verhältnismäßigkeit
4. Risikobewertung (Ursache, Art, Schwere, Eintrittswahrscheinlichkeit, Maßnahmen)
5. Abhilfemaßnahmen (Pseudonymisierung, Verschlüsselung, Backups, Zugangsbeschränkungen)
6. Standpunkt der Betroffenen (oder Begründung warum nicht eingeholt)
7. Empfehlung des Datenschutzbeauftragten

**Bei DSFA-Ergebnis = hohes Risiko ohne Abhilfemöglichkeit:** Konsultation der DSb verpflichtend.

## Data Breach Meldung

- Meldung an DSb bei Risiko
- Meldung an Betroffene bei **hohem** Risiko
- **Unverzüglich, spätestens 72 Stunden ab Bekanntheit**
- Inhalt: Art der Verletzung · wahrscheinliche Folgen · getroffene Maßnahmen · Kontaktdaten

## Datenschutzbeauftragte (DSB)

**Verpflichtend wenn:** umfangreiche regelmäßige und systematische Überwachung in der Kerntätigkeit (Banken, Versicherungen, Kreditauskunfteien) ODER Verarbeitung sensibler Daten.

**Qualifikation:** Zertifizierung TÜV/WIFI/ETC — ca. 3.000 EUR, 40h + Prüfung, 3 Jahre gültig.

**Aufgaben:** Beratung · Überwachung Einhaltung DSGVO · Schulungen · Beratung DSFA · Bearbeitung von Begehren.

## Auftragsverarbeiter

Verarbeitet Daten im Auftrag des Verantwortlichen (Beispiel: IT-Dienstleister; kein Auftragsverarbeiter: Steuerberater).

**Vertrag Pflichtinhalt:** Verarbeitung nur auf dokumentierte Weisung · Vertraulichkeit und Sicherheitsmaßnahmen · Unterauftragsverarbeiter nur mit Genehmigung · Unterstützung bei DSGVO-Pflichten · Löschung nach Vertragserfüllung.

## Internationaler Datenverkehr

**Nicht genehmigungspflichtig:** alle EU/EWR-Länder + Drittländer mit Angemessenheitsbeschluss (alle 4 Jahre erneuert): Andorra, Argentinien, Färöer, Guernsey, Insel Man, Israel, Japan, Jersey, Kanada, Neuseeland, Schweiz, Südkorea, Uruguay, UK, USA*.

*USA: nur zertifizierte Unternehmen (EU-US Data Privacy Framework, seit 2023) — dataprivacyframework.gov

**US-EU Geschichte:**

- 2000–2016: Safe Harbour (EuGH gekippt: Schrems I)
- 2016–2020: EU-US Privacy Shield (EuGH gekippt: Schrems II)
- 2023–heute: EU-US Data Privacy Framework (Biden Executive Order 2022)

**Standardschutzklauseln (SCC):** von EU-Kommission oder Aufsichtsbehörde abgenommen · rechtsverbindliche Garantien · Datenexporteur und -importeur müssen Recht des Drittlandes auf Wirksamkeit prüfen.

## Strafen

|Verstoß|Strafe|
|---|---|
|Gravierende Verstöße|bis 20 Mio. EUR oder 4 % weltweiter Jahresumsatz|
|Weniger gewichtige Verstöße|bis 10 Mio. EUR oder 2 % weltweiter Jahresumsatz|

## Behörden

**Datenschutzbehörde (DSb):** Unabhängige Justizbehörde · Leitung vom BPräs. auf 5 Jahre bestellt · Beschwerdeverfahren, amtswegige Prüfungen, Verwaltungsstrafverfahren.

**Europäischer Datenschutzausschuss (EDSA):** Ehemals Artikel-29-Gruppe · grenzüberschreitende Fälle · berät EU-Kommission · Leitlinien und Empfehlungen · Mitglieder aus allen EWR-Ländern.

## Praxistipps

### Sicherheitsmaßnahmen-Matrix

||Technisch|Organisatorisch|Physisch|
|---|---|---|---|
|Präventiv|Firewall|Awareness-Schulung|Tresor|
|Detektiv|Endpoint Protection|IT-Analysten|Lichtschranken|
|Reaktiv|Restoreplan|Maßnahmenplan|Alarm|
|Abschreckend|Protokollierung|Stichproben|Kameras|

### Werbung

|Opt-In erforderlich|Opt-Out möglich|
|---|---|
|Telefonwerbung (§ 174 TKG)|Postalische Werbung (§ 151 Abs 9 GewO)|
|E-Mail-Werbung an Nicht-Kunden|Werbung an bestehende Kunden (§ 174 TKG)|
|Verwendung sensibler Daten||
|Profiling||

### Cookies

- Einwilligung erforderlich (§ 165 ff TKG 2021)
- Ausnahme: funktionale Cookies (technisch notwendig)
- Device Fingerprinting umstritten (Einwilligung empfohlen)
- Einwilligung muss freiwillig sein — Nutzungspflicht als Bedingung = unzulässig
- Alternative: Gebühr für werbefreie Version zulässig

---

# Teil 2: Digitale Barrierefreiheit

## Definition & Grundlagen

**Digitale Barrierefreiheit:** Alle Menschen können Websites und Apps nutzen — mit oder ohne Beeinträchtigung — unabhängig von Behinderung, ohne besondere Erschwernis oder fremde Hilfe.

Barrierefreiheit ≠ Sonderlösung, sondern **inklusive Standardlösung**. Ziel: von Anfang an mitdenken (wie Responsiveness oder Dark-Mode).

**Dimensionen:**

- Visuell: Sehbeeinträchtigungen, Farbfehlsichtigkeit
- Auditiv: Hörbeeinträchtigungen, laute Umgebungen
- Motorisch: eingeschränkte Beweglichkeit
- Kognitiv: Lernschwierigkeiten, leichte Sprache

**Warum relevant für alle:** 1,9 Mio. Menschen in Österreich mit Beeinträchtigungen (1 von 4) · Senioren · situative Einschränkungen (Sonnenbrille, kein Kopfhörer, Fremdsprache) · besseres Design für alle.

## Mythen

|Mythos|Realität|
|---|---|
|Betrifft nur wenige|1,9 Mio. in AT, 1 von 4, steigt mit Alter|
|Schränkt Design ein|Gutes Design ist inklusives Design (Beispiel: Apple)|
|Zu teuer und aufwendig|Aufwand entsteht durch spätes Nachbessern — frühzeitig integriert günstig|
|KI/Plugins können nachbessern|Tools helfen, ersetzen aber kein Verständnis|
|Separate Angebote genügen|Inklusion statt Separation — „Barrierefrei First"|

Aktuell: >90 % aller Websites mit Barrieren (Monitoring Bericht 2022). Häufigste Probleme: fehlende Alt-Texte, schlechte Kontraste, Fokusprobleme.

## Gesetzliche Grundlagen — Österreichische Timeline

|Jahr|Gesetz|
|---|---|
|2004|E-Government-Gesetz (E-GovG) → barrierefreie Behörden-Websites|
|2008|Beitritt UN-Behindertenrechtskonvention|
|2016|BGStG (Bundes-Behindertengleichstellungsgesetz) → Diskriminierungsverbot IT|
|2016|EU-Richtlinie 2016/2102 (WAD) → Basis für WZG|
|2019|WZG – Web-Zugänglichkeitsgesetz → öffentliche Stellen|
|2019|EU-Richtlinie 2019/882 (EAA) → Basis für BaFG|
|2025|BaFG – Barrierefreiheitsgesetz → privater Sektor (ab 28.06.2025)|

## WZG — Web-Zugänglichkeitsgesetz (öffentliches Recht)

**Gilt für:** Bundesbehörden, Bundesministerien, **Universitäten**, Bundesunternehmen (§ 2 WZG).

**Anforderung:** wahrnehmbar, bedienbar, verständlich, robust (§ 3 WZG). Standard: **WCAG 2.1 AA**.

**Ausnahmen (§ 2 Abs 3 WZG):**

- Dateien vor 23.09.2018 veröffentlicht
- Videos/Audio vor 23.09.2020
- Live-Medien
- Karten (sofern Kerninformationen barrierefrei)
- Inhalte Dritter außerhalb Wirkungsbereich
- Intra-/Extranet vor 23.09.2019 bis Generalsanierung
- Schul- und Kindergartenwebsites
- Archivierte Inhalte
- Unverhältnismäßige Belastung

**Barrierefreiheitserklärung (§ 4 WZG) — Pflichtinhalt:**

- Einleitung
- Stand der Vereinbarkeit (vollständig / teilweise / nicht) mit WCAG 2.1 AA
- Auflistung nicht barrierefreier Inhalte
- Datum und Methode der Erstellung
- Feedback-Mechanismus
- Durchsetzungsverfahren
- Link auf FFG-Website

Erreichbar über Startseite · Reaktion auf Meldungen: **2 Monate** · Monitoring durch FFG (Österreichische Forschungsförderungsgesellschaft).

## BaFG — Barrierefreiheitsgesetz (privater Sektor)

**Ab 28.06.2025** in Kraft.

**Geltungsbereich (§ 2):**

- Hardware inkl. Betriebssysteme (PC, Mac)
- Selbstbedienungsterminals (Geld-, Fahrkarten-, Check-In-Automaten)
- Verbraucherendgeräte (Smartphones, Smart TVs)
- E-Book-Lesegeräte
- E-Kommunikationsdienste (Internet-/Videotelefonie, Messenger)
- Audiovisuelle Mediendienste
- Personenverkehr (Luft, Bus, Schiene, Schiff)
- Bankdienstleistungen
- E-Commerce B2C

**Ausnahmen:** Kleinstunternehmen (<10 Personen, <2 Mio. EUR Umsatz) · Stadt-/Regionalverkehr · Inhalte vor 28.06.2025 · Karten · Inhalte Dritter · Archivierte Inhalte.

**Übergangsfristen (§ 37):** bis 28.06.2030 (bestehende Dienste/Produkte) · bis 28.06.2040 (SB-Terminals).

**Pflichten Dienstleistungserbringer (§ 14):** Barrierefreiheitserklärung oder AGB (WCAG 2.1 AA / EN 301 549) · barrierefreie Beschreibung der Dienstleistung · Korrekturmaßnahmen bei Nichtkonformität · Kooperationspflicht gegenüber Sozialministerium · Aufbewahrungspflicht 5 Jahre.

**Strafe (§ 36):** Höchststrafe **80.000 EUR** · reduzierte Strafen für KMU/Kleinstunternehmen · Strafgelder fließen in Fonds für Menschen mit Behinderungen · Marktüberwachung: Sozialministerium.

## WCAG — Grundprinzipien (POUR)

|Prinzip|Inhalt|
|---|---|
|Perceivable (Wahrnehmbar)|Alt-Texte, Untertitel, ausreichende Kontraste|
|Operable (Bedienbar)|Tastaturzugänglichkeit, kein Zeitdruck, sichtbarer Fokus|
|Understandable (Verständlich)|Klare Sprache, konsistente Navigation, verständliche Fehlermeldungen|
|Robust|Kompatibel mit Hilfstechnologien, korrekte semantische HTML-Struktur|

**WCAG-Konformitätsstufen:** A (Minimum) · **AA (gesetzlich gefordert)** · AAA (freiwillig).

## Technische Anforderungen

**Alt-Texte:** Jedes informative Bild braucht beschreibenden Alt-Text · dekorative Bilder: alt="" · Beispiel: "Drei rote Birnen auf Holzstück".

**Tastaturzugänglichkeit:** Alle Funktionen per Tab/Enter/Pfeiltasten erreichbar · sichtbarer Fokus-Indikator · keine Tastaturfallen · logische Tab-Reihenfolge.

**Struktur & Navigation:** Überschriften-Hierarchie H1→H6 · Landmark-Regionen (nav, main, header, footer) · konsistente Navigation auf allen Seiten.

**Formulare:** Jedes Eingabefeld braucht `<label>` · präzise Labels ("E-Mail-Adresse" statt "Email") · Fehlermeldungen automatisch fokussiert · Zoom bis 200 % ohne Inhaltsverlust (WCAG-Anforderung).

## Testing-Tools

|Automatisiert|Semi-automatisch|
|---|---|
|Lighthouse (Chrome DevTools)|Keyboard-Testing (Tab-Navigation)|
|Accessibility Inspector (Firefox)|NVDA (NonVisual Desktop Access, Windows)|
|WAVE (Web Accessibility Evaluation Tool)|VoiceOver (macOS/iOS)|
|axe (Browser-Extension)|Contrast Checker / WCAG & APCA Kontrastrechner|
|Accessibility Linters|Zoom 200 % Test|

## UX Design Praxis-Checkliste

- Design von Anfang an inklusiv planen (Screenreader, Alt-Texte, Farbwahl)
- Klare, einfache Sprache
- Konsistente Navigation auf allen Seiten
- Sichtbares Feedback (Fokus-Stile, Fehlermeldungen)
- Responsive Design (flexible Layouts & Schriftgrößen)
- Eigene Komponenten nach WAI-ARIA Practices
- Geprüfte Designsysteme verwenden

---

# Teil 3: Lizenzen & Urheberrecht

## Schutzarten im Überblick

- Urheberschutz (UrhG)
- Markenschutz (MarkenSchG)
- Patentschutz (PatG)
- Gebrauchsmusterschutz
- Geschmacksmusterschutz ("Design-Schutz")

---

## Urheberrecht (UrhG)

### Geschichte

|Jahr|Ereignis|
|---|---|
|1440|Buchdruck|
|1475|Erstes 2-jähriges Druckrecht|
|1710|Statute of Anne (England)|
|1791|Droit d'auteur (Frankreich)|
|1795|Copyright (USA)|
|1952|Universal Copyright Convention (UCC)|

Zwei Konzepte: Anglo-Amerikanisch (öffentliches Interesse an Wissensverbreitung) vs. Französisch (Persönlichkeitsrechte).

### Schutzgebiete § 1 UrhG

**Voraussetzungen:** eigentümliche geistige schöpferische Leistung + Wahrnehmbarkeit + Originalität.

|Bereich|Beispiele|
|---|---|
|Literatur § 2|Sprachwerke, Computerprogramme, Bühnenwerke, Rezepte, Liedtexte, Drehbücher, Landkarten|
|Tonkunst § 1 ff|Musik (Melodie, Harmonik, Rhythmus) — Schlager, Sinfonie, Filmmusik, Computerspielmusik|
|Bildende Künste § 3|Baukunst, Fotografie, Malerei, Zeichnungen, 3D-Druck|
|Filmkunst § 4|Filmwerke, Laufbildwerke, Stummfilme, Tonfilme, Fernsehproduktionen|
|Sammelwerke § 6|Datenbanken, AI-Trainingsdaten, Kochbücher, Lexika, Magazine|

### Computerprogramme § 40 ff UrhG

- Umfasst alle Ausdrucksformen inkl. Maschinencode und Entwicklungsmaterial
- Werknutzungsrechte beim Dienstgeber (gilt auch für Datenbanken)
- Werknutzungsrechte prinzipiell übertragbar

**Berechtigte Nutzer dürfen:** Sicherungskopien herstellen · Funktionieren beobachten/untersuchen um zugrunde liegende Ideen zu ermitteln.

**OGH 4Ob45/05d — Schutzkriterien:** lange, viele Schritte, aufwändig, eigenartige UI · Aufgabe erlaubt mehrere Lösungen · individuelle Merkmale · ungewöhnlicher Grad an Erfahrung und Fachkenntnis.

### Rahmen & Schutzdauer § 10 ff UrhG

- Entsteht **mit der Schöpfung** — keine Registrierung erforderlich
- **Schöpferprinzip:** Persönlichkeitsrecht, an natürlicher Person gebunden
- **Regelschutzdauer:** 70 Jahre nach Tod des Schöpfers
- Vererbbar, aber **nicht übertragbar unter Lebenden**
- **Schutzlandprinzip**

**Miturheber vs. Teilurheber (§ 11):**

- Miturheber: gemeinsame Schaffung → gemeinsame Urheberrechte
- Teilurheber: Verbindung eigenständig verwertbarer Werke zu einem Ganzen

### Verwertungsrechte § 14 ff UrhG

Übersetzungs- und Bearbeitungsrecht · Vervielfältigungsrecht · Verbreitungsrecht · Vermietrecht · Senderecht · Vortrags-, Aufführungs-, Vorführungsrecht · Zurverfügungstellungsrecht.

### Leistungsschutzrechte

|Schutzgegenstand|Frist (Jahre)|
|---|---|
|Ausübender Künstler|50 / 70|
|Veranstalter|50|
|Lichtbilder, Laufbilder|50|
|Schallträger|70|
|Rundfunksendungen|50|
|Nachgelassene Werke|25|
|Datenbankhersteller|15|

### Nicht geschützt

**Freie Werke:** Gesetze, Verordnungen, amtliche Erlässe.

**Freihaltebedürfnis:** Gedanken, Ideen, Methoden, Systeme, technische Lösungen, mathematische Formeln, Theorien, Fakten, historische Abläufe, künstlerische Stile.

### Öffentliche Wiedergabe (OGH 4Ob347/97a)

Vorführung digitaler Werke vor unbestimmtem Personenkreis. Kriterien: keine persönliche Beziehung zum Veranstalter + großer Personenkreis + kommerziell.

### Freie Werknutzung § 41 ff UrhG

- Flüchtige und begleitende Vervielfältigungen (RAM, Swap)
- Vervielfältigung zum privaten und eigenen Gebrauch (h.M. 5–7 Kopien)
- Berichterstattung über Tagesereignisse
- Einrichtungen des Kulturerbes
- Beherbergungsbetriebe (in Amtssprache, nach 2 Jahren)
- Unwesentliches Beiwerk · amtlicher Gebrauch
- Barrierefreie Übersetzung
- Zitate, Karikaturen, Parodien und Pastiches
- Text- und Data-Mining
- Forschungseinrichtungen, nicht kommerziell
- Privat: rechtmäßiger Zugang, nicht ausdrücklich verboten
- Pressekonferenzen, politische Reden
- Tonkunst: kirchlicher, bürgerlicher, militärischer Anlass, nicht kommerziell
- Schul- und Universitätsprivileg, Forschung (ausgenommen: Skripte)

### Dekompilierung § 40e UrhG

Erlaubt bei: vorliegender Genehmigung · Herstellung von Interoperabilität · Behebung von Fehlern (EuGH).

### Scraping § 42h UrhG

Erlaubt für frei zugängliche Werke zur automatisierten Auswertung (Muster, Trends, Korrelationen). **Verboten** bei maschinenlesbarem Nutzungsvorbehalt (z.B. robots.txt, RFC 9309). Max. 500 KiB empfohlen.

### Recht am eigenen Bild § 78 UrhG

Bildnisse dürfen nicht öffentlich verbreitet werden, wenn berechtigte Interessen des Abgebildeten verletzt werden. Thumbnails: i.A. keine Verletzung. Paywalls dürfen nicht umgangen werden. Verlinkung auf illegale Inhalte verboten.

### Umgehung von Schutzmaßnahmen § 90b–d

Verboten: Umgehung technischer Schutzmaßnahmen + Herstellung/Verkauf/Vermietung von Umgehungsmitteln. Schutzsysteme: Zugangskontrolle (Passwörter) · Verwendungskontrolle (Kopierschutz, Geolocation) · Integritätskontrolle (Markierungen).

### Verwaiste Werke

Rechtsinhaber nicht feststellbar → unentgeltliche Nutzung für Bewahrung/Restaurierung/Gemeingüter. Meldung an EUIPO verpflichtend. Vergütungspflicht bei späterer Ausforschung — Recht verjährt nach 10 Jahren.

### Urheberrechtsverletzung — Rechtsfolgen

Unterlassungsklage · Beseitigungsklage · Schadensersatzklage · Urteilsveröffentlichung · bei Gewerbsmäßigkeit: bis zu 2 Jahren Freiheitsstrafe.

---

## Verwertungsgesellschaften (VerwGesG)

**§ 2 VerwGesG:** Organisation die in gesammelter Form Rechte mehrerer Rechteinhaber wahrnimmt, im Eigentum von Rechteinhabern.

|Gesellschaft|Zuständigkeit|
|---|---|
|AKM / AUME|Musik: öffentliche Aufführung, Radio, TV, Klingeltöne, Downloads, Streaming, SMV|
|Bildrecht GmbH|Bildende Kunst, Architektur, Fotografie, Grafik, Design, Folgerechtsgebühren|
|Literar-Mechana|Sprachwerke, Musiknoten, Bibliothekstantieme, Reprographievergütung|
|LSG|Leistungsschutzrechte|
|RAW, VAM|Filmkunst und Laufbilder|
|VGR|Literatur/Kunst (Rundfunkunternehmer)|
|VdFS|Film: Regie, Kamera, Schnitt, Szenenbild, Kostümbild, Schauspiel|

---

## Markenrecht

**Grundlagen:** Unternehmenskennzeichen + Kennzeichen von Waren/Dienstleistungen · Marketingtool · Schutzlandprinzip · Klassifikation von Nizza: 34 Warenklassen + 11 Dienstleistungsklassen · Benutzungszwang: Löschungsantrag nach 5 Jahren möglich · nachträgliche Erweiterung nicht möglich.

### Markenarten

|Markenart|Beschreibung|
|---|---|
|Wortmarke|Buchstaben, Zahlen, Sonderzeichen — keine Formatierung|
|Bildmarke|Vektorgrafik/PNG, mono- oder polychrom, statisch|
|Wortbildmarke|Kombination Wort + Bild|
|Positionsmarke|Gleichbleibende Position auf markierten Waren|
|Formmarke|3D-Form|
|Farbmarke|Farbe i.V.m. Verkehrskreis|
|Klangmarke|Jingle, kurze Tonfolge|
|Hologrammarke|Holografische Merkmale|
|Mustermarke|Regelmäßig wiederholte Elemente|
|Bewegungsmarke|Bewegung/Positionsänderung, keine Töne|
|Multimediamarke|Bewegung/Positionsänderung inkl. Töne|

### Registrierungshindernisse § 4 MarkenSchG

Konflikt mit eingetragener Marke · fehlende Unterscheidungskraft · Hoheitszeichen · sittenwidrig/gesetzeswidrig · Täuschung · Deonym/Freihaltebedürfnis.

### Registrierung

|Typ|Behörde|Dauer|Schutz|
|---|---|---|---|
|Nationale Marke|Patentamt|3 Monate (10 Tage Fast-Track)|AT|
|Unionsmarke|EUIPO|6 Monate (15 Tage Fast-Track)|EU|
|Internationale Marke|Madrider Abkommen|18 Monate|120 Länder|

Kosten: 1.000–3.000 EUR · Schutzdauer: **10 Jahre** (verlängerbar) · ® erst ab Registrierung.

---

## Patente

**Voraussetzungen:** neu (zum Zeitpunkt der Anmeldung nicht bekannt) · gewerblich anwendbar · nicht trivial · Lösung eines technischen Problems · Patent wird veröffentlicht · max. **20 Jahre** Schutzdauer.

**Sachpatent:** räumlich fassbarer Gegenstand (Maschine, Medikament). **Verfahrenspatent:** zeitlicher Ablauf von Vorgängen (Herstellungs-/Anwendungsverfahren). **Verwendungspatent:** bekannte Sachen/Verfahren auf neue, nicht naheliegende Art.

**Nicht patentierbar:** Entdeckungen, wissenschaftliche Theorien, mathematische Methoden · Diagnoseverfahren, chirurgische Verfahren · Wiedergabe von Informationen · Perpetuum mobile · Pflanzensorten/Tierarten · **Quellcode** · Sittenwidriges.

**Computerprogramme als Patent:** nur wenn "weitere technische Wirkung" über normale Hardware-Software-Wechselwirkung hinausgeht.

### Patent vs. Gebrauchsmuster

||Patent|Gebrauchsmuster|
|---|---|---|
|Neuheitsschonfrist|0 Monate (absolut)|6 Monate|
|Max. Schutzdauer|20 Jahre|10 Jahre|
|Prüfung|a priori|a posteriori|
|Kosten|höher|niedriger|

Können gleichzeitig angemeldet werden.

---

## Geschmacksmusterschutz

Schützt das Aussehen (Farben, Form, Oberflächenstruktur, Werkstoff) · 2D und 3D · Computerprogramme nicht schützbar (aber: Website-Layout schützbar) · Sammelmusteranmeldung (bis 50 Muster) · Geheimmuster (18 Monate) · **25 Jahre** Schutz (5 × 5 Jahre) · ab 100 EUR · **12 Monate Neuheitsschonfrist** · WIPO (67 Länder).

---

## Lizenzen

**Definition:** rechtliche Grundlage, über geistiges Eigentum verfügen zu dürfen. Beinhaltet i.d.R. Recht auf Nutzung, Herstellung oder Verkauf.

### Exklusivität

|Merkmal|Exklusiv|Allein|Nicht-Exklusiv|
|---|---|---|---|
|Lizenznehmer erwirbt Rechte|ja|ja|ja|
|Alleiniges Ausübungsrecht|ja|—|—|
|Lizenzgeber darf weitere vergeben|—|—|ja|
|Lizenzgeber darf selbst ausüben|—|ja|ja|

**Sublizenz:** ohne ausdrückliche Vereinbarung nicht erlaubt.

**Beschränkungen:** personell (Floating, Named User) · örtlich · zeitlich · technisch (CPU, RAM).

**Gebührenmodelle:** Initialkosten · wiederkehrende Fixkosten · nutzungsabhängige variable Kosten (CPU, Nutzer, I/O).

**EULA:** Browsewrap, Clickwrap, Shrinkwrap · Ziel Lizenzgeber: Eigentum behalten, Haftung abgeben.

---

## Open Source & FLOSS

### Geschichte

|Jahr|Ereignis|
|---|---|
|1983|GNU-Projekt (Stallman)|
|1985|Free Software Foundation|
|1987–88|GCC, GDB|
|1989|GPLv1|
|1991|GPLv2|
|1992|LGPL + GNU/Linux|
|2007|GPLv3|

### Vier Freiheiten

- **0:** Programm für jeden Zweck ausführen
- **1:** Funktionsweise untersuchen und anpassen (Quellcode erforderlich)
- **2:** Programm umverteilen
- **3:** Verbessern und Verbesserungen freigeben (Quellcode erforderlich)

### OSS-Definition (10 Kriterien)

Freie Weiterverbreitung · Quellcodezugang · abgeleitete Werke erlaubt · Integrität des Autorcodes · keine Diskriminierung · keine Nutzungseinschränkungen · allgemeingültige Lizenz · produktneutral · keine Einschränkung anderer Software · technologieneutral.

---

## Lizenzübersicht

### Permissive Lizenzen (kein Copyleft)

|Lizenz|Bedingungen|Hinweis|
|---|---|---|
|MIT-0 / BSD-0|Keine|Public Domain Äquivalent|
|MIT|Copyright-Hinweis in Kopien|Ruby, Node.js, Angular, React|
|BSD-2-Clause|Copyright in Source + Binaries|a.k.a. Simplified BSD|
|BSD-3-Clause|BSD-2 + kein Endorsement|a.k.a. New BSD. Django, Go, Chromium|
|BSD-4-Clause|BSD-3 + Werbematerial-Acknowledgement|Inkompatibel mit GPL → Lösung: BSD-3|
|Apache 1.0|Angelehnt BSD-4, "Apache" nicht im Namen|—|
|Apache 1.1|Angelehnt BSD-3, Anerkennung in Doku|—|
|Apache 2.0|Patentlizenz, Offenlegungspflicht Codeänderungen, kein Copyleft|Kafka, Tomcat, Spark|

### Copyleft

> Abgeleitete Werke müssen unter denselben Lizenzbedingungen freigegeben werden. Copyleft-Effekt tritt mit der **Distribution** in Kraft.

|Lizenz|Besonderheit|Stärke|
|---|---|---|
|GPLv1|Einführung Copyleft + Offenlegungspflicht Sourcecode|stark|
|GPLv2|Liberty-Or-Death-Klausel (§7), geographische Eingrenzung (§8)|stark — Git, WordPress, Linux|
|LGPLv2|Für Libraries — kein Copyleft für Nutzung, Copyleft für Ableitungen|schwach (Library)|
|GPLv3|Verbot Tivoisierung, keine geogr. Einschränkung, Apache-Kompatibilität|stark|
|LGPLv3|Wie LGPLv2 in Anlehnung an GPLv3|schwach (Library) — 7-Zip, VLC|
|AGPLv3|Offenlegungspflicht auch für SaaS-Nutzung|sehr stark — Grafana, MinIO|

**Dual-Licensing:** Software unter zwei Lizenzen gleichzeitig (z.B. GPL + kommerziell).

---

## Creative Commons

|Kürzel|Bedeutung|
|---|---|
|CC0|Aktiv in Public Domain gestellt|
|PD Mark|Urheberrecht abgelaufen|
|BY|Namensnennung erforderlich|
|SA|Share Alike — Copyleft-Effekt|
|NC|Nicht kommerziell|
|ND|Keine Bearbeitungen erlaubt|

**CC 4.0 Kombinationen:** CC0 · CC BY · CC BY-SA · CC BY-NC · CC BY-ND · CC BY-NC-SA · CC BY-NC-ND.

**Legacy (nicht mehr aktiv):** CC DevNations · CC Sampling · CC Sampling+.

---

## Querverbindungen (Prüfungsrelevant)

- Urheberrecht entsteht automatisch — Marken/Patente/Geschmacksmuster müssen **registriert** werden
- Quellcode: **kein Patent**, aber **Urheberrechtschutz** greift
- Datenbanken: Schutz als Sammelwerk (UrhG) + Leistungsschutz des Herstellers (15 Jahre)
- robots.txt + § 42h UrhG: Scraping erlaubt, sofern kein maschinenlesbarer Nutzungsvorbehalt
- Copyleft tritt erst bei **Distribution** in Kraft — relevant für SaaS (→ AGPLv3)
- BSD-4-Clause inkompatibel mit GNU GPL → BSD-3-Clause verwenden
- DSFA Empfehlung: bei ≥ 2 Kriterien OR „Rote Kategorie"
- Data Breach: **72h ab Bekanntheit**, nicht ab dem Ereignis
- WZG gilt für TU Wien (Universität = öffentliche Stelle)
