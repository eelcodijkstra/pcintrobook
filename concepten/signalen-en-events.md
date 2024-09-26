(h-signalen-en-events)=
# Signalen en events

Het resultaat van een sensor kan een *signaal* zijn of een *event*.
Ook het aansturen van een actuator kan via een signaal of een event.

- **Een signaal heeft op elk moment een waarde.**
- **Een event heeft alleen een waarde op een bepaald ("ondeelbaar") moment.**

Voorbeeld: in de figuur zie je het signaal van een drukknop, als functie van de tijd: dit signaal is laag (0) als de drukknop niet ingedrukt is, en hoog (1) zolang de drukknop ingedrukt is.
Het indrukken van de drukknop is een event; dit vind je in het signaal als de overgang van 0 naar 1.
(Het loslaten van de drukknop zou je ook als event kunnen zien: dat is de overgang van 1 naar 0.)

In micro:bit Python zijn er twee verschillende functies voor de drukknoppen A en B:

- `button_a.is_pressed()` - geeft de huidige waarde van het signaal
- `button_a.was_pressed()` - geeft aan dat er een "button event" geweest is sinds de vorige aanroep van deze functie.

In de opdrachten zie je het verschil tussen deze beide:

- [led met afzonderlijke aan- en uitknop](#opdr-led-aan-uit-knoppen)
- [led met enkele aan- en uitknop](#opdr-led-enkele-aan-uit-knop)

## Digitale signalen

Een *digitaal signaal* heeft twee verschillende waarden: 0 of 1.

In het elektrische domein gebruik je meestal 0V voor 0, en 3V (of 5V) voor 1.

## Analoge signalen

## Detecteren van een event in een signaal




* signaal
    * heeft op elk moment een waarde
    * analoge signalen (ook: bemonsterde, gediscretiseerde analoge signalen)
        * analoog niveau (bij uitvoer); PWM
        * input: analoog-digitaal conversie (beperkt aantal bits; bemonstering: periode, niveaus)
    * digitale signalen (binair)
    * voorbeeld: het signaal van een accelerometer
* event
    * heeft alleen een waarde op een bepaald ("ondeelbaar") moment
    * voorbeeld: het indrukken van een knop (of: het weer loslaten...)
* herkennen van events in signalen; bijvoorbeeld: stappen herkennen in het signaal van een accelerometer (versnellingssensor)
    * of, van een hartslag in een ECG
    * eenvoudig: van het indrukken van een knop, in het digitale signaal van die input

In het algemeen zijn events belangrijk voor de software: de software moet daarop reageren.
(Events zijn min of meer verbonden aan toestanden: een event zorgt voor een verandering van de toestand. Denk aan het indrukken van een schakelaar om het licht aan of uit te doen.)

Ander voorbeeld: event van temperatuur die onder of boven een bepaalde grens komt. Dit is aanleiding om de CV aan of uit te schakelen.

Systeem voor het verwerken van signalen (zonder events) - bijvoorbeeld een proportionele regeling. (Of, in een algemener geval, een PID regeling: met integratie en differentiatie)




 


