# Begrippenlijst

:::{glossary}

periode
: kleinste deel van een {term}`periodiek signaal` dat steeds herhaald wordt.

frequentie
: de frequentie van een {term}`periodiek signaal` is het omgekeerde van de {term}`periode` $T$: frequentie $f = 1/T$.

periodiek signaal
: {term}`signaal` waarin dezelfde signaalvorm steeds herhaald wordt; zie ook {term}`periode` en {term}`frequentie`. Een *sinus*signaal is een voorbeeld van een periodiek signaal.

signaal
: **een signaal heeft op elk moment een waarde**. Een *digitaal signaal* kan twee waarden aannemen (0 en 1). Een *analoog signaal* kan meerdere waarden aannemen, bijvoorbeeld een waarde in het bereik 0..1023, als resultaat van `pin.read_analog()`.

event
: **een event heeft alleen een waarde op het (ondeelbare) moment dat deze event optreedt**. Het indrukken van een knop is een voorbeeld van een event.

initialisatie
: het deel van een (besturings)programma dat eenmalig uitgevoerd wordt, voordat de besturingslus (`while True:`) begint.

besturingslus
: het deel van een besturingsprogramma dat voortdurend herhaald wordt (`while True:`), totdat de controller uitgezet of gereset wordt.

idempotent
: een actie is *idempotent* als het niet uitmaakt of deze één keer of meerdere keren achter elkaar uitgevoerd wordt. Een voorbeeld is een schakelaar met aparte drukknoppen voor "aan" en "uit": het maakt niet uit of je de aan-knop eenmaal indrukt of meerdere keren achter elkaar. (Ook het verversen van een pagina in de browser is *idempotent*, behalve als die pagina een formulier bevat.)

one-shot timer
: een timer die uitgeschakeld wordt nadat deze afgelopen is; in tegenstelling tot een {term}`periodieke timer` die steeds voor de volgende periode ingesteld wordt.

periodieke timer
: een timer die nadat deze afgelopen is weer ingesteld wordt voor de volgende periode. Deze timer is dus altijd actief.

pulse width modulation
: (PWM) een periodiek digitaal signaal met een bepaalde verhouding tussen de "1" tijd en de "0" tijd. Deze *duty cycle* wordt uitgedrukt als de verhouding tussen de "1" tijd en de hele periode, als percentage. De Python opdracht `pin0.write_analog(level)` stelt een PWM-signaal in voor `pin0`, waarbij `level` een getal is tussen 0..1023; 1023 komt overeen met een duty cycle van 100%.

PWM
: zie {term}`pulse width modulation`

sensor
: een sensor zet een fysiek verschijnsel om in informatie

actuator
: een actuator zet informatie om in (de sturing van) een fysiek verschijnsel.

servo
: servo-motoren zijn er in twee soorten: 180 graden servo's, om te sturen. Deze kunnen draaien over een hoek van 0..180 graden. De hoek geef je op met een PWM-signaal. En 360 graden servo's, soms voorzien van een wiel: deze kun je gebruiken om een robotkarretje aan te drijven. De snelheid linksom of rechtsom geef je op met een PWM-signaal.

signaal-sturing
: bij signaal-sturing wordt een invoer-signaal omgerekend naar een uitvoer-signaal.

event-sturing
: bij event-sturing wordt een invoer-event verwerkt wat uiteindelijk resulteert in een uitvoer-event of een uitvoer-signaal. Een event kan ook resulteren in een toestandsovergang, waardoor de betekenis van de volgende event(s) kan veranderen.

I2C
: I2C is een protocol voor de communicatie tussen een controller en de "randapparaten" daarvan, zoals sensoren en actuatoren. Deze communicatie gebruikt 2 verbindingen: SDA (seriële data; een twee-richtingsverbinding) en SCL (seriële clock). Een verbinding met een sensor of actuator heeft daarnaast nog een voedingsspanning (Vcc) en een "aarde" (GND) nodig, in totaal 4 draden.) Dit is een busverbinding waar meerdere randapparaten op dezelfde draden aangesloten kunnen worden.

potmeter
: een potmeter is een analoge sensor waarvan de waarde afhangt van de hoek waarover de as verdraaid is. Soms wordt dit ook een "rotatiesensor" genoemd. Technisch gezien is het een weerstand met *variabele aftakking*. Je vindt een potmeter bijvoorbeeld als volumeregelaar van een versterker.

blokkerende opdracht
: een opdracht die een grote hoeveelheid tijd in beslag kan nemen waarbij de controller niet in staat is andere opdrachten uit te voeren. Een voorbeeld hiervan is de `sleep(duration)` opdracht. Hierbij is het systeem tijdelijk "doof" voor input, bijvoorbeeld sensor-events of radio-berichten. Door het gebruik van blokkerende opdrachten kunnen de timing-eisen van het systeem in gevaar komen. Door het gebruik van (timer)events kunnen deze blokkerende opdrachten vermeden worden (ten koste van een wat ingewikkelder programma). Andere voorbeelden van blokkerende opdrachten zijn: het lezen van een bestand van achtergrondgeheugen; het raadplegen van een database; het wachten op een respons van een internet-server.

:::