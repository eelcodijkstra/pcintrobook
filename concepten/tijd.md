# Tijd

De fysieke wereld speelt zich af in allerlei dimensies, in ruimte en in *tijd*.
Voorwerpen bewegen met een bepaalde snelheid, het verwarmen van een kamer kost tijd, enzovoorts.

Bij het ontwerpen van een physical computing systeem moet je rekening houden met het gedrag daarvan in de tijd.
Je moet bijvoorbeeld weten hoe vaak je een bepaalde waarde moet meten, of hoe snel je moet kunnen reageren op een bepaald fysiek verschijnsel.

Denk bijvoorbeeld aan de temperatuurregeling van een woonkamer, via het aan- en uitzetten van de CV-installatie.
Hoe vaak moet je de temperatuur in de kamer meten? Hoe snel moet je kunnen reageren op een andere warmtevraag? Hoe snel moet je kunnen reageren op de temperatuurstijging door de CV?

Voor het beantwoorden van dergelijke vragen moet je een idee (model) hebben van de hele installatie, van instelbare thermostaat tot de warmtecapaciteit van het CV-systeem en van de kamer, en de manier waarop warmte weglekt uit de kamer.
Bovendien moet je weten hoe snel de CV-installatie aangestuurd kan worden: je kunt deze waarschijnlijk niet tienmaal per seconde aan- en uitzetten.

Je conclusie zal waarschijnlijk zijn dat als je elke seconde meet, je metingen snel genoeg zijn. Het reageren op een veranderende vraag hoeft ook niet sneller dan ca. 1 seconde. En het aan- en uitzetten van de CV moet waarschijnlijk beperkt worden tot eens per minuut. Je hebt waarschijnlijk ook geen ingewikkelde berekeningen nodig die veel tijd vragen. Je hebt dus geen snelle computer nodig voor die regeling: elke eenvoudige microcontroller is meer dan snel genoeg.

Een ander voorbeeld is een robot die een lijn moet volgen. Het hangt van de snelheid van deze robot af, hoe vaak je de positie van de robot moet meten en bijsturen. Je moet "op tijd" de robot kunnen bijsturen. (Het omgekeerde is ook het geval: als je niet vaak kunt meten en sturen, kun je de robot ook niet snel laten rijden.) 

**real-time system.** Een systeem dat altijd "op tijd" kan reageren noemen we een *real time system*. Dit moet snel genoeg zijn voor de fysieke omgeving waarin het moet meten en sturen. 

**Opmerking.** Een real-time system hoeft niet beslist "zeer snel" te zijn; het moet *voldoende snel* zijn voor de fysieke omgeving waarin het werkt.

## Expliciete periodes: timers en real-time klokken

Soms speelt tijd expliciet een rol in de fysieke omgeving: denk bijvoorbeeld aan de verkeerslichten voor een kruispunt.
Een eenvoudige regeling hiervoor heeft een bepaalde "groen"-tijd voor elke richting, met een "geel"-tijd voor de overgang tussen de verschillende richtingen.

Voor een knipperend verkeerslicht staan de aan- en uit-tijden ook vast.

In deze gevallen heb je *timers* nodig om deze *tijdsintervallen* te beschrijven. Een timer is een soort kookwekker die na een bepaalde periode afloopt. (Zie: XXX)

In andere gevallen moet je een fysieke gebeurtenis kunnen koppelen aan de klok-tijd; bijvoorbeeld voor het aansturen van het maandelijks testalarm moet je precies de actuele datum en tijd kennen. In zo'n geval heb je een *real time clock* (RTC) nodig. (Dit kun je ook zien als een speciale "sensor".)

## Tijd als surrogaat voor een lastige meting

Soms gebruik je een timer ("kookwekker")  als vervanging van een lastige meting. Denk aan het koken van een ei: je wilt eigenlijk weten wat de kern-temperatuur van het ei is, om op een geschikt moment te stoppen, voor een hard- of zachgekookt ei. Maar die kerntemperatuur is lastig te meten. In plaats daarvan meten we hoe lang het ei in kokend water gelegen heeft. Bijvoorbeeld: 5 minuten voor een zachtgekookt ei, en 9 minuten voor een hardgekookt ei.

Andere voorbeelden hiervan zijn: het gebruik van de magnetron-timer.

Voorbeeld: als je een robot moet besturen, en je kunt de snelheid van de wielen niet meten, dan kun je het verband meten tussen de duur van het afleggen van een afstand, of van het draaien over een bepaalde hoek, bij een bepaald motorvermogen. Je weet dan bijvoorbeeld dat 2/10 seconde alleen de rechtermotor "vol" vermogen, overeenkomt met een hoek naar links van 90 graden. Daarna kun je de robot sturen met behulp van precies getimede opdrachten. (Dit is niet erg precies, maar beter dan niets.)

