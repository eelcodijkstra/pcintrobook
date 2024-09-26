(led-drukknop)=
# LED met drukknop

:::{admonition} Concepten en voorkennis
**Voorkennis**

**Concepten**  besturingsprogramma, besturingslus, LED-schakeling, signaal-sturing
:::

:::{figure} ../figs/octopus-led-red.png
:width: 200

Rode LED
:::

**Schakeling:** LED aangesloten op pin 0 van de microbit. Daarnaast gebruiken we knop A op de microbit.

**Programma:**

```python
from microbit import *

led = pin0
led.write_digital(0)

while True:
    button_value = button_a.is_pressed()
    led.write_digital(button_value)
```

**Toelichting.** Het besturingsprogramma hierboven bestaat uit (i) de import-opdracht(en) voor de libraries die je gebruikt, in dit geval: de `microbit` library, met definities voor `pin0`, `write_digital`, enz.; (ii) de {term}`initialisatie` van de LED; deze initialisatie wordt eenmaling uitgevoerd; en (iii) de {term}`besturingslus`: `while True: ...opdrachten`. De opdrachten in de besturingslus worden steeds herhaald totdat je de microbit reset of uitzet.

In de *initialisatie* wordt de variabele `led` gekoppeld aan `pin0`, en wordt de LED uitgeschakeld (`0`). In de *besturingslus* wordt het *signaal* van knop A gelezen, en weggeschreven naar de led. De LED brandt dan alleen als de knop A ingedrukt is. (Dit is een voorbeeld van *signaal-sturing*.)

```{figure} ../figs/button-led-signal.drawio.png
:width: 600
:align: center

Drukknop-signaal (input) en LED-signaal (output). Als de drukknop ingedrukt is, is is het signaal 1, anders 0. Een signaalwaarde 1 voor de LED laat de LED branden.
```

**Opdracht 1.** Bouw de schakeling, laad het programma op de microbit, en demonstreer de werking.

**Vraag 2.** Voor het aan- en uitschakelen van een LED is dit programma niet echt handig, je kunt dan beter één van de andere oplossingen gebruiken, zoals de LED met afzonderlijke aan- en uitknop. Kun je een situatie bedenken waarin het gebruik van zo'n signaalsturing van een LED zinvol is, met een ander signaal als input?

**Opdracht 3.** Pas het programma aan zodat de LED brandt als knop A niet ingedrukt is, en uitgaat als je knop A indrukt.
