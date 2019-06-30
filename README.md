<img src="https://raw.githubusercontent.com/tamedia-ddj/brennpunkt_bauernhof_public/master/files/Bauernhof_Logo.jpg">

# Brennpunkt Bauernhof
## Analyse des Datenbestandes zu den Direktzahlungen 2014 bis 2017

Ein Rechercheteam von Tamedia veröffentlich diese Woche eine Serie von Artikeln zur Landwirtschaft. Es wurden dazu Daten über Direktzahlung sowie über 600 Strafurteile gegen Landwirte ausgewertet.

In den vorliegenden Notebooks sind die relevanten Ausschnitte der Analyse dokumentiert. Der beiliegende Datensatz wurde zur Wahrung des Datenschutzes gekürzt und verändert (Gemeinde, Kantone und Zahlenwerte wurden willkürlich vertauscht).




0. [Datenvorbereitung](https://github.com/tamedia-ddj/brennpunkt_bauernhof_public/blob/master/0_Data_Preparation.ipynb)
1. Kürzungen
	* Methodik: [GitHub](https://github.com/tamedia-ddj/brennpunkt_bauernhof_public/blob/master/1_Kuerzungen.ipynb)
    * Artikel:
        * [Skandalöse Zustände auf Schweizer Bauernhöfen](https://www.tagesanzeiger.ch/schweiz/brennpunkt-bauernhof/skandaloese-zustaende-auf-schweizer-bauernhoefen/story/17687029)
        * [Sogar Tierquäler erhalten Subventionen](https://www.tagesanzeiger.ch/schweiz/brennpunkt-bauernhof/bauern-erhalten-subventionen-trotz-leidender-tiere/story/19918846)


Quelle des Datensatzes: BLW

---

#### 1. Datenvorbereitung
Der Datensatzes der 213'259 Direktzahlungen in den Jahren 2014 bis 2017 wird in einem ersten Schritt zur späteren Untersuchung aufbereitet. Variablen ohne Informationsgehalt werden entfernt und neue berechnet (z.B. die Summe aller Direktzahlungen, inkl. Ganzjahres- und Sömmerungsbetriebe).

Zudem wird eine konsistente Liste aus Gemeinde-IDs, Gemeinden und Kantonen erstellt (Variablen `GDE_GEMEINDE_NR`, `GDE_NAME` und `ABJ_KANTON`). Aus administrativen Gründen ist die Verbindung von `GDE_NAME` und `ABJ_KANTON` im gelieferten Datensatz nicht durchgehend korrekt. Um Fehler zu vermeiden, wir in den folgenden Notebooks die hier erstellte Liste `clean_gde` als Referenz-Tabelle herbeigezogen.


Ein Ausschnitt aus den ersten beschreibende Statistiken liefert ein Bild über die Verteilung und Entwicklung der Direktzahlungen und der Merkmale der begünstigten Bauernbetrieben.



#### 2. Kürzungen

Das Notebook zum Thema *Kürzungen* stellt die verteilten Direktzahlung in Relation zu den ausgesprochenen Reduktionen. Dazu werden die wichtigsten Kennzahlen ermittelt:

* Anzahl Betriebe die Direktzahlungen erhalten haben (Gesamt und für die aktuellste Periode)
* Anzahl Betriebe die Kürzungen erhalten haben (Gesamt und für die aktuellste Periode)
* Summe aller ausgesprochenen Kürzungen
* Anzahl Betriebe die mehrmals Kürzungen hinnehmen mussten (1,2,3 oder 4-Mal)

Zur späteren Visualisierung werden Tabellen mit Kennzahlen auf Gemeindeebene erzeugt. Die in der Tabelle `cutbacks_gde` werden folgende Variablen berechnet:

Variable | Beschreibunng
--- | --- 
`KUERZUNGEN` | Anzahl Kürzungen auf Gemeindeebene
`BETRIEBE_TOTAL` | Anzahl Betriebe auf Gemeindeebene
`KUERZUNGEN_ANTEIL` | Prozentualer Anteil der Betriebe die Kürzungen erhalten haben
`KUERZUNGEN_BETRAG_AVG` | Durchschnittliche Höhe der Kürzungen pro Gemeinde


In der Tabelle `cutbacks` werden auf Ebene der Gemeinde die Anzahl der Betriebe ermittelt, bei denen in 3 oder mehr Jahren (von insgesamt 4 Jahren) Kürzungen veranlasst wurden. Während des Exportprozesses wird der Spalte `multiple_cutbacks` die Anzahl Betriebe hinterlegt, die diese Bedingungen erfüllen.

Um die korrekten Gemeinden- und Kantons-Bezeichungen zu erhalten, wird für beide Tabelle die in Punk 1 erstellte Tabelle `clean_gde` herbeigezogen. Zudem wird eine Bereinigung der Gemeindenamen mit der Funktion `remove_kte()` durchgeführt. Damit werden konsistent alle Kantonsbezeichnungen aus dem Gemeindenamen entfernt.

Beide Tabllen werden zur weiteren bearbeitung als csv-Datei exportiert. 





