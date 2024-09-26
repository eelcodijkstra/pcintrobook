# FAQ

Hieronder een aantal veelgestelde vragen.

**Wat is het verschil tussen een analoge en een digitale temperatuursensor?** In beide gevallen wordt een temperatuur omgezet in een spanning. Deze spanning moet vervolgens omgezet worden in een getal (analoog/digitaal-omzetting). Deze omzetting kan aan de kant van de microcontroller plaatsvinden - bijvoorbeeld door een analoge input-pin van de microbit te gebruiken in combinatie met de `pin.read_analog()`-functie. In dat geval bestaat de communicatie tussen de sensor en de microcontroller uit een analoge waarde, en spreek je over een analoge temperatuursensor. Door de analoge communicatie is deze eenvoudig in het gebruik.

De omzetting van spanning naar getal (A/D omzetting) kan ook in de sensor zelf plaatsvinden. Dan moet er een digitaal protocol zijn om dit getal naar de controller te communiceren. Dit zijn digitale temperatuursensoren. Voorbeelden hiervan zijn: 

- DS18B20 - gebruikt het "one wire protocol"
- BME280 - (naast temperatuur ook luchtdruk en luchtvochtigheid) - gebruikt I2C of SPI protocol
- DHT20 - (temperatuur en luchtvochtigheid) - gebruikt I2C protocol

In het geval van een serieel protocol, zoals I2C, SPI of one-wire, kun je met meerdere sensoren communiceren via dezelfde draden; dit spaart pinnen en draden. Daarom gebruiken gecombineerde sensoren, zoals hierboven, gewoonlijk zo'n protocol.

Voor de communicatie met deze digitale sensoren heb je een *library* nodig; niet alleen voor de seriële communicatie zelf, zoals I2C, maar ook voor de specifieke sensor.

Nadat de communicatie van de waarde, via een analoge of digitale verbinding met speciaal protocol, heb je in beide gevallen een "waarde van een analoog signaal" als resultaat, waaraan je niet meer kunt zien hoe dat gecommuniceerd is.

