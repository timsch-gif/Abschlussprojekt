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
![image](https://github.com/timsch-gif/Abschlussprojekt/blob/Abgaben/berlin_bev_Choroplethenkarte.png)
## *Ergebnis*
***Arbeitsaufgabe:***\
Erstellen Sie bitte im A3-Format ein gutaussehende Karte zur Bevölkerungsdichte Berlins, welche die Choroplethenmethode in der Standardvariante einer dsymetrischen Choroplethenkarte gegenüberstellt. Laden Sie das Ergebnis als .pdf auf Moodle hoch.\

* ***Einfache Choroplethenkarte:*** Bevölkerung von Berlin durch km2.
  
* ***Dasymetrische Choroplethenkarte:*** Bevölkerungszahl zugeschnitten auf tatsächlich bewohntem Gebiet.

## *Arbeitsschritte*
1.	Datenbeschaffung – Das Shapefile der Planungsräume Berlins ([LOR 2021](https://www.berlin.de/sen/sbw/stadtdaten/stadtwissen/sozialraumorientierte-planungsgrundlagen/lebensweltlich-orientierte-raeume/)) sowie die Einwohnerzahlen ([CSV, Stand 1/2023](https://www.berlin.de/sen/sbw/stadtdaten/stadtwissen/monitoring-soziale-stadtentwicklung/bericht-2021/tabellen/)) wurden von der Berliner Senatsverwaltung heruntergeladen.
2.	Aufbereitung der CSV – Überflüssige Kopfzeilen und Spalten wurden in Excel entfernt; 1000er Trennpunkte deaktiviert; beim Import nach QGIS erhielten sowohl PLR Nummer als auch Einwohnerzahl den Datentyp Ganzzahl.
3.	Join – Mit „Attribute nach Feldwert verbinden“ wurden die Einwohnerzahlen an die PLR Geometrien angefügt. Damit war der Layer für die einfache Choroplethenkarte vollständig.
4.	Klassifizierung & Layout – In den Layereigenschaften wurde EW / ($area / 10 000) als Ausdruck hinterlegt, Jenks Klassen gewählt und Farben angepasst; Anzahl, Grenzwerte und Legende wurden manuell verfeinert.
5.	Dasymetrische Schritte:
* Filtern der Corine Daten auf Code_18 = 111 OR 112 mittels „Nach Ausdruck extrahieren“.
* Auflösen zu einer einzigen Urban Fabric Fläche.
* Verschneidung dieser Fläche mit dem mit Einwohnerzahlen angereicherten PLR Layer, sodass jeder bebaute Polygonteil seine Einwohnerzahl erbte.
* Neuberechnung von Fläche und Dichte in einer neuen Spalte.
* Symbolisierung: unbewohnte Teile grau, bewohnte Teile als abgestufte Choroplethenkarte; Stil des einfachen Layers wurde kopiert und neu klassifiziert.
