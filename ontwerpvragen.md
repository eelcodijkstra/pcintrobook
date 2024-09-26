# Ontwerpvragen

Bij het ontwerpen van een physical computing systeem zijn de volgende vragen van belang:

**Welke fysische verschijnselen wil je meten?** Per fysiek verschijnsel: wat zijn de specifieke kenmerken daarvan; hoe precies moet je die meten? Hoe snel veranderent dit? Hoe vaak moet je dit meten? - en dan in tweede instantie: welke sensor(en) heb je daarvoor beschikbaar? Wat zijn de kenmerken daarvan (zie bijv. de datasheet).

**Welke fysische verschijnselen wil je sturen?** Per fysiek verschijnsel: wat zijn de kenmerken daarvan; hoe precies moet je sturen? Hoe snel moet je sturen? Hoe snel moet je reageren op een verandering (reactiesnelheid)?

Sommige fysische verschijnselen kun je in meerdere fysieke dimensies waarnemen. Bijvoorbeeld: de aanwezigheid van personen in een ruimte kun je detecteren op basis van: visuele waarneming (camera); infrarood-waarneming (PIR sensor); radar, radio-verstoring (radar-sensor; radio-signaalsterkte); geluid (microfoon); CO2-niveau (gassensor); gewicht op de vloer, op een stoel (load cell; druksensor); ... Je kunt daaruit een keuze maken die gemakkelijk te meten is en voldoende betrouwbaar. Om de betrouwbaarheid te vergroten kun je soms meerdere sensoren combineren ("sensor fusion").

*Voorbeeld:* voor het betrouwbaar detecteren van het vallen van een persoon kun je bijvoorbeeld een accelerometer gebruiken (versnellingsmeter), of een luchtdruksensor (hoogtemeter); voor een grotere betrouwbaarheid kun je deze combineren.





