# Kloppend hart

Dit is een eenvoudig voorbeeld, om te zien of alles werkt: test eerst het programma op de host-computer; breng het programma dan over van de host-computer naar de microbit, en laat het daar uitvoeren.

Initieel is het display leeg. In de lus toont het programma een hart op het display, en 500 ms later een leeg display, en 500 ms later weer het hart enz.

```python
from microbit import *

display.clear()

while True:
    display.show(Image.HEART)
    sleep(500)
    display.clear()
    sleep(500)
```

Dit programma volgt de [structuur van een *besturingsprogramma*](besturingsprogramma-structuur) in (micro)Python.
Dit is een eenvoudig programma, omdat het geen invoer gebruikt: het gedrag (de uitvoer) zal daardoor altijd hetzelfde zijn.

## Variaties

* laat in plaats van een hart, een andere figuur zien.
* verander de snelheid (frequentie) waarmee het hart knippert. Zorg er voor dat de "aan"tijd waarin het oplicht gelijk blijft aan de "uit"tijd waarin het scherm zwart is.
    * wat is de maximale tijd (minimale frequentie) waarbij je het hart nog ziet knipperen?
* verander de verhouding tussen de "aan"tijd en de "uit"tijd.
    * wat is het effect als de "aan"tijd veel kleiner is dan de "uit"tijd, en de frequentie hoog genoeg zodat je het hart niet ziet knipperen?
