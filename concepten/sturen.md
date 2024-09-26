# Besturing

We behandelen hier hoe de controller de invoer van de sensoren verwerkt en op basis daarvan de actuatoren aanstuurt.
We bekijken dit vooral vanuit de *software*: welke programma-constructies heb je nodig voor bepaalde resultaten?
Hoe ziet het besturingsprogramma eruit?

## Signalen en events

In de software maken we voor de invoer en voor de uitvoer een onderscheid tussen *signalen* en *events*.

:::{admonition} Signalen en events
**Een signaal heeft op elk moment een waarde.** Denk bijvoorbeeld aan het signaal van een temperatuursensor, of van een accelerometer.

**Een event heeft alleen op waarde op een enkel "ondeelbaar" moment.** Denk bijvoorbeeld aan de event van het indrukken van een drukknopschakelaar (zoals de knoppen A en B op de microbit); of de event van een "stap" (voor een stappenteller).
:::

Verder onderscheiden we *digitale signalen* en *analoge signalen*. Een digitaal signaal heeft twee waarden, 0 en 1. Een analoog signaal kan een groot aantal verschillende waarden aannemen; bijvoorbeeld, in het geval van een 10-bits analoog signaal, de waarden 0..1023.
Het signaal van een drukknopschakelaar is digitaal: ingedrukt (1) of losgelaten (0).
Het signaal van een temperatuursensor is analoog: dit kan de waarden 0..1023 aannemen, bijvoorbeeld voor het temperatuurbereik 0..100 graden (Celcius).

## Het besturingsprogramma

Een *besturingsprogramma* heeft in microbit Python in grote lijnen de volgende structuur:

```Python
import van externe modules

...definities van lokale variabelen en functies

while True:
    inlezen van de inputs
    berekenen van de (te veranderen) outputs
    schrijven van de veranderde output(s)
```

De waarde van een output blijft staan totdat deze aangepast wordt.
Dit betekent dat je alleen veranderde outputs hoeft te schrijven.

De opdrachten in de lus `while True:` worden achtereenvolgens uitgevoerd, en dit wordt steeds herhaald totdat je de controller *reset* of uitzet.

Het besturingsprogramma moet in principe op elk moment op (bijna) alle invoer kunnen reageren.
Denk bijvoorbeeld aan de besturing van een wasmachine of van een magnetron: je moet tijdens de uitvoering van het programma nog kunnen ingrijpen, op z'n minst om het te kunnen onderbreken.
Of denk aan een robot: op het moment dat deze een lijn volgt, moet deze nog steeds in staat zijn om obstakels te herkennen.

**Problemen/foutzoeken** Als een besturingsprogramma erg traag lijkt te reageren, kan dat komen doordat dit programma *blokkerende opdrachten* bevat, zoals `sleep`, het wachten op invoer, het lezen van een bestand, of het raadplegen van een database.

## Signaal-besturing

Bij signaal-besturing bepaal je de waarde van het uitgaande signaal op basis van het ingaande signaal.
In het eenvoudige geval hangt het uitgaande signaal alleen af van het ingaande signaal *op dat moment*.

Voorbeeld van eenvoudige signaal-besturing zijn:

* een drukknop gekoppeld aan een lamp: de lamp brandt (alleen) als de drukknop ingedrukt is;
* een potmeter gekoppeld aan een lamp (een *dimmer*): de lamp brandt feller naarmate de potmeter verder naar rechts gedraaid is.

In het eerste voorbeeld zijn de invoer en de uitvoer digitale signalen. In het tweede voorbeeld zijn zowel de invoer als de uitvoer *analoge signalen*. Een groter getal staat dan voor een potmeter die verder naar rechts gedraaid is, of (bij de uitvoer) voor een lamp die meer licht geeft.

Voorbeeld: drukknop-signaal *direct* gekoppeld aan het display. Het display brandt alleen als knop A ingedrukt is.

```Python
from microbit import *

# set level of leds, in range 0 (off) to 9 (max leve)
def set_leds_level(n):
    for i in range(5):  # display: 5 x 5 led matrix
        for j in range(5):
            display.set_pixel(i, j, n)

set_leds_level(0)

while True:
    set_leds_level(button_a.is_pressed() * 9)
```

Het resultaat van `button_a.is_pressed()` is een `bool` waarde: `False` of `True`.
In Python is `bool` een subclass van `int`: `False` is `0`, `True` is `1`.
Het resultaat van `button_a.is_pressed() * 9` is dus `0` of `9`.

Voorbeeld 2: een potmeter *direct* gekoppeld aan het display. De potmeter is verbonden met `pin_0`.

```Python
from microbit import *

# set level of leds, in range 0 (off) to 9 (max leve)
def set_leds_level(n):
    for i in range(5):  # display: 5 x 5 led matrix
        for j in range(5):
            display.set_pixel(i, j, n)

set_leds_level(0)
# potmeter (analog input) connected to pin_0

while True:
    in_value = pin_0.read_analog()
    set_leds_level( in_value * 10 // 1024)
```

Het bereik van `in_value` is 0..1023 (analoge input).
Dit moeten we terugrekenen naar het bereik van het display-helderheid: 0..9.
We vermenigvuldigen eerst met het bereik van de uitvoer, en delen vervolgens door het bereik van de invoer.
De deling `//` staat voor `int` deling, het deeltal van geheeltallige deling met rest.
(Ga na dat het resultaat een waarde in het bereik 0..9 is.)

In een **complexere???** signaal-besturing kan het uitgaande signaal ook afhangen van de voorgeschiedenis (de vorige waarden van de invoer, samengevat in de *toestand*).

### Feedback-regeling

Je kunt een potmeter gebruiken als snelheidsregeling voor een motor, als in het voorbeeld van de dimmer.
Maar je hebt dan geen maat voor de snelheid van de motor. Bovendien zal de motor bij eenzelfde stand van de potmeter langzamer gaan draaien, als je deze zwaarder belast.

Als je de snelheid van motor preciezer wilt sturen, dan moet je de *werkelijke snelheid van de motor meten*, en deze vergelijken met de ingestelde snelheid (bijvoorbeeld van de potmeter). Als de snelheid groter is dan de ingestelde snelheid, moet je die verkleinen; als de snelheid kleiner is, dan moet je die vergroten.

Een systeem waarbij het resultaat van de actuator gemeten wordt en vergeleken wordt met een ingestelde waarde, om daarmee de actuator bij te sturen, noemen we een *feedback-systeem*.

Enkele voorbeelden van feedback-systemen:

* de temperatuurregeling (thermostaat) in een kamer (of in een oven): de thermostaat meet de actuele temperatuur, en vergelijkt die met de ingestelde waarde. Als de temperatuur lager is dan de ingestelde waarde, wordt de verwarming ingeschakeld. Als de temperatuur hoger is dan de ingestelde waarde, wordt de verwarming uitgeschakeld.

**Feed-forward regeling.** Het aansturen van een actuator zonder het meten van het effect daarvan heet ook wel een *feed-forward* regeling.
Dit werkt goed als het effect van de actuator goed te voorspellen is, zoals in het geval van een lamp (dimmer). Dit werkt minder goed als het effect door bijvoorbeeld omgevingsinvloeden niet goed voorspelbaar is, zoals bijvoorbeeld bij de temperatuurregeling (afhankelijk van de omgevingstemperatuur) of van de snelheidsregeling van een motor (afhankelijk van de belasting van de motor). In die gevallen heb je een feedback-regeling nodig.

### PID-regeling

Een verfijnde vorm van een feedback-regeling is de zogenaamde PID-regeling. (Zie bijvoorbeeld Wikipedia: ) In dit geval gebruik je naast de huidige waarde van de input(s), ook de historie daarvan, samengevat in de *toestand*.

## Event-besturing

Een input-event wordt in het besturingsprogramma gekoppeld aan een *actie*.
Deze actie kan bijvoorbeeld het aanpassen van een output zijn, het versturen van een radiobericht, of het aanpassen van de *toestand* (zie verderop).

Een eenvoudige voorbeeld is het (onderstaande?) programma voor het aan- en uitzetten van een lamp:
het indrukken van knop A (een event) resulteert in het aanzetten van de lamp (hier: het display);
het indrukken van knop B resulteert in het uitzetten van de lamp.

```Python
from microbit import *

ledson = Image(  # all LEDs full brightness
    '99999:'
    '99999:'
    '99999:'
    '99999:'
    '99999:'
)

display.clear()

while True:
    if button_a.was_pressed():
        display.show(ledson)
    if button_b.was_pressed():
        display.clear()
```

In microbit Python geeft de functie `x.was_pressed()` aan dat de knop `x` ingedrukt (geweest) is: er is een "indrukken" *event* geweest voor deze knop.
De functie `x.is_pressed()` geeft aan of de knop `x` *op dat moment* ingedrukt is: het is een *signaal*-functie.

In het bovenstaande voorbeeld wordt de event `button_a.was_pressed()` door middel van de `if`-opdracht gekoppeld aan de actie `display.show(ledson)`:
als (`if`) op het moment van uitvoeren van de opdracht, de voorwaarde (*conditie*) `button_a.was_pressed()` `True` is, dan worden de bijbehorende (ingesprongen) opdrachten uitgevoerd, in dit geval: `display.show(ledson)`.
En de event `button_b.was_pressed()` wordt op dezelfde manier gekoppeld aan de actie `display.clear()`.

### Event handler

Als de actie voor een event uit meerdere opdrachten bestaat, definiëren we voor deze actie vaak een aparte functie.
Een functie gekoppeld wordt aan een event (zoals hierboven) noemen we wel een *event handler*.

```Python

def handle_x():  # de event-handler
    ...reeks opdrachten

while True:
    ...
    if event_x: 
        handle_x() # aanroep van de handler bij optreden van event
    ...
```

## Event-besturing met toestand

In het bovenstaande voorbeeld gebruiken we twee drukknoppen voor het besturen van de lamp.
Door het gebruik van een toestandsvariabele kunnen we met één knop volstaan:

```Python
from microbit import *

ledson = Image(  # all LEDs full brightness
    '99999:'
    '99999:'
    '99999:'
    '99999:'
    '99999:'
)

display.clear()
ledstate = 0

while True:
    if button_a.was_pressed():
        if ledstate == 0:
            display.show(ledson)
            ledstate = 1
        else # ledstate ==1 
            display.clear()
            ledstate = 0
```

In de toestandsvariabele `ledstate` houden we bij of de leds branden (`ledstate == 1`) of niet (`ledstate == 0`).
Als knop A ingedrukt wordt (event), inspecteren we de toestandsvariabele, en afhankelijk van de toestand zetten we de leds aan of uit. We moeten daarbij wel de toestand bijwerken.

> Merk op dat je in Python schrijft: `x == 0` om te bepalen of x gelijk is aan 0 (een *conditie*), en `x = 0` om `x` de waarde `0` te geven (een *assignment* of toekenning).
> Je spreekt het eerste uit als "x is nul", en het tweede als "x wordt nul".

Bovenstaande event-besturing met toestand kunnen we ook weergeven in een toestandsdiagram:

### Toestandsdiagrammen

We kunnen ook een "discrete" dimmer maken met behulp van drukknoppen: als knop A ingedrukt wordt, moeten de leds meer licht geven; als B ingedrukt wordt, minder. In het onderstaande voorbeeld gebruiken we twee verschillende lichtniveaus, maar dat kun je naar behoeven uitbreiden.

```Python
from microbit import *

# set level of leds, in range 0 (off) to 9 (max leve)
def set_leds_level(n):
    for i in range(5):  # display: 5 x 5 led matrix
        for j in range(5):
            display.set_pixel(i, j, n)

display.clear()
ledstate = 0

while True:
    if button_a.was_pressed():
        if ledstate == 0:
            set_leds_level(5)
            ledstate = 1
        elif ledstate == 1:
            set_leds_level(9)
            ledstate = 2
        elif ledstate == 2:
            pass
    if button_b.was_pressed():
        if ledstate == 0:
            pass
        elif ledstate == 1:
            display.clear()
            ledstate = 0
        elif ledstate == 2:
            set_leds_level(5)
            ledstate = 1
```

(timers)=
### Timer-events

Tijd speelt een grote rol in de besturing van fysieke systemen. (Zie: ...)
We gebruiken in besturingsprogramma's daarvoor onder andere *timers*.
Een timer kun je zien als een kookwekker: je zet de timer zodat deze over een bepaalde tijd afloopt.
Het aflopen van een timer is een *event*: daar kun je weer een actie aan koppelen.

Eenvoudig voorbeeld van een timer: knipperlicht.

```Python
from microbit import *
import utime

# set level of leds, in range 0 (off) to 9 (max leve)
def set_leds_level(n):
    for i in range(5):  # display: 5 x 5 led matrix
        for j in range(5):
            display.set_pixel(i, j, n)
            
display.clear()
led_state = 0
toggle_interval = 500  # 500 ms = 0.5 seconds
timer_deadline = utime.ticks_add(utime.ticks_ms(), toggle_interval)

while True:
    current_time = utime.ticks_ms()
    
    if utime.ticks_diff(current_time, timer_deadline) >= 0:
        if led_state == 0:
            set_leds_level(0)
            led_state = 1
        else: # led_state == 1
            set_leds_level(9)
            led_state = 0
        timer_deadline = utime.ticks_add(current_time, toggle_interval) # for next timer event
```

**Opmerking 1.** Je kunt een eenvoudig knipperlicht maken met behulp van de `time.sleep()`-functie, maar dat heeft als nadeel dat je dat knipperlicht niet met andere taken kunt combineren, doordat de `sleep`-functie het programma tijdelijk pauzeert. De bovenstaande implementatie staat wel toe dat je deze met andere taken combineert.

**Opmerking 2.** In dit geval is er sprake van een "software timer". Op veel systemen kun je ook gebruik maken van een "hardware timer": een kookwekker in hardware-vorm.



