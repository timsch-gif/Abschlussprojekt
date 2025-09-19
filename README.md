#  DTM | Abschlussprojekt - Timo Schwarz | SoSe25 
## Impressum

Autor:  Timo Schwarz\
Matr.Nr:  107211\
Kontakt:  tisc3469@bht-berlin.de\
Kurs:  Visualisierung von Geodaten (DTM)\
Betreuer:  Prof. Dr. Florian Hruby
<br><br><br>
# Inhaltsverzeichnis
[EP.01 | Dasymetrische Choroplethenkarte](#EP.1)<br>
[EP.02 | Gitterchoroplethenkarte](#EP.2)<br>
[EP.03 | Punktrasterkarte](#EP.3)<br>
[EP.04 | Value-by-alpha Mapping](#EP.4)<br>
[EP.05 | Tilemaps](#EP.5)<br>
[EP.06 | Flowmaps](#EP.6)<br>
[EP.07 | Mesh-Daten](#EP.7)<br>
[EP.08 | Animationen in QGIS](#EP.8)<br>
[EP.09 | 3D-Gebäudemodelle](#EP.9)<br>
<br><br>
<a id="EP.1"></a>
<br>
# EP.01 | Dasymetrische Choroplethenkarte (Bevölkerungsverteilung in Berliner Bezierken)  
## *Ergebnis*
![image](https://github.com/timsch-gif/Abschlussprojekt/blob/Abgaben/berlin_bev_Choroplethenkarte.png)

* ***Einfache Choroplethenkarte:*** Bevölkerung von Berlin durch km2.
  
* ***Dasymetrische Choroplethenkarte:*** Bevölkerungszahl zugeschnitten auf tatsächlich bewohntem Gebiet.

## *Arbeitsschritte*
***1. Besorgen der Daten***
* Erst die [Planungsräume Berlins (LOR 2021)](https://www.berlin.de/sen/sbw/stadtdaten/stadtwissen/sozialraumorientierte-planungsgrundlagen/lebensweltlich-orientierte-raeume/) als Shapefile von der Senatsverwaltung herunterladen.
* Anschließend [Einwohnerzahlen](https://www.berlin.de/sen/sbw/stadtdaten/stadtwissen/monitoring-soziale-stadtentwicklung/bericht-2021/tabellen/=) downloaden.
* Datei der Einwohnerzahlen (CSV, Stand Januar 2023) bereinigen (nur Einwohner*innen-Spalten behalten) und als Ganzzahl in Qgis importieren.
  
***2. Erstelle einen Join***
* PLR ID als Ganzzahlspalte in Attributtabelle des Shapefiles anlegen.
* CSV und Shapefile per Attribute verknüpfen.

***3. Einfache Choroplethenkarte***
* Bevölkerungsdichte im Feldrechner berechnen
`"EW" / ($area / 10000)` → Einwohner je Hektar \
Symbolisierung: abgestuft \
Klassifizierung nach Jenks mit Farbverlauf.

***4. Dasymetrische Choroplethenkarte***
* [Corine Land Cover Daten (CLC)](https://land.copernicus.eu/en/technical-library) herunterladen und auf urbane Codes 111 und 112 filtern.
* Mit den Werkzeug *Auflöse* zusammenführen → Urban Fabric.
* Dann durch *Verschneidung* mit LOR-Einwohnern.
* Dichte nur bezogen auf urbane Fläche berechnen.
* Extremwerte prüfen und falls nötig per Hand löschen.
* Symbolisierung: unbewohnte Fläche entfernen.

## *Vorteile*
* Klare Ergebnisse da die Dichte sich nur auf Bebeaute Fläche bezieht und nicht durch unbebaute Flächen Verfälscht wird.
* Man kann Hotspots gut erkennen
* Guter Weg zur Analyse der Fläche

## *Nachteile*
* Es werden viele Daten benötigt wie z.B. LOR, CLC oder Einwohnerzahlen.
* Vereinfacht das Thema schnell zu leicht.

<a id="EP.2"></a>
<br>
# EP.02 | Kleines Einmaleins der thematischen Kartographie | Gitterchoroplethenkarte
## *Ergebnis*
![image](https://github.com/timsch-gif/Abschlussprojekt/blob/Abgaben/Abgaben%20DTM%20SoSe25/Kirschb%C3%A4ume_Berlin_hex_500_layout_hochkant.png)

## *Arbeitsschritte*
***1. Besorgen der Daten***
* Bezirksgrenzen und Baumbestand sind frei als WFS-Layer im [Geoportal Berlin](https://fbinter.stadt-berlin.de/fb/index.jsp) verfügbar.

***2. Nach Baumarten im WFS filtern***
* In den beiden Baum-Layern Kirschbäume per Ausdruck auswählen.
`art_dtsch ILIKE '%kirsche%'`
* Anschließend nur die ausgewählten Baumarten als Punktlayer ins Projekt importieren.

***3. Hexergongitter erstellen***
* Dies geht über: *Vektor* → *Recherchewerkzeuge* → *Gitter erzeugen*: Typ = Hexagon (Polygone), Seitenlänge 500 m (Einheit hier Meter).
* Gitter über die Fläche von Berlin erstellen und mit Stadtgrenze zuschneiden.

***4. Aggregation / räumlichen Join erstellen***
* *Attribute nach Position verknüpfen (Zusammenfassung)*:
* *Ziel* = Hexagon-Grid, Join = Kirschbaum-Punkte, dann Anzahl der Bäume pro Zelle berechnen.

***5. Symbolisierung***
* Am besten eignet sich eine Abgestufte Symboliesierung nach Baumanzahl.
* Hier unterteilt in 7 Klassen nach Jenks.
* Ich habe mich für einen Farverlauf von Rosa zu Lila entschieden.

***6. Drucklayout erstellen***
* Wie gewohnt mit Karte, Kartentitel, Legende, Maßstab, Quellen, Datum und Namen.

## *Vorteile*
