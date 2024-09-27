# 5. Knipperende LED

:::{admonition} Concepten en voorkennis
**Voorkennis** events, toestand, toestandsovergang, toestandsdiagram

**Concepten**  (periodieke) timer, periode
:::

**Schakeling:** LED aangesloten op pin 0

In dit voorbeeld gebruiken we een *timer* om de LED periodiek aan- en uit te schakelen: we krijgen zo een knipperende LED.

**Programma:**

```Python
from microbit import *
import utime

led = pin0

period = 2000 # ms
on_period = period // 2

timer_limit = 0 # gives immediate time_out
state = 0

while True:
    now = utime.ticks_ms()
    if utime.ticks_diff(now, timer_limit) > 0: # now > timer_limit?
        if state == 0
            state = 1
            led.write_digital(1)
            timer_limit = utime.ticks_add(now, on_period)
        else:
            state = 0
            led.write_digital(0)
            timer_limit = utime.ticks_add(now, period - on_period)
```

**Toelichting.** Dit programma heeft dezelfde opzet als het programma voor het aan- en uitzetten van de LED met één enkele aan/uit-knop. (*Vergelijk deze.*). De schakelaar-event is nu vervangen door een timer-event. Als de timer afloopt (`now > timer_limit`) schakelen we de led aan of uit, afhankelijk van de toestand. Daarbij zetten we direct `timer_limit` voor de volgende timer-event: de timer is altijd actief. (Dit is een *periodieke timer*.)

De tikken kunnen "rond tellen": als `utime.ticks_ms()` de maximale waarde bereikt heeft, begint deze weer bij 0 te tellen. Dit betekent dat de vergelijking tussen `now` en `timer_limit` wat ingewikkelder is dan een vergelijking tussen 2 "normale" getallen. Door het verschil `now - timer_limit` te schrijven als `utime.ticks_diff(now, timer_limit)` los je dat probeem op. Op eenzelfde manier schrijf je `now + on_period` als `utime.ticks_add(now, on_period)`.

N.B.: `now > timer_limit` kun je ook schrijven als `now - timer_limit > 0` ; voor deze laatste vorm kun je dan de `diff`-functie gebruiken.

```{figure} ../figs/knipperende-led-diagram.drawio.png
:width: 300
:align: center

Toestandsdiagram knipperende LED
```

In dit toestandsdiagram is (ten opzichte van de LED aan/uit schakeling) de knop-event vervangen door een timer-event.

**Opdracht 1.** Bouw de schakeling, laad het programma op de microbit, en demonstreer de werking.

**Opdracht 2.** Verander de {term}`periode` van de knipperende LED, bijvoorbeeld naar 1000ms (of nog kleiner). Wat is het effect? Wat is het effect als je de periode verkleint tot 10 ms?

**Opdracht 3.** Verander `on_period` als fractie van `period`, bijvoorbeeld naar 1/8. Wat is het effect? Wat is het effect als je dit combineert met een periode van 10 ms?


