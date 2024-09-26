(sensoren)=
# Sensoren

* eenvoudige digitale sensoren
    * digitale input
    * voorbeeld: drukknop
* analoge sensoren
    * voorbeeld: temperatuursensor
    * voorbeeld: potmeter (geeft een analoog signaal; "rotatiesensor")
        * potmeter als onderdeel van een muis?
    * a/d omzetting (vaak in de sensor; soms in de microcontroller: analoge input)
* complexe sensoren
    * met een complex interface; bijvoorbeeld: i2c, met een sensor-specifiek protocol
    * gebruik van libraries (software bij de sensor; voor het aansturen van de sensor)
    * voorbeeld: BME280 (ic2; gecombineerd: temperatuur, luchtdruk, en luchtvochtigheid)
    * ook: meten/detecteren van samengestelde events
        * denk bijv. aan het detecteren van bepaalde *gebaren*.
* eigenschappen van sensoren
    * datasheet
    * nauwkeurigheid (precisie en nauwkeurigheid?) - reproduceerbaar/herhaalbaar (kleine variatie) en getrouw
    * stroomverbruik (en afmetingen e.d.; denk bijvoorbeeld ook aan gebruik van een lucht-venster voor CO2 meting, drukmeting e.d.)
    * ...kosten... (in het algemeen geldt: sensoren die in een telefoon gebruikt worden, worden goedkoop. 

