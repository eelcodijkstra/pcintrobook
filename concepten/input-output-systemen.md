(input-output-systemen)=
# Input-output systemen

*Physical computing* verbindt de fysieke wereld, van materie en krachten, met de virtuele wereld van informatie en rekenen.

(voorbeelden van physical computing)

## Embedded systems

Een computer die ingebouwd is in een apparaat dat geen computer is, om dat apparaat aan te sturen, noemen we een *embedded system*.
Je vindt deze in allerlei apparaten, van LED-lamp en tandenborstel via printer, magnetron en TV, tot auto en robot.
In veel van die gevallen zie je aan de buitenkant van het apparaat niet dat er een computer in zit; 
maar vaak is dat de handigste manier om het apparaat te besturen.
In al die gevallen gaat het om physical computing: fysieke verschijnselen die gemeten of aangestuurd worden door een computer.

(Voorbeelden van embedded systems.)

## Computers

:::{image} ../figs/computer.drawio.png
:width: 500
:::

In de informatie-wereld gaat het om informatieverwerkende systemen; een voorbeeld daarvan is een *computer*.
Een computer bestaat typisch uit de volgende onderdelen:

* invoer (of input), via invoerapparaten zoals toetsenbord, muis, trackpad, aanraakscherm, camera
* uitvoer (of output), via uitvoerapparaten zoals beeldscherm of luidspreker
* verwerkingseenheid (central processing unit, CPU)
* geheugen, vaak gesplitst in:
    * werkgeheugen (RAM)
    * opslag of achtergrondgeheugen (bijvoorbeeld Flash, harde schijf/SSD)
    * programmageheugen
* communicatie, bijvoorbeeld via bedraad netwerk (Ethernet) of draadloos netwerk (WiFi)
* (energievoorziening, bijvoorbeeld batterij/accu)

De inhoud van het werkgeheugen gaat verloren als je de computer uitzet.
Maar de inhoud van het achtergrondgeheugen en het programmageheugen blijft bewaard, 
en kan gebruikt worden als je de computer weer aanzet.
(Dit heet daarom ook wel *persistent geheugen*.)

Het programmageheugen is soms gecombineerd met het achtergrondgeheugen(?)

Voor het verbinden van de fysieke wereld aan een dergelijke computer gebruiken we *sensoren* en *actuatoren*.



:::{admonition} Sensor
Een *sensor* zet een fysiek verschijnsel om in informatie.

Voorbeelden van sensoren zijn: schakelaar, temperatuursensor, microfoon, camera.
:::

:::{margin}
Je kunt sensoren vergelijken met *zintuigen*, die informatie leveren voor je hersenen. En actuatoren met spieren, die informatie omzetten in beweging.
:::

:::{admonition} Actuator
Een *actuator* zet informatie om in een fysiek verschijnsel.

Voorbeelden van actuatoren: motor, luidspreker, LED (lampje).
:::



## Microcontrollers

Bij een *microcontroller* zin de bovengenoemde computer-onderdelen gecombineerd in een *geïntegreerde schakeling* ofwel IC (integrated circuit, ook wel "chip"). Bovendien heeft een microcontroller allerlei aansluitpunten voor extra invoer en uitvoer, zoals sensoren en actuatoren.
Microcontrollers worden veel gebruikt in embedded systems en andere physical computing systemen.

Een embedded system heeft eigenlijk maar één toepassingsprogramma: de besturing van het apparaat. Dit betekent dat je van te voren weet hoeveel rekenkracht je nodig hebt. Dit is anders dan bij een *general purpose computer* zoals in een laptop of desktop: daar weet je van te voren niet welke toepassingen erop uitgevoerd moeten kunnen worden.

Bij een microcontroller gaat het niet om maximale rekenkracht, maar vooral om lage kosten met voldoende rekenkracht voor de betreffende toepassing. De goedkoopste microcontrollers kosten 

## micro:bit

Een micro:bit is een klein bordje met een *physical computing* systeem, met een microcontroller, sensoren, actuatoren, communicatie, en energievoorziening. 
Je kunt dit direct gebruiken met de ingebouwde sensoren en actuatoren, maar je kunt er ook gemakkelijk andere sensoren en actuatoren op aansluiten.

(foto van een microbit).


In de afbeelding van de microbit zie je een aantal ICs (zwarte blokjes), met verschillende functies.


zie: https://microbit.org/get-started/features/overview/



Robot - met bovenstaande onderdelen

## Programmeren

Een microcontroller is een programmeerbare computer. Een computer is in principe universeel: deze kan heel veel verschillende taken uitvoeren, wat je ook kunt zien aan de toepassingen van computers. In het programma voor de microcontroller beschrijf je heel precies welke rekenstappen op elk moment uitgevoerd moeten worden, en daarmee, welke taak de microcontroller uitvoert. In het bijzonder beschrijf je hoe de output van de microcontroller op een zeker moment bepaald worden uit de inputs van dat moment *en daarvoor*.

### microbit: blokjesprogrammeren

Een programma voor een computer schrijf je in een programmeertaal die zowel door mensen als door computers goed begrepen kan worden.
Dit programma wordt vervolgens omgezet in een programma dat efficiënt door de computer uitgevoerd kan worden.

We geven hier een voorbeeld van een microbit-programma in Makecode: een "blokjes" programmeertaal.

:::{image} ../figs/microbit-prog-0.png
:width: 300
:::

De betekenis van dit programma is als volgt:

* als (op enig moment) knop A ingedrukt wordt, toon dan een vrolijke smiley op het scherm.
* als (op enig moment) knop B ingedrukt wordt, toon dan een droevige smiley (?) op het scherm.

Dit programma beschrijft hoe de microcontroller de uitvoer (naar het scherm) bepaalt uit de invoer (de knoppen).

**Opdracht.**

* maak dit programma met de Makecode editor en voer het uit in de simulator.
* laad dit programma naar je mictobit, en voer het uit.
* breid dit programma uit, zodat er een hartje getoond wordt als je microbit geschud wordt.

Voor het gebruik van de Makecode editor en het aansluiten van je microbit, zie Appendix X.

**Opmerking.** Het laatst getoonde beeld blijft staan, in dit geval. Dit is meestal ook wat je wilt. We zullen later zien hoe je dit zo kunt programmeren dat de uitvoer precies overeenkomt met de invoer op dat moment: als je geen knop indrukt, wordt geen smiley getoond.