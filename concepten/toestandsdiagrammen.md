(toestandsdiagrammen)=
# Toestandsdiagrammen

Voorkennis: events (en signalen)

Een toestandsdiagram bestaat uit een eindig aantal

* *toestanden* (weergegeven door cirkels); meestal nummeren we de toestanden; en een eindig aantal
* *toestandsovergangen* (weergegeven door pijlen tussen de toestanden); een overgang (van P naar Q) is gelabeld met een event (E) en met een actie (A): als de event E optreedt in de toestand P, dan wordt de actie A uitgevoerd, en wordt Q de nieuwe toestand.  De actie kan bijvoorbeeld een output een bepaalde waarde geven.

Voorbeeld!

:::{figure} ../figs/led-knoppen-dimmer.drawio.png
:width: 500

Een LED-dimmer met knoppen
:::

Een toestandsdiagram is een handig middel om een event-besturing te beschrijven.

Controleer het toestandsdiagram op *volledigheid*: in principe moet elke toestand voor elk event een uitgaande pijl hebben. Als de betreffende event geen effect heeft in een toestand moet je dat apart noteren, bijvoorbeeld door een pijl vanuit die toestand naar zichzelf te tekenen, gelabeld met die event, met een streepje als actie. (In Python gebruik je `pass` voor "geen actie".)

Een toestandsdiagram is de grafische weergave van een *eindige automaat*, een begrip dat zowel in de theoretische informatica als in de software- en hardware-praktijk veel gebruikt wordt.

## Van toestandsdiagram naar Python code

Met de volgende procedure zet je een toestandsdiagram om in Python code.

**1. Maak een tabel van de toestandsovergangen.** Deze tabel heeft als kolommen: van-toestand, event, actie, naar-toestand.

Het voorbeeld van de dimmer met knoppen A en B wordt dan:

| van-toestand | input(event) | actie | naar-toestand |
| :---:        | :---:        | :---: | :---:         |
| 0            | A            | level 1 | 1           |
| 0            | B            | -       | 0           |
| 1            | A            | level 2 | 2           |
| 1            | B            | level 0 | 0           |
| 2            | A            | -       | 2           |
| 2            | B            | level 1 | 1           |



**2. Sorteer deze tabel in de volgorde van (input)events en vervolgens in de volgorde van van-toestand.**

| van-toestand | input(event) | actie | naar-toestand |
| :---:        | :---:        | :---: | :---:         |
| 0            | A            | level 1 | 1           |
| 1            | A            | level 2 | 2           |
| 2            | A            | -       | 2           |
| -            | -            |         |             |
| 0            | B            | -       | 0           |
| 1            | B            | level 0 | 0           |
| 2            | B            | level 1 | 1           |



**3. Schrijf de tabel om naar Python-code.** Maak voor elke event een `if`, en maak binnen die event onderscheid (via geneste `if ... elif`) tussen de toestanden. Per toestand krijg je een actie en een toekenning van de nieuwe toestand (naar-toestand).

```Python
    if button_a.was_pressed():
        if state == 0 :
            led.write_analog(maxlevel // 2)
            state = 1
        elif state == 1:
            led.write_analog(maxlevel)
            state = 2
        elif state == 2:
            pass

    if button_b.was_pressed():
        if state == 0:
            pass
        elif state == 1:
            led.write_analog(0)
            state = 0
        elif state == 2:
            led.write_analog(maxlevel // 2)
            state = 1
```

Deze reeks if-opdrachten plaats je in de besturingslus van je Python besturingsprogramma.

**Opmerking.** Je kunt voor elke event een afzonderlijke `if`-opdracht gebruiken, zoals hierboven; of, je gebruikt een doorlopende `if ... elif ...` waarin je de verschillende events onderscheidt. Beide oplossingen zijn mogelijk. In het eerste geval handel je alle events cyclisch af ("round robin" scheduling). In het tweede geval heeft de eerste event prioriteit; je handelt de tweede event pas af als er de eerste event niet meer optreedt, enz. Dit is een scheduling op basis van prioriteit. 

De code voor het tweede geval zou worden:

```Python
    if button_a.was_pressed():
        if state == 0 :
        ...

    elif button_b.was_pressed():
        if state == 0:
        ...
```


