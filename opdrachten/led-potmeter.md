(led-potmeter)=
# LED dimmer met potmeter

:::{admonition} Concepten en voorkennis
**Voorkennis** signaal-sturing

**Concepten** analoge input, analoge output (PWM)
:::

**Schakeling:** LED aangesloten op pin 0, potmeter aangesloten op pin 1.

Als je de potmeter linksom draait, neemt het lichtniveau van de LED af; als je de potmeter rechtsom draait, neemt het lichtnvieau toe. (Net als bij de volumeregeling van een versterker.)

**Programma: **

```python
from microbit import *

led = pin0
potmeter = pin1

led.write_analog(0)

while True:
    level = potmeter.read_analog()
    led.write_analog(level)
```

**Toelichting** De opdracht `potmeter.read_analog()` leest de analoge waarde van de potmeter: een getal in het bereik 0..1023. Deze waarde wordt vervolgens gebruikt als ({term}`PWM`) uitgangsniveau voor de LED, via `led.write_analog(level)`.

Dit is een voorbeeld van *signaal-sturing*: het input-signaal wordt direct omgerekend in het bijbehorende output-signaal.

**Opdracht 1.** Bouw de schakeling, laad het programma op de microbit, en demonstreer de werking.

**Opdracht 2.** Pas het programma aan zodat tussen de opeenvolgende herhalingen een pauze zit van 20 ms, met behulp van de `sleep(t)` functie aan het eind van de besturings-lus; hierin wordt `t` uitgedrukt in ms. 

- (a) Merk je een vertraging in de reactie op de potmeter-instelling? 
- (b) Hoe groot kun je deze pauze maken voordat je wel een vertraging in de reactie merkt? 
- (c) Maakt het uit waar in de besturingslus je deze `sleep`-opdracht plaatst?

*Opmerking.* Vaak combineer je de signaal-sturing met andere opdrachten, bijvoorbeeld voor het afhandelen van allerlei events. Deze opdrachten leveren een vertraging op, maar dat hoeft voor de signaal-sturing niet direct een probleem te zijn: zoals je merkt is in dit geval die vertraging niet direct van invloed op het waarneembare gedrag.


