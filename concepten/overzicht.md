# Overzicht

## Inleiding

FIG physical computing system

Een *physical computing systeem* verbindt de fysieke wereld, van materie, energie, krachten en velden, met de informatie-wereld, van data, rekenen, computers en internet. 
Een physical computing systeem heeft als doel om de fysieke wereld te meten en/of te sturen.

Voorbeelden van physical computing vind je in de robotica, zelfrijdende auto's, (slimme) thermostaten, embedded systemen zoals in magnetrons, wasautomaten, printers, enz.
[^note-hci]

[^note-hci]: De interactie tussen mens en computer vindt plaats via de fysieke wereld: sommige sensoren, zoals een drukknop, een luidspreker of een display, zijn eigenlijk gericht op de interactie met mensen, niet op het sturen in de fysieke wereld. Afhankelijk van je doel kan dit wel of niet onder physical computing vallen.

De belangrijkste onderdelen van een physical computing system zijn *sensoren*, *actuatoren*, en de *controller(s)*.

Een **sensor** zet een fysisch verschijnsel om in informatie.
Voorbeelden van sensoren zijn: temperatuursensor, drukknop, accelerometer (versnellingssensor), afstandssensor, microfoon, camera.

Een **actuator** zet informatie om in een fysisch verschijnsel.
Voorbeelden van actuatoren zijn: allerlei soorten motoren, klep, luidspreker, lamp, display.

Een **controller** is een computer (in een physical computing system) die de invoer uit de sensoren verwerkt en op basis daarvan de actuatoren aanstuurt.
Een controller **communiceert** vaak met andere informatiesystemen, bijvoorbeeld via een radioverbinding. Deze communicatie kan gebruikt worden voor het versturen van waarnemingen (sensorgegeven) en voor het ontvangen van stuurinformatie.

## Over signalen en events

In de besturingssoftware van een controller hebben we te maken met *signalen* en *events*, als invoer van de sensoren, en als uitvoer naar de actuatoren. Ook in de communicatie kom je signalen en events tegen.

Een **signaal** heeft op elk moment een waarde. Een voorbeeld van een signaal is het verloop van de temperatuur in de tijd; of het signaal van een accelerometer (versnellingssensor) zoals dat in de tijd verloopt.

Een **event** heeft alleen een waarde op een enkel, ondeelbaar moment. Een voorbeeld van een event is het indrukken van een drukknopschakelaar, of het schudden van de microbit.

Een signaal kun je als fysiek verschijnsel zien, bijvoorbeeld in de vorm van een elektrische spanning of stroom.
Maar je kunt het ook zien als een informatie-verschijnsel: dan spreek je alleen over getalwaarden. In de besturingssoftware hebben we alleen te maken met deze getallen.

Deze getallen kunnen een bepaald fysieke grootheid representeren, bijvoorbeeld een temperatuur, een versnelling, of een lichtsterkte. Je kunt een getal omrekenen in de fysieke eenheid van die grootheid, zoals graden Celcius, m/s2, of lumen.

### Verbinding tussen sensoren, actuatoren en controller

De verbinding tussen een sensor of een actuator en de controller kan op verschillende manieren plaatvinden: dit kan een analoog (elektrisch) signaal zijn, of een digitaal (elektrisch) signaal, soms in de vorm van een complex protocol zoals {term}`I2C` over een paar draden. In dit materiaal zien we de verbinding tussen sensor of actuator en controller als een *toevallige implementatie-keuze*: deze is niet van fundamenteel belang voor de fysische wereld, en ook niet voor de manier waarop je de besturingssoftware ontwerpt.

### Analoge en digitale signalen

We beschouwen zoals gezegd, signalen zoals deze in de besturingssoftware voorkomen: een signaal bestaat dan uit een reeks getallen die de waarden in de loop van de tijd voorstellen. 

* een digitaal signaal heeft op elk moment een waarde 0 of 1;
* een analoog signaal heeft op elk moment een waarde uit een groter bereik, typisch tussen 0..1023 (10 bits). Dit analoge signaal kan ook omgerekend worden naar de gebruikelijke fysieke eenheden, zoals graden Celcius voor temperatuur, of graden of radialen voor een hoekverdraaiing.

We gebruiken dezelfde terminologie voor de sensoren en actuatoren: een sensor die een analoog signaal in de besturingssoftware geeft, noemen we een analoge sensor; een sensor die een digitaal signaal in de besturingssoftware geeft, noemen we een digitale sensor.

(Zoals gezegd kan dit analoge signaal vanuit de sensor in digitale vorm naar de controller gecommuniceerd worden: dat maakt voor de verwerking in de besturing niet uit. Elders heet een analoge sensor met een digitale communicatie ook wel een digitale sensor, maar die terminologie gebruiken we hier niet.)

### Signaalbesturing: signaal(en) in, signaal(en) uit

FIG signaal in - signaal uit

Een eenvoudige vorm van besturing is wanneer je een input-signaal direct omrekent naar een output-signaal.

Een digitaal voorbeeld is de drukknop die direct een LED aanstuurt: alleen als de knop ingedrukt is, brandt de LED. De digitale waarde van de drukknop (als digitale sensor) wordt gekopieerd naar de output voor de digitale aansturing van de LED (aan of uit).

```Python
    button_value = button_a.is_pressed()
    led.write_digital(button_value)
```

Een analoog voorbeeld is de LED-dimmer met {term}`potmeter`: met de potmeter stel je het lichtniveau in. De analoge waarde van de potmeter (analoge sensor) wordt direct omgerekend in het analoge niveau voor de LED (analoge actuator).

```Python
    level = potmeter.read_analog()
    led.write_analog(level)
```

In het geval van analoog in - analoog uit moet de signaalwaarde soms omgerekend worden, bijvoorbeeld van het bereik van een potmeter (0..1023) naar het bereik van een servo (25..125). Als het om een lineair verband gaat, kun je hiervoor de volgende formule gebruiken:

$$(x - in_{min}) * (out_{max} - out_{min} / (in_{max} - in_{min}) + out_{min}$$

De waarde `x` met als bereik `in_min .. in_max` wordt afgebeeld op het bereik `out_min .. out_max`. 

(In de Arduino-context gebruik je daarvoor de functie `map`.)

Deze eenvoudige besturing kun je gebruiken als je het effect van de actuator in de fysieke omgeving goed kunt voorspellen, zoals bijvoorbeeld bij een LED of bij een servo. Als dat niet het geval is, bijvoorbeeld door verstoring van de omgeving, kun je een *feedback-besturing* gebruiken.

#### Feedback-regelaar

FIG feedback-regelaar

In de feedback-besturing gebruik je twee input-signalen, en één output-signaal. Het ene input-signaal is de ingestelde waarde: het effect in de fysieke omgeving dat je wilt bereiken. Het andere input-signaal komt van een sensor die het actuele effect in de fysieke omgeving meet. Als die twee verschillen, stuur je via het output-signaal de actuator aan.

Voorbeeld: een (verwarmings)thermostaat heeft twee inputs: een ingestelde temperatuur, en een gemeten temperatuur; als de gemeten temperatuur lager is dan de ingestelde temperatuur, wordt de actuator voor de verwarming aangestuurd. De verwarming wordt weer uitgezet als de ingestelde temperatuur bereikt is.

Voor het aansturen van de actuator (hier: de verwarming) heb je twee mogelijkheden: een *aan/uit regeling* (ook wel een bang-bang regeling genoemd); of een *proportionele regeling* (voor een "modulerende verwarming"). In het laatste geval kun je de hoeveelheid warmte (of dergelijke) per tijdseenheid regelen. Als het verschil tussen de gemeten temperatuur en de ingestelde temperatuur groot is, laat je de verwarming meer warmte leveren; als dit verschil klein is, minder.

Een ander voorbeeld van een feedback-regeling vind je bij een lijnvolger van een robot: als de lijn links van het midden van de robot is, stuur je de robot naar rechts; als de lijn rechts van het midden van de robot is, stuur je naar links. Ook hier heb je weer de mogelijkheden van een aan-uit regeling en van een proportionele regeling. In dat laatste geval heb je wel een sensor nodig die bepaalt hoe ver de lijn van het midden af is.

Een veel gebruikte vorm van een proportionele feedback-regeling is de *PID-regelaar*: in dat geval gebruik je niet alleen de actuele sensorwaarden, maar ook de sensorwaarden en de instelwaarde(n) uit het verleden, voor een soepele regeling. (Zie: https://nl.wikipedia.org/wiki/PID-regelaar.)


## Event-besturing

Naast signalen heb je in de besturingssoftware te maken met events. Zoals gezegd: een event heeft alleen een waarde op een enkel, ondeelbaar moment.

Voorbeelden van events zijn: het indrukken van een knop, een stap (in het geval van een stappenteller), het ontvangen van een radiobericht, het maken van een bepaald gebaar (gesture) zoals het schudden van de microbit. Daarnaast kunnen we intern (in de controller) events genereren, bijvoorbeeld *timer-events*. 

In de event-besturing *koppel je een event aan een actie*. Deze actie kan bijvoorbeeld een output-waarde instellen, een timer ("kookwekker") starten, en zorgen voor de overgang naar een andere toestand (zie verderop).

In de aan/uit regeling voor de LED gebruik je de event van het indrukken van knop A voor het aanzetten van de LED; en het indrukken van knop B, voor het uitzetten van de LED.

FIG event -> actie

Voor het koppelen van een event aan een actie gebruik je in Python de `if` (conditionele opdracht): als de event opgetreden is, voer dan de actie uit. De functie `button.was_pressed()` is één van de event-functies in microbit Python.

```Python
    if button_a.was_pressed():
        led.digital_write(1)
    if button_b.was_pressed():
        led.digital_write(0)
```

In microbit Python zijn een aantal event-functies voorgedefinieerd, bijvoorbeeld voor de knoppen A en B, en voor de accelerometer. In andere gevallen moet je de *event detecteren* met een speciale voorwaarde, zoals in het geval van een timer-event, of van de event van het indrukken van een externe knop.

## Toestandsdiagram

Bij complexere besturingen worden events gecombineerd met een *toestand*. Een dergelijke besturing beschrijven we grafisch in de vorm van een *toestandsdiagram*. Dit bestaat uit een (eindig, meestal klein) aantal (benoemde) toestanden, getekend als cirkels, en overgangen tussen die toestanden, in de vorm van pijlen tussen de cirkels. Een overgang is *gelabeld* met een input-event en met een actie. Een pijl van toestand P naar toestand Q, gelabeld met event E en actie A betekent: als in toestand P event E optreedt, voer dan actie A uit en ga naar toestand Q. Eén van de toestanden is de *begintoestand*, aangegeven door een enkele ongelabelde inkomende pijl.

:::{figure} ../figs/led-knoppen-dimmer.drawio.png
:width: 500

Toestandsdiagram voor een LED-dimmer met knoppen.
:::

Je kunt de besturing ontwerpen als toestandsdiagram, en daarna op een systematische manier vertalen in Python-code, zie: [](#toestandsdiagrammen).

In een toestandsdiagram kun je allerlei soorten input-events gebruiken; in het bijzonder kun je ook timer-events als input gebruiken, voor het "triggeren" van een toestandsovergang.

## Communicatie

Een controller kan communiceren met andere informatie-systemen, bijvoorbeeld via een radio, of bedraad. In het geval van de microbit kun je communiceren via de seriële verbinding (via USB) met de host-computer; en via de pakket-radio met andere microbits.

Het ontvangen van een (radio)bericht kun je beschouwen als een event, waaraan je de verwerking van het bericht als actie koppelt.

## Structuur van een besturingsprogramma

Een besturingsprogramma (in microbit Python) heeft de volgende structuur:

```Python
import ... gebruikte libraries, modules

...lokale definities (functies, variabelen)
...initialisatie van variabelen en sensoren/actuatoren (toestand, outputs)

while True:  # de besturingslus
    ...lezen en schrijven van signalen
    ... event-condities en bijbehorende acties
```

De niet-eindigende herhaling `while True: ...` vormt de *besturingslus*: de opdrachten in deze lus worden herhaald totdat je de controller (microbit) reset of uitzet.
De opdrachten vóór de besturingslus worden eenmalig uitgevoerd: deze vormen de *initialisatie*.

*(Voor hulp bij Python-constructies verwijzen we in eerste instantie naar de microbit Python editor. T.z.t. wordt dit materiaal aangevuld met een Python-aanhangsel.)*

