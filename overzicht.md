# Overzicht 

| Les         | Concept(en) | Voorkennis |
| :---        | :---        | :---       |
| Kloppend hart | Controller, Host computer |  |
| LED met drukknop | Digitale signalen, besturingsprogramma |  |
| LED met afzonderlijke aan- en uitknop | Events, besturingsprogramma |  |
| LED met enkele aan/uitknop | Toestand, toestandsdiagram | events |
| Knipperende LED | Periodieke signalen, timer (periodiek)| events |
| LED met tijdschakeling | Timer (one-shot) | events |
| LED-dimmer met potmeter | Analoog inputsignaal, analoge output (PWM) | signalen |
| LED-dimmer met 2 knoppen | Toestand, toestandsdiagram, analoge output (PWM) | events |
| Servo-motor met potmeter | Servo (feedback) | Analoge input |
| DC-motor met potmeter | Analoge output (PWM), power | Analoge input  |
| Verkeerslichten | | Toestandsdiagram, Timers |
| Lijnvolger | lijn-sensor, feedback | DC-motor |
| Afstandsmeting | ultrasoon sensor | |


We gebruiken in de voorbeelden de volgende sensoren en actuatoren. Deze kun je door vergelijkbare sensoren of actuatoren vervangen.

| Soort | Sensor      | functie(s)| Actuator | functie(s) |
| :---  | :---        | :---      | :--- | :--- |
| Digitaal | Drukknop | `button.is_pressed()` (signaal)    | LED  | `led.write_digital(x)` |
|          |          | `button.was_pressed()` (event)     |      |                        |
|          |          | `pin.read_digital()`  (signaal)    |      |                        |
| Analoog  | Potmeter | `potmeter.read_analog()` (signaal) | LED  | `led.write_analog(x)`  |
