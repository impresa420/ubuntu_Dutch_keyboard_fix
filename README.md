> English explaination below!

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

> English version
# Ubuntu Keyboard Fix: US-International layout with Dutch Language ID
This fix ensures that you use the physical keyboard layout of **English (US, international, with dead keys)**, while the system tells applications (such as OnlyOffice) that the language is **Dutch**. This makes Dutch spell checking work automatically.
## Step 1: Adding the Layout Definition
Add the US-International logic to the Dutch symbols file.
1. Open the terminal and edit the 'nl' file:
   `sudo nano /usr/share/X11/xkb/symbols/nl`
2. Scroll to the bottom and paste this block:
```
partial alphanumeric_keys
xkb_symbols "us_intl" {
    include "us(intl)"
    name[Group1]= "Dutch (US International custom)";
};
```
## Step 2: Registering the Variant in the System
Make the new option visible in Ubuntu's Settings.
1. Open the rules file:
   `sudo nano /usr/share/X11/xkb/rules/evdev.xml`
2. Search (Ctrl+W) for `Dutch`.
3. Look a little lower for the first `<variantList>` you encounter.
4. Paste the following block directly below the `<variantList>` line:
```xml
    <variant>
      <configItem>
        <name>us_intl</name>
        <description>Dutch (US International custom)</description>
      </configItem>
    </variant>
```
5. Save and close.
## Step 3: Activating in Ubuntu
1. Restart your computer (important to refresh the XML list).
2. Go to **Settings > Keyboard**.
3. Click **+** under Input Sources.
4. Click the three dots (...) -> **Other**.
5. Search for and select: **Dutch (US International custom)**.
6. Remove any other sources so that only this one remains.
## Why this method?
* **OnlyOffice:** Directly detects "Dutch" for spell checking.
* **Keys:** Retains `" + a = ä` behaviour (dead keys).
* **System:** Prevents conflicts between language settings and keyboard mappings.
