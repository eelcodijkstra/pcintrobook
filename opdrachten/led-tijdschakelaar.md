# LED-tijdschakelaar

"one shot timer"

Schakeling: LED aangesloten op pin 0; daarnaast gebruiken we knop A.

Met drukknop A zet je de LED aan. Na een bepaalde tijd (de `on_period`) schakelt de LED weer uit. Als je tijdens het branden van de LED weer op de knop drukt, gaat deze tijd opnieuw in.

```Python
from microbit import *

led = pin0

on_period = 5 * 1000 # ms
on_limit = 0     # not relevant when state == 0
state = 0

while True:
    now = utime.ticks_ms()
    if button_a.was_pressed():
        led.write_digital(1)
        state = 1
        on_limit = utime.ticks_add(now, on_period)
    if state == 1 and utime.ticks_diff(now, on_limit) > 0:
        led.write_digital(0)
        state = 0
```

Dit programma is een combinatie van de LED aan/uitschakelaar met enkele knop en de knipperende LED: met (event) knop A zet je de LED aan, daarbij wordt ook de timer ingesteld. Bij de event van het aflopen van de timer schakelt de LED uit.
Merk op dat bij het indrukken van de knop de timer altijd opnieuw ingesteld wordt, ook als de lamp al brandt.

Er is in dit geval sprake van een {term}`one-shot timer`: nadat de timer afgelopen is, loopt deze niet meer, totdat deze opnieuw ingesteld wordt. In dit geval kunnen we uit de toestand opmaken of de timer loopt. We mogen de timer `on_limit` alleen controleren deze loopt, met andere woorden: als `state == 1`, vandaar de extra voorwaarde bij de laatste `if`.
(Een {term}`periodieke timer` loopt altijd: in dat geval heb je geen aparte (toestands)variabele nodig om bij te houden of de timer wel of niet loopt.)

```{figure} ../figs/led-met-timer-diagram.drawio.png
:width: 500
:align: center

Toestandsdiagram LED met tijdschakelaar
```

**Opdracht 1.** Bouw de schakeling, laad het programma op de microbit, en demonstreer de werking

**Opdracht 2.** Verander het programma zodat de timer niet opnieuw ingesteld wordt als de LED al brandt.

**Opdracht 3.** Gebruik in plaats van knop A, een bewegingssensor voor het aanzetten van de LED.
