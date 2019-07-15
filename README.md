# de-voetgangerskaart
Actuele gegevens over voetgangers.

## toelichting
De voetgangerskaart is een verzameling van gegevens rondom voetgangers. Het bestaat uit een QGIS-project en uit een (opzet voor) gegevens. De voetgangerskaart helpt om inzicht te krijgen in welke informatie we rondom voetgangers willen weten.

## gegevens
De voetgangerskaart bevat bestaande gegevens en afgeleide gegevens. 
De volgende entiteiten zijn beschikbaar:

* basisgegevens (Voetgangerskaart_basisgegevens.gpkg):
  * wegdelen_agg
  * voetgangerswegdelen
* indicatoren per voetgangerswegdeel (Voetgangerskaart_indicatoren.gpkg):
  * stoepbreedtes_bruto
  * voetgangerswegdelen_indicatoren
* indicatoren per gebied (Voetgangerskaart_per_gebied.gpkg):
  * Voetgangers_per_CBS_buurt
  * Voetgangers_per_CBS_wijk
  * Voetgangers_per_TIR_subbuurt
  * Voetgangers_per_1ha_hexagon
  
### basisgegevens
#### wegdelen_agg
Wegvakonderdelen uit de BOR, samengevoegd op straatcode + segmentID.

Een segment bestaat uit alle aan elkaar grenzende wekvakonderdelen met dezelfde straatcode. Alle wegdeeltypes zijn meegenomen, dus ook bijvoorbeeld 'Berm verhard'.

#### voetgangerswegdelen
Bruto beschikbare ruimte voor voetgangers.

Als bron zijn de wegdelen uit de BOR gehanteerd. Bruto houdt in dat obstakels, zoals fietstrommels, installatiekasten, etc. hier nog niet van zijn afgetrokken.

Alle voetgangerswegdelen zijn gerelateerd aan de wegdeelsegmenten in wegdelen_agg (zie hierboven). De voetgangerswegdelen hebben in de BOR een waarde voor 'lengte'. Deze waardes zijn per straatcode + segment gesommeerd. Bijvoorbeeld: als een wegsegment aan beide kanten een stoep heeft met 10 meter lengte, dan wordt 20 meter geretourneerd als totale stoeplengte bij dat segment.

### indicatoren per voetgangerswegdeel
#### stoepbreedtes_bruto
Beschikbare stoepbreedtes, op basis van bruto beschibare ruimtes voor voetgangers, ingedeeld in breedteklassen.

De volgende klassen zijn gehanteerd (in meters):

* `> 3.60`
* `2.90 - 3.60`
* `2.20 - 3.60`
* `1.80 - 2.20`
* `0.90 - 1.80`
* `< 0.90`

Elke stoepbreedte is gerelateerd aan een wegdeelsegment (zie wegdelen_agg hierboven).

#### voetgangerswegdelen_indicatoren
Voetgangerswegdelen met per straatcode + segmentID een aantal indicatoren:
* aantal bomen
  * Het aantal bomen op en binnen 2 meter van het (gehele) wegdeel waar het voetgangerswegdeel deel van uitmaakt. 
  * Het aantal bomen per 100 m voetgangerswegdeel.
* aantal banken
  * Het aantal banken op en binnen 2 meter van het (gehele) wegdeel waar het voetgangerswegdeel deel van uitmaakt.
  * Het aantal banken per 100 m voetgangerswegdeel.
* aantal voordeuren
  * Het aantal verblijfsobjecten op en binnen 10 meter van het (gehele) wegdeel waar het voetgangerswegdeel deel van uitmaakt.
  * Het aantal verblijfsobjecten per 100 m voetgangerswegdeel.

Voor het aantal voordeuren is aangenimen dat een voordeur overeenkomt met een adres in de het Adreslocatiebestand (ALB). De gegevens zijn niet geschikt om de druk op het voetgangerswegdeel te bepalen; een groot appartementencomplex kan bijvoorbeeld slechts 1 hoofdadres hebben. Deze gegevens zeggen iets over de levendigheid van de gevelwand. 

### indicatoren per gebied
De indicatoren zijn ook naar de volgende gebieden geaggregeerd:
* CBS-wijk
* CBS-buurt
* TIR-subbuurt
* 1ha-hexagons


## QGIS project
Het QGIS-project visualiseert de beschikbare voetgangersgegevens en geeft een opzet voor een structuur voor toekomstig toe te voegen gegevens.

De legenda is ingedeel in de volgende groepen:

* 'Aanbod - Beschikbare Ruimte'
* 'Vraag - Benodigde Ruimte'
* 'Toekomstige Vraag - Benodigde Ruimte'
* 'Basis'

De groep '**Aanbod - Beschikbare Ruimte**' bevat, per voetgangerswegdeel en op gebiedsniveau, gegevens over de beschikbare ruimte en aantrekkelijkheid voor voetgangers.

De groep '**Vraag - Benodigde Ruimte**' is bedoeld voor gegevens rondom de vraag van voetgangers op de beschikbare ruimte. Die vraag kan berekend zijn aan de hand van modellen, maar de vraag kan ook feitelijk geconstateerd zijn; bijvoorbeeld door tellingen uit te voeren.

De groep '**Toekomstige Vraag - Benodigde Ruimte**' is bedoeld voor voorspellingen over de voetgangersvraag in de toekomst. Bijvoorbeeld de uitwerking van extrapolaties, what-if-scenario's etc.

De groep '**Basis**' bevat basisgegevens op basis waarvan de gegevens rondom vraag en aanbod zijn gebaseerd. Bijvoorbeeld de wegdelen die voor voetgangers bedoeld zijn, de locatie van bomen, bankjes, attractiepunten, etc.
