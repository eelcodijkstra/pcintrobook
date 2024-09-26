# Rest

Dit bestand bevat paragrafen die elders verwijderd zijn, omdat ze daar niet pasten. Ik moet controleren of deze inhoud nog ergens ondergebracht moet worden, of dat deze gewoon weg kan.

## Sturen

### Onderdelen van een controller

De controller is een computer met de volgende onderdelen:

* programmageheugen, met daarin het besturingsprogramma;
* werkgeheugen (RAM), om de tussenresultaten van berekeningen te bewaren;
* achtergrondgeheugen, voor het *persistent* bewaren van gegevens (bijvoorbeeld: Flash geheugen);
    * vaak worden het programmageheugen en het achtergrondgeheugen gecombineerd
* een rekeneenheid (CPU): deze voert het programma uit
* aansluitingen voor invoer en uitvoer van sensoren en actuatoren, en voor communicatie met de buitenwereld.

Een controller verschilt van een "normale" computer vooral door het soort en aantal aansluitingen voor invoer en uitvoer.
Bovendien voert een controller meestal maar één (besturings)programma uit, waardoor het geheugen veel kleiner kan zijn dan dat van een algemeen bruikbare computer.

### Samenvatting?

* directe input-output relatie (signaal)
    * vb: schakelaar - LED (aan/uit) of motor (aan/uit) 
    * vb: potmeter - LED (helderheid) of motor (snelheid)
* gebruik van events
    * vb: afzonderlijke schakelaar voor aan- en uitzetten van LED of motor
    * (je hebt dan geen toestand nodig; alleen input- en output-events; output blijft staan...)
    * (
* gebruik van events en toestand
    * vb: een enkele schakelaar voor aan- en uitzetten - LED of motor)
    * vb: twee schakelaars voor dimmer (LED), snelheidsregeling (motor)

### Aansluitingen

Voor het aansluiten van sensoren en actuatoren op een microcontroller gebruik je de input- en output-pinnen.
Soms ligt de functie van een pin vast, soms kun je deze instellen in de software.

https://tech.microbit.org/hardware/edgeconnector/

### Inputs

Een microcontroller heeft een aantal inputpinnen voor het aansluiten van sensoren.

* digitale inputs, voor een digitale sensor zoals een schakelaar.
* analoge inputs, voor een analoge sensor zoals een potmeter (meten van draaiing). De analoog-dgitaalomzetter zet de analoge spanning op deze input om in een getal. (Zie A/D conversie).

Soms heeft een sensor een combinatie van input en output nodig, zoals een ultrasoon afstandssensor.

Daarnaast kun je ingewikkelder sensoren aansluiten via een *serieel protocol*, zoals I2C of SPI.

Voorbeeld: microbit-pinnen:

Zoals je ziet hebben sommige pinnen een vaste functie, terwijl andere pinnen meerdere functies kunnen hebben.
In de software geeft je dan aan hoe je die pin gebruikt.

Je moet altijd rekening houden met de *elektrische eigenschappen* van de pinnen: een pin kan maar een beperkte spanning of stroom verwerken. In het geval van de microbit: 3.3V als maximale (input) spanning, en 5mA als maximale stroom.
Als je een pin buiten de specificaties gebruikt, kan de microcontroller onherstelbaar beschadigd raken.

(Als je een *inductieve belasting* zoals een luidspreker, motor of relais direct op een pin aansluit kun je deze overbelasten, door de hoge spanningspieken die het schakelen daarvan kan geven.)

### Outputs

* signalen (bemonstering? timing?)
* digitale output (event of signaal)
* analoog output-niveau: PWM (event, bij instellen, overgang))
* analoge output (signaal)