# Servo-motoren

Er zijn twee soorten servo-motoren: 180 graden servo's om te sturen, en 360 graden servo's die je kunt gebruiken als aandrijving. We behandelen eerst de 180 graden servo en daarna de 360 graden servo.
De 180 graden servo is de meest voorkomende variant. Als er verder niets bij staat, wordt die versie bedoeld.

Met een 180 graden servo-motor kun je sturen, bijvoorbeeld het roer en de zeilen bedienen van een radiografisch bestuurbare zeilboot; of de roeren van een radiografisch bestuurbaar vliegtuig.
Zo'n servo kunt je maar over een beperkte hoek draaien, maximaal 180 graden (een halve draai).
Bij deze servo krijg je vaak allerlei opzetstukjes om de servo aan een roer of iets dergelijks te verbinden.

```{figure} ../figs/octopus-servo.png
:width: 300
:align: center

180 graden servo met opzetstukjes
```

Je kunt met een servo allerlei dingen besturen. Een voorbeeld is de bekende melkpak-monster-robot:

:::{iframe} https://www.youtube.com/embed/egl3fNAYylk?si=SYPxlMXgJgbjJm_X
:width: 100%

Melkpad-monster met servo bovenin voor de beweging van de bek.
:::

Een servo heeft 3 aansluitingen:

- 0V (GND) - bruin (in plaats van zwart)
- 3V ("power") - rood
- signaal - oranje (in plaats van geel)

Voor het aansturen van een servo heb je maar 1 (signaal)pin nodig; de andere aansluitingen zijn voor de "power" van de servomotor.

Soms heeft een servo een hogere spanning nodig dan de 3.3V van de microbit, bijvoorbeeld 5V. Ook moet de spanningsbron moet altijd **voldoende stroom** kunnen leveren voor de servo: het kan dan handig zijn, zeker als je meerdere servo's gebruikt, om een bordje te gebruiken met aparte servo-aansluitingen. Bovendien moet je dikke en/of korte aansluitdraden gebruiken voor de servo: ansders gaat er teveel energie in de draden verloren voor een betrouwbare werking van de servo. (Zie ook de website van Hans de Jong.)

## Servo-motoren: PWM besturing

Een servo stuur je aan met een {term}`PWM` signaal; dat is de signaalvorm die je krijgt bij `pin.write_analog()`.
De {termm}`periode` voor de servo moet 20 ms zijn. Met de duty-cycle stel je de hoek van de servo in, volgens de tabel hieronder. 90 graden is de middenstand.

| pulsbreedte | hoek | analoog uit |
| :----------: | :--: | :----------: |
|      0.5 ms |  0   |    25 |
|        1 ms |  45  |    50 |
|      1.5 ms |  90  |    75 |
|        2 ms | 135  |   100 |
|      2.5 ms | 180  |   125 |

De waarde in de laatste kolom is de waarde voor `angle` te gebruiken in `pin.write_analog(angle)`.
Het totale analoge-output bereik is 0..1023; daarvan gebruik je maar een klein deel.

*Berekening:* de *duty cycle* voor 0 graden is: pulsebreedte/periode = 0.5/20 is 1/40 ofwel 0,025; in procenten: 2,5% duty cycle. Als het bereik van de analoge output 0..1023 is, dan komt dit overeen met 0,025 * 1023 =  25,575, afgerond 25.

## Potmeter-servo schakeling

In het onderstaande programma gebruiken we een potmeter voor het aansturen van de servo: als de potmeter links staat moet de servo in de maximale linker stand staan; als de potmeter rechts staat, maximaal rechts.

Het bereik van de potmeter-waarde is 0..1023; het bereik van de servo-waarde is 25..125 (0..100 + 25). Dit betekent dat we de waarde van de potmeter moeten omrekenen voordat we deze gebruiken voor de servo.

- van 1023 terug naar 100 (ongeveer): delen door 10
- en dan 25 erbij optellen.

```Python
from microbit import * 

# servo on pin 0
# potmeter on pin 1

servo = pin0
potmeter = pin1

servo.set_analog_period(20) 
while True:
    in_signal = potmeter.read_analog()
    servo_signal = in_signal // 10 + 25
    servo.write_analog(servo_signal)
    sleep(10)
```

**Toelichting**.

**Opdracht 1.** Bouw de schakeling, laad het programma naar de microbit, en demonstreer de werking. Zet een opzetstukje op de servo-as, om duidelijk de hoek te kunnen zien.

**Opdracht 2.** (Zelf uitrekenen.) Met welke hoek komt een analoge output-waarde van 42 overeen? Wat is daarbij de pulsbreedte? K





## 360 graden of continue servo

De 360 graden servo kan over een volledige hoek draaien. Vaak is op de servo een wiel gemonteerd. Deze servo kun je gebruiken voor het aandrijven van een robotkarretje, met een servo voor elk wiel.

```{figure} ../figs/octopus-360-servo.png
:width: 300
:align: center

360 graden servo met wiel
```

Je kunt hetzelfde programma als hierboven gebruiken voor het aansturen van een continue servo, of het programma hieronder.
In de middenstand (1.5 ms, analoge outputwaarde 75) staat de servo stil.
Een kleinere waarde laat de servo linksom draaien, met de maximale snelheid bij 0.5 ms (analoge output 25).
Bij een grotere waarde dan 75 draait de servo rechtsom, met de maximale snelheid bij 2.5 ms (analoge output 125).


## Servo-besturing met knoppen

Schakeling: servo aan pin0; daarnaast gebruiken we de knoppen A en B op de microbit.

In plaats van een potmeter kun je ook de knoppen A en B gebruiken voor het instellen van de hoek (bij een 180 graden servo) of de richting/snelheid (bij een 360 graden servo).
Knop A verlaagt de hoek of de richting/snelheid, knop B verhoogt deze.

```Python
from microbit import * 

servo = pin0

servo.set_analog_period(20)
servo_signal = 75 # neutral, center

while True:
    if button_a.was_pressed():
        servo_signal = max(servo_signal - 5, 25)
        servo.write_analog(servo_signal)
    if button_b.was_pressed():
        servo_signal = min(servo_signal + 5, 125) 
        servo.write_analog(servo_signal)
```

Door het gebruik van de `max`- en `min`-functies beperken we de waarden van `servo_signal` tot het bereik 25..125.
Ga dit na, bijvoorbeeld voor de situatie waarin `servo_signal` de waarde 25 heeft, en dus `servo_signal - 5` de waarde 20.

**Opdracht 0.** Bouw deze schakeling, laad het programma op de microbit, en demonstreer de werking.
Gebruik eerst een 180 graden servo, en pas daarna de schakeling aan voor een 360 graden servo, als je die hebt.

## Links

- https://support.microbit.org/support/solutions/articles/19000101864-using-a-servo-with-the-micro-bit#programming
- https://kitronik.co.uk/blogs/resources/servos-brief-guide : deze webpagina geeft een goede en beknopte uitleg over servo's.
- de website over servo's en de microbit van Hans de Jong: https://www.hansdejongehv.nl/microbit-servos/index.html . De meeste servo's zijn gemaakt voor 4,5-5V voedingsspanning: dan heb je een externe voeding nodig, in de vorm van een batterij-pak of een USB-voeding. Hans beschrijft ook duidelijk hoe je die voeding en de microbit aansluit.
- https://www.youtube.com/watch?v=9WWPwK7HZEw - hoe je een aparte (sterkere) voeding verbindt aan de servo.

