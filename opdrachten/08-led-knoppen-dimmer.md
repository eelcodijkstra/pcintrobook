# 8. LED dimmer met knoppen

:::{admonition} Concepten en voorkennis
**Voorkennis** events, toestand, toestandsdiagram, analoge output

**Concepten** toestand, toestandsdiagram (oefening)
:::

**Schakeling*:* LED aan pin 0, daarnaast gebruiken we de knoppen A en B

Met knop A verhoog je de lichtsterkte van de LED, met knop B verlaag je de lichtsterkte. Je kunt de lichtsterkte instellen op 3 niveaus: 0 (uit), 1 (halve lichtsterkte), en 2 (volledige lichtsterkte).
De LED wordt aangestuurd via een *analoge output*.

**Programma**

```Python
from microbit import *
import utime

led = pin0
max_level = 1023

state = 0

while True:
 
    if button_a.was_pressed():
        if state == 0:
            led.write_analog(max_level // 2)
            state = 1
        elif state == 1:
            led.write_analog(max_level)
            state = 2
        elif state == 2
            pass 

    if button_b.was_pressed():
        if state == 2:
            led.write_analog(max_level //2)
            state = 1
        elif state == 1:
            led.write_analog(0)
            state = 0
        elif state == 0
            pass 

```

**Toelichting.**
Dit programma stuurt de LED aan met `led.write_analog(level)`. Hierbij is `level` een waarde in het bereik 0..1023. Met deze analoge schrijfopdracht stel je een *analoog niveau* in op de betreffende output-pin. Hiervoor wordt gebruik gemaakt van pulsbreedte-modulatie ({term}`pulse width modulation`, PWM). Een dergelijk analoog niveau gebruik je bijvoorbeeld voor het instellen van de lichtsterkte (zoals hier) of van de snelheid van een motor.

```{figure} ../figs/led-knoppen-dimmer-diagram.drawio.png
:width: 500
:align: center

Toestandsdiagram LED dimmer met knoppen
```

**Opdracht 1.** Bouw de schakeling, laad het programma op de microbit, en demonstreer de werking.

**Opdracht 2.** Breid het aantal lichtniveaus uit dat je met deze dimmer kunt instellen: 0, 1/4, 1/2, 1 (als fractie van het maximale niveau).

- teken eerst het toestandsdiagram voor deze uitbreiding
- pas daarna het programma aan