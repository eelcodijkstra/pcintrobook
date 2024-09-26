(led-drukknop)=
# LED met drukknop

Schakeling: LED aangesloten op pin 0 van de microbit. Daarnaast gebruiken we knop A op de microbit.

```python
from microbit import *

led = pin0
led.write_digital(0)

while True:
    button_value = button_a.is_pressed()
    led.write_digital(button_value)
```

**Toelichting.** In de {term}`initialisatie` wordt de variabele `led` gekoppeld aan `pin0`, en wordt de LED uitgeschakeld (`0`). In de {term}`besturingslus` wordt het *signaal* van knop A gelezen, en weggeschreven naar de led. De LED brandt dan alleen als de knop A ingedrukt is. (Dit is een voorbeeld van *signaal-sturing*.)

```{figure} ../figs/button-led-signal.drawio.png
:width: 600
:align: center

Drukknop-signaal (input) en LED-signaal (output)
```

REF???

**Opdracht 1.** Bouw de schakeling, laad het programma op de microbit, en demonstreer de werking.

**Vraag 2.** Voor het aan- en uitschakelen van een LED is dit programma niet echt handig, je kunt dan beter één van de andere oplossingen gebruiken. (REF). Kun je een situatie bedenken waarin het gebruik van zo'n signaalsturing van een LED zinvol is, met een ander signaal als input?

**Opdracht 3.** Pas het programma aan zodat de LED brandt als knop A niet ingedrukt is, en uitgaat als je knop A indrukt.
