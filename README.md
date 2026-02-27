# Ubuntu Keyboard Fix: US-International layout met Nederlandse Taal-ID

Deze fix zorgt ervoor dat je de fysieke toetsenbordindeling van **Engels (VS, internationaal, met dode toetsen)** gebruikt, maar dat het systeem tegen programma's (zoals OnlyOffice) zegt dat de taal **Nederlands** is. Hierdoor werkt de Nederlandse spellingcontrole automatisch.

## Stap 1: De Layout-definitie toevoegen
Voeg de US-International logica toe aan het Nederlandse symbolenbestand.

1. Open de terminal en bewerk het 'nl' bestand:
   `sudo nano /usr/share/X11/xkb/symbols/nl`
2. Scroll naar de bodem en plak dit blok:

```
partial alphanumeric_keys
xkb_symbols "us_intl" {
    include "us(intl)"
    name[Group1]= "Dutch (US International custom)";
};
```

## Stap 2: De Variant registreren in het systeem
Zorg dat de nieuwe optie zichtbaar wordt in de Instellingen van Ubuntu.

1. Open het regels-bestand:
   `sudo nano /usr/share/X11/xkb/rules/evdev.xml`
2. Zoek (Ctrl+W) naar `Dutch`.
3. Kijk iets lager naar de eerste `<variantList>` die je tegenkomt.
4. Plak daar, direct onder de regel `<variantList>`, dit blokje tussen:
```xml
    <variant>
      <configItem>
        <name>us_intl</name>
        <description>Dutch (US International custom)</description>
      </configItem>
    </variant>
```
5. Opslaan en sluiten.

## Stap 3: Activeren in Ubuntu
1. Herstart je computer (belangrijk om de XML-lijst te verversen).
2. Ga naar **Instellingen > Toetsenbord**.
3. Klik op **+** bij Invoerbronnen.
4. Klik op de drie puntjes (...) -> **Overige**.
5. Zoek en kies: **Nederlands (US International custom)**.
6. Verwijder eventuele andere bronnen zodat alleen deze overblijft.

## Waarom deze methode?
* **OnlyOffice:** Detecteert direct "Nederlands" voor spellingcontrole.
* **Toetsen:** Behoudt `" + a = ä` gedrag (dead keys).
* **Systeem:** Voorkomt conflicten tussen taal-instellingen en toetsenbord-mappings.
