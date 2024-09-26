# Opzet van het lesmateriaal

Het lesmateriaal is opgezet rond de belangrijke concepten van Physical Computing.
In de Opdrachten (eigenlijk: etudes) worden deze concepten stap voor stap ingevoerd en geoefend.
De oplossingen uit deze opdrachten kunnen gebruikt worden als bouwstenen in een groter project.

## Praktische keuzes

* gebruik van microbit
* gebruik van Python of van
* gebruik van robot-systeem:
    * DFRobot Maqueen (Plus?); (NB: geen potmeter en geen servo! - servo's zitten wel in de mechanical parts kit)
    * Elekfreaks Nezha (met Lego); Planet X sensoren/actuatoren
* andere systemen:
    * DFRobot motor driver expansion board (GSV) of DFRobot Boson/Gravity expansion board
    * (Gravity is Grove compatibel? - Boson is meer vergelijkbaar met PlanetX, maar wat minder op technisch Lego georiënteerd; eigenlijk meer basisonderwijs)
    * Elekfreaks microbit Tinkerkit

## Ontwerpvragen

* tijdgedrag van de fysieke omgeving; welke eisen stelt dit aan het tijdgedrag van de controller (of: besturing)?
* welke fysieke grootheden wil je waarnemen? met welke precisie? welke sensoren zijn daarvoor geschikt? met welke andere eigenschappen? welke eisen stellen deze sensoren?
* fysieke gebeurtenissen (events): hoe te meten met sensoren? welke grootheden, welke sensoren? Een fysieke gebeurtenis kan zich in meerdere dimensies (met verschillende fysieke grootheden) afspelen.
* sturen in de fysieke omgeving: met welke actuatoren? welke eisen stellen deze (in het bijzonder: tijdgedrag, precisie, en vermogen).


## Belangrijke principes

Controller ontkoppelt de inputs van de outputs: je kunt via de controller allerlei combinaties van inputs en outputs maken. Met dezelfde potmeter kun je een LED dimmen, of de snelheid van een motor regelen.
Met dezelfde drukknoppen kun je een LED aan- of uitzetten, of een motor aan- of uitzetten.
Je kunt er ook een meting of een besturing op afstand mee maken.

vgl. de directe besturing: sensor aan actuator gekoppeld, voor de LED; door het gebruik van een tweede sensor (drukknop) kun je de LED aan- en uitschakelen, wat zonder een controller veel lastiger is (je hebt dan bijv. een mechanische constructie nodig).



