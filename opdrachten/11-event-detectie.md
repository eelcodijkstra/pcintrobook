# 11. Event-detectie

Voor sommige events heeft microbit Python speciale functies, bijvoorbeeld `button.was_pressed()` of `accelerometer.was_gesture(shake)`. Maar voor externe sensoren moet je de events zelf detecteren.
We geven hieronder een voorbeeld hoe je de event van het indrukken van een knop kunt detecteren in het (digitale) signaal van die knop.

Het indrukken van knop A komt overeen met de overgang van 0 naar 1 in het digitale signaal van de knop. Om deze overgang te detecteren vergelijken we de vorige waarde van dit signaal met de huidige waarde: als de vorige waarde 0 was, en de huidige waarde 1, dan hebben we met een event te maken van het indrukken van de knop. In dat geval voeren we de actie uit die bij het indrukken van die knop hoort.

:::{figure} ../figs/button-signal-event.drawio.png
:width: 600

Van drukknop-signaal naar drukknop-event: overgang van 0 naar 1
:::

We gebruiken het voorbeeld van de LED met een enkele aan/uit knop, waarin we in plaats van de event-functie `was_pressed()` de signaal-functie `is_pressed()` gebruiken, die altijd de *huidige waarde* van het knop-signaal weergeeft.

Schakeling: LED aan pin 0; daarnaast gebruiken we knop A van de microbit.

```python
from microbit import *

led = pin0
led.write_digital(0)  # LED uit
state = 0
button_value = 0

while True:
    button_prev_value = button_value
    button_value = button_a.is_pressed()
    if button_prev_value == 0 and button_value == 1: # button event detected
        if state == 0:
            led.write_digital(1)
            state = 1
        elif state == 1:
            led.write_digital(0)
            state = 0      
```

**Toelichting.** Om de overgang van 0 naar 1 in het signaal van de knop te kunnen detecteren, vergelijken we de vorige waarde `button_prev_value` met de huidige waarde, `button_value`. Als de eerste 0 is en de tweede 1, hebben we de event van het indrukken van de knop gedetecteerd, en voeren we de bijbehorende actie uit. We moeten daarvoor steeds de vorige waarde van het knop-signaal onthouden. Vóór het lezen van het signaal bewaren we eerst de vorige waarde, om die met de nieuw gelezen waarde te kunnen vergelijken.

**Opdracht 1.** Bouw de schakeling, laad het programma op de microbit, en demonstreer de werking.

:::{figure} ../figs/octopus-crash-sensor.png
:width: 300

Octopus crash sensor (micro switch)
:::

**Opdracht 2.** Vervang de ingebouwde knop A door de externe "crash sensor" (een zogenaamde *micro switch*), verbind deze met pin1. Voor het lezen van de signaalwaarde van die sensor gebruik je dan `pin1.read_digital()`. 

* (a) Deze sensor geeft een 1 als deze *niet ingedrukt* is, en een 0 als deze ingedrukt is. Wat betekent dat voor de werking van het programma?
* (b) Pas het programma aan zodat de werking gelijk is als bij knop A: direct bij het indrukken verandert de LED.