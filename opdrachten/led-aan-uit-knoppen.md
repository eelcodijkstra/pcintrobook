(opdr-led-aan-uit-knoppen)=
# LED met afzonderlijke aan- en uitknop

:::{admonition} Concepten en voorkennis
**Voorkennis** besturingsprogramma, bestursingslus, LED-schakeling

**Concepten** events en event-handling, idempotent gedrag
:::

**Schakeling:** een externe LED aangesloten op pin 0. Daarnaast gebruiken we de knoppen A en B.

**Programma:**

```python
from microbit import *

led = pin0
led.write_digital(0)  # LED uit

while True:
    if button_a.was_pressed():
        led.write_digital(1)
    elif button_b.was_pressed():
        led.write_digital(0)  
```

**Toelichting.** 
De functie-aanroep `button_a.was_pressed()` levert `True` als de knop A ingedrukt geweest is sinds de laatste aanroep van deze functie; anders `False`.  Deze functie signaleert de *event* van het indrukken van deze knop.

> De functie `button_a.was_pressed()` is een *event-functie* in microbit Python; deze geeft aan of er sinds de vorige aanroep van deze functie, de knop A ingedrukt geweest is. De functie `button_a.is_pressed()` is een *signaal-functie*: deze geeft aan of de knop A op het moment van aanroep ingedrukt is: de actuele signaal-waarde.

Als deze event opgetreden is, wordt de bijbehorende actie ("event handler") uitgevoerd. In het geval van knop A is dat het aanzetten van de LED.

Op eenzelfde manier wordt, als knop B ingedrukt geweest is, de LED weer uitgezet.

Dit programma is een voorbeeld van het *event-sturing*. Het volgt de algemene structuur in de besturingslus voor het *afhandelen van events*:

```Python
while True:
    if event1:
        handle_event1
    elif event2:
        handle_event2
    elif event3:
        handle_event3
    ...
```

**Idempotent gedrag.** Merk op dat het niet uitmaakt of je één van de knoppen eenmaal indrukt, of meerdere keren achter elkaar. Dit noemen we {term}`idempotent` gedrag. Dit kan handig zijn als de knoppen bijvoorbeeld minder betrouwbaar zijn: als je denkt dat de knop niet gewerkt heeft, druk je die nog een keer in: dat heeft nog steeds hetzelfde effect. Als je maar één knop gebruikt voor het aan- en uitzetten van de LED heb je geen idempotent gedrag. (REF - volgende opdracht)

**Opdracht 1.** Bouw de schakeling, laad het programma op de microbit, en demonstreer de werking.

**Opdracht 2.** Verander het programma zodat je de LED uitzet met knop A, en aanzet met knop B. Zorg er in dit geval ook voor dat de LED brandt als je nog geen knop aangeraakt hebt.

**Vraag 3.** Wat is het effect als je in plaats van de event-functies `button.was_pressed()` hier de signaal-functies gebruikt (`button.is_pressed()`)? Kun je dat verklaren uit het *idempotente gedrag* van de knoppen? Waarom zou je (in een groter programma waarin dit als onderdeel opgenomen is) toch de voorkeur geven aan de bovenstaande event-sturing?
