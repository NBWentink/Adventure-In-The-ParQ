# Handleiding — Adventure in the ParQ Prototype

## Overzicht

Dit prototype draait als webpagina via GitHub Pages en is te bekijken op een iPad of computer. Alle inhoud staat in één bestand (`index.html`) en de bijbehorende bestanden staan geordend in submappen.

---

## Mappenstructuur

```
Prototype/
├── index.html                  ← Alle schermen, logica en stijlen
└── assets/
    ├── achtergronden/          ← Park- en jungleachtergrond, grondafbeeldingen
    ├── lettertypes/            ← Thumpa.otf (het lettertype)
    ├── mascottes/              ← Alle mascottes (welkom, groep, voltooid, etc.)
    ├── ui/                     ← Knoppen, iconen, QR-overlay, medailles, kaart
    ├── audio/                  ← Algemene audio (intro, voltooiing)
    └── opdrachten/
        ├── groep3/
        │   ├── opdracht1/
        │   │   ├── state-1.png     ← Animatieframe 1
        │   │   ├── state-2.png     ← Animatieframe 2
        │   │   ├── state-3.png     ← Animatieframe 3  (indien van toepassing)
        │   │   ├── instructie.mp3  ← Audio bij de opdracht
        │   │   └── voltooid.mp3    ← Audio na voltooiing
        │   ├── opdracht2/
        │   ├── opdracht3/
        │   └── opdracht4/
        └── groep4/
            ├── opdracht1/
            ├── opdracht2/
            ├── opdracht3/
            └── opdracht4/
```

---

## Teksten aanpassen

Alle opdrachtteksten staan bij elkaar in `index.html`. Zoek naar het gedeelte:

```
const opdrachtenPerGroep = {
```

Hieronder staat per groep en per opdracht een blok met de volgende velden:

| Veld            | Betekenis                                               |
|-----------------|--------------------------------------------------------|
| `titel`         | Kleine titel bovenin het scherm ("Opdracht 1")          |
| `naam`          | Interne naam van de opdracht (bijv. "Rivier")           |
| `instructie`    | De opdrachttekst die de leerlingen lezen/horen         |
| `voltooid`      | De tekst na het voltooien van de opdracht              |
| `voortgangTekst`| De tekst op het voortgangsscherm (tussenstand)         |

**Voorbeeld:**
```js
instructie: 'Oh nee! Er stroomt hier een grote rivier...',
voltooid:   'Dat hebben jullie goed gedaan!...',
```

---

## Afbeeldingen vervangen

### Animatieframes van een opdracht

Elke opdracht heeft één of meerdere animatieframes (de "stop-motion" afbeeldingen). Deze staan in:

```
assets/opdrachten/groep[X]/opdracht[Y]/state-[Z].png
```

**Vervangen:** Sla het nieuwe bestand op met exact dezelfde naam (`state-1.png`, `state-2.png`, etc.) in dezelfde map.

> **Tip:** De afbeeldingen zijn het scherpst bij een breedte van **1668 pixels** (dubbele resolutie voor iPad-retinasherm).

### Frames toevoegen of verwijderen

Het aantal frames per opdracht staat in `index.html` in het veld `states`:

```js
states: [
  'assets/opdrachten/groep3/opdracht1/state-1.png',
  'assets/opdrachten/groep3/opdracht1/state-2.png',
  'assets/opdrachten/groep3/opdracht1/state-3.png'
]
```

Voeg een regel toe of verwijder een regel om frames toe te voegen of te verwijderen.

### Mascottes

De mascottes staan in `assets/mascottes/`. De volgende bestanden worden actief gebruikt:

| Bestand                | Wanneer zichtbaar                          |
|------------------------|---------------------------------------------|
| `mascotte-welkom.png`  | Groepskeuze-scherm, nog niets geselecteerd  |
| `mascotte-groep3.png`  | Groepskeuze-scherm, Groep 3 geselecteerd    |
| `mascotte-groep4.png`  | Groepskeuze-scherm, Groep 4 geselecteerd    |
| `mascotte-voltooid.png`| Voltooiingsscherm na een opdracht           |
| `mascotte-compleet.png`| Eindscherm (alle opdrachten gedaan)         |
| `Mascotte_Links.png`   | QR-scanscherm (wijst naar de camera)        |

---

## Audio vervangen

Audio per opdracht staat in:

```
assets/opdrachten/groep[X]/opdracht[Y]/instructie.mp3   ← bij de opdracht
assets/opdrachten/groep[X]/opdracht[Y]/voltooid.mp3     ← na voltooiing
```

Algemene audio:

```
assets/audio/jungle-avontuur.mp3   ← intro/achtergrondmuziek
assets/audio/opdracht-compleet.mp3 ← geluid alle opdrachten klaar
```

**Vervangen:** Zet het nieuwe `.mp3`-bestand op exact dezelfde locatie met exact dezelfde naam.

---

## Een nieuwe groep toevoegen

1. **Maak mappen aan:**
   ```
   assets/opdrachten/groep5/opdracht1/
   assets/opdrachten/groep5/opdracht2/
   ...
   ```

2. **Voeg afbeeldingen en audio toe** in die mappen (zie structuur hierboven).

3. **Voeg de groep toe in `index.html`**, zoek naar `const opdrachtenPerGroep = {` en voeg na de bestaande groepen toe:
   ```js
   5: [
     {
       id: 1, titel: 'Opdracht 1', naam: 'Naam opdracht',
       instructie: 'De opdrachttekst...',
       voltooid: 'Voltooiingstekst...',
       voortgangTekst: 'Voortgangstekst...',
       isLaatste: false,
       states: [
         'assets/opdrachten/groep5/opdracht1/state-1.png',
         'assets/opdrachten/groep5/opdracht1/state-2.png'
       ]
     },
     // ... opdrachten 2, 3, 4
   ]
   ```

4. **Voeg de groepsknop toe op scherm 02** in `index.html`, zoek naar `groep-circle-4` en voeg daarna toe:
   ```html
   <div id="groep-circle-5" class="groep-circle layer" style="left:XXXpx;top:280px;" onclick="selectGroep(5)">
     <span class="groep-lbl">GROEP</span>
     <span class="groep-nr">5</span>
     <span class="groep-leerlingen">XX leerlingen</span>
   </div>
   ```

5. **Voeg een mascotte toe** voor de nieuwe groep in `selectGroep()` (zoek op `groep-mascot-center`):
   ```js
   else if (nr === 5) mascot.src = 'assets/mascottes/mascotte-groep5.png';
   ```

---

## Publiceren (GitHub Pages)

Het prototype staat live op GitHub Pages. Na elke wijziging:

1. Sla de bestanden op
2. Open **GitHub Desktop**
3. Schrijf een korte beschrijving (bijv. "Tekst opdracht 3 aangepast")
4. Klik **Commit to main**
5. Klik **Push origin**

Na een minuut of twee is de wijziging live op het iPad-prototype.

---

## Aandachtspunten

- Verander **nooit** de bestandsnamen van actieve bestanden — de HTML verwijst er direct naar.
- Afbeeldingen mogen maximaal **~300 KB** zijn voor snelle laadtijden op een iPad.
- Audio is het beste in **MP3-formaat** (44.1 kHz, stereo of mono).
- De pagina is ontworpen voor een iPad-scherm van **834 × 1194 pixels**.
