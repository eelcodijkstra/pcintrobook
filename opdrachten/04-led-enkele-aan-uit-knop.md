(opdr-led-enkele-aan-uit-knop)=
# 4. LED met enkele aan- en uitknop

:::{admonition} Concepten en voorkennis
**Voorkennis** events

**Concepten** toestand (state), toestandsovergang, toestandsvariabele, toestandsdiagram
:::

**Schakeling:** een externe LED aangesloten op pin 0. Daarnaast gebruiken we de knop A.

**Programma:**

```python
from microbit import *

led = pin0
led.write_digital(0)  # LED uit
state = 0

while True:
    if button_a.was_pressed():
        if state == 0:
            led.write_digital(1)
            state = 1
        elif state == 1:
            led.write_digital(0)
            state = 0
```

**Toelichting.** Dit programma combineert het gebruik van *events* (van knop A) met een *toestandsvariabele*:
de variabele `state` geeft aan of de LED brandt. De actie bij het indrukken van de knop is nu afhankelijk van de toestand: als de lamp uit is, schakel je die aan, en past de toestand aan; als de lamp brandt, schakel je die uit, en past de toestand aan.

De onderstaande figuur geeft het toestandsdiagram hiervoor:

```{figure} ../figs/led-aan-uit-schakelaar-diagram.drawio.png
:width: 300
:align: center

Toestandsdiagram LED-schakelaar
```
De *toestanden* worden weergegeven door cirkels, de *toestandsovergangen* door pijlen tussen deze toestanden. Deze overgangen zijn *gelabeld* met "input-event /  actie": `A/LED off` betekent de overgang bij het indrukken van knop A; daarbij moet de actie `LED off` uitgevoerd worden.
De inkomende pijl links geeft de begintoestand aan (initialisatie).

**Opdracht 1.** Bouw de schakeling, laad het programma op de microbit, en demonstreer de werking.

**Opdracht 2.** Verander de initialisatie zo dat de LED direct brandt (`led.write_digital(1)`). Wat moet je dan nog meer veranderen?

