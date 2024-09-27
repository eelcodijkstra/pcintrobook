# 9. LED instelbare PWM dimmer

:::{admonition} Concepten en voorkennis
**Voorkennis** timers, periodieke timer, analoge input, analoge output 

**Concepten** software PWM (oefening) 
:::

**Schakeling:** LED op pin0, potmeter op pin1; daarnaast gebruiken we de knoppen A en B 

Je kunt via de analoge output PWM (pulsbreedtemodulatie) in hardware gebruiken. In dit voorbeeld maken we de PWM zelf in software, met behulp van een timer. Via de potmeter kun je de periode (en de frequentie) van de PWM instellen. Met de knoppen A en B kun je de *duty cycle* vergroten c.q. verkleinen. We demonstreren deze software PWM met een knipperende en dimmende LED.

Met een digitale output kun je een LED aan- en uitzetten, door 1 respectievelijk 0 naar de output te schrijven. Het lijkt alsof je daarmee de lichtsterkte van de LED niet kunt regelen. Maar: je kunt hiermee de LED wel laten knipperen, bijvoorbeeld 1s aan en 1s uit. Je kunt de snelheid van het knipperen zo hoog maken, bijvoorbeeld 1 ms aan en 1 ms uit, dat je oog het schakelen van de LED niet meer ziet. Je oog ziet dan alleen een LED die minder fel brandt omdat deze de helft van de tijd uit is. Dit is de manier waarop je een LED-dimmer kunt maken. Door de verhouding tussen de aan-tijd en de uit-tijd te veranderen, kun je de lichtsterkte regelen.

FIG LED aan- uit

Voor het microbit-programma gebruiken we een potmeter voor het regelen van de lichtsterkte: de verhouding tussen de aan- en uittijd. We gebruiken de knoppen A en B voor het regelen van de frequentie waarmee de LED knippert. Hiermee kun je ook demonstreren dat als je de frequentie hoog genoeg maakt, je oog het knipperen niet meer ziet.

**Programma**

```Python
from microbit import *
import utime

led = pin0
potmeter = pin1

period = 2000 # ms
on_period = period // 2

timer_limit = 0 # gives immediate time_out
led_on = False

while True:
    now = utime.ticks_ms()
    if utime.ticks_diff(now, timer_limit) > 0:
        if led_on:
            led_on = False
            led.write_digital(0)
            timer_limit = utime.ticks_add(now, period - on_period)
        else:
            led_on = True
            led.write_digital(1)
            timer_limit = utime.ticks_add(now, on_period)
 
    if button_a.was_pressed():
        period = period // 2
        if period < 2:
            period = 2 # ms
    elif button_b.was_pressed():
        period = period * 2
        if period > 2000:
            period = 2000 # ms

    potm = potmeter.read_analog() # 0..1023
    on_period = period * potm // 1023
```

De minimale periode is 2 ms; dit komt overeen met 500 Hz. Dit is ruim boven de frequentie die het menselijk oog nog kan waarnemen. We gebruiken voor de timer de milliseconde-ticks: we kunnen dan niet met kleinere tijden rekenen dan in ms. De maximale periode is 1 s (1000 ms). Voor deze demonstratie is een grotere periode niet erg zinvol (maar, je kunt dit maximum eenvoudig aanpassen).

Opmerking. Het programmadeel:

```Python
        period = period // 2
        if period < 2:
            period = 2 # ms
```
            
kun je ook schrijven als:

```Python
        period = max(period // 2, 2)
```

Door het maximum van deze twee uitdrukkingen te nemen zorg je ervoor dat period nooit kleiner wordt dan 2.
Op dezelfde manier kun je voor knop B schrijven, om te zorgen dat period nooit groter wordt dan 2000:

```Python
        period = min(period * 2, 2000)
```

Je krijgt dan:

```Python
    if button_a.was_pressed():
        period = max(period // 2, 2) # ms
    elif button_b.was_pressed():
        period = min(period * 2, 2000) # ms
```
        
**Opmerking.** Je kunt op deze manier de LED niet helemaal uitschakelen: het programma blijft schakelen tussen aan en uit, waardoor ook voor on_period == 0 de LED korte tijd brandt. En je ook is gevoelig genoeg om dat nog wel waar te nemen. Test dit maar eens door via knop B de maximale periode in te stellen (2 seconden), en met de potmeter de aan-periode minimaal (0) te maken: je blijft die korte flits zien.

**Analoge output: hardware PWM**

In het voorbeeld hierboven wordt de lichtsterkte van de LED aangepast door de verhouding tussen de aan-tijd en de uit-tijd te veranderen, ofwel tussen de aan-tijd en de hele periode. Dit principe heet pulsbreedte modulatie ( Pulse Width Modulation, PWM): hiermee kun je via een digitale output een analoog niveau instellen. De verhouding tussen de aan-tijd en de periode heet de duty cycle; meestal druk je die uit als percentage. Een aan-tijd van 5 ms met een periode van 20 ms heeft dan een duty cycle van 25%; 10 ms op 20 ms 50%; enzovoorts.

De analoge output van de microbit, met de Python functie `pin.analog_write(x)`, stuurt de betreffende pin aan met een PWM-signaal. De parameter x moet liggen tussen 0 en 1023, voor een duty cycle van 0% tot 100%.

Met deze analoge output kun je een analoog niveau instellen, bijvoorbeeld de lichtsterkte van een LED, of de snelheid van een motor. Deze is niet geschikt voor een echt analoog signaal, zoals spraak: daarvoor heb je een uitgang nodig met een digitaal/analoog omzetter. Maar dat valt buiten het bestek van de microbit. (De "muziek" die de microbit maakt is helemaal gemaakt met een digitale uitgang die je aanstuurt met een periodiek signaal met verschillende periodes (toonhoogtes).)

```Python
from microbit import *

while True:
    potm = pin0.read_analog()
    pin1.write_analog(potm)
```

Omdat deze PWM in hardware uitgevoerd wordt, zie je geen korte flitsen bij de niveaus 0 en 1023