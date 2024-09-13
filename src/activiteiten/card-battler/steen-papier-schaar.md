---
categories:
  - Activiteiten
tags:
  - CSS
  - HTML
  - JavaScript
  - Spel
---

# Steen, Papier, Schaar

<!-- TODO: Screenshot van het eindresultaat -->

Als eerste stap in het bouwen van een card battler, gaan we een versie van _steen, papier, schaar_ maken.

Voor deze activiteit heb je Visual Studio Code nodig en een project map. Indien je deze nog niet op je computer geïnstalleerd hebt, volg dan [deze handleiding](/handleidingen/visual-studio-code).

## Voorbereiding

Als eerste hebben we een bestand nodig waar we het spel in gaan schrijven. Maak in de project map een nieuw bestand met de naam `index.html`, open het bestand en voeg de volgende inhoud aan het bestand toe. Dit zorgt er voor dat we het spel kunnen gaan bouwen en dat het er goed uit gaat zien als we klaar zijn.

```html Lege pagina template
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Card Battler - Steen, Papier, Schaar</title>

    <link
      rel="stylesheet"
      media="(prefers-color-scheme:light)"
      href="https://cdn.jsdelivr.net/npm/@shoelace-style/shoelace@2.16.0/cdn/themes/light.css"
    />
    <link
      rel="stylesheet"
      media="(prefers-color-scheme:dark)"
      href="https://cdn.jsdelivr.net/npm/@shoelace-style/shoelace@2.16.0/cdn/themes/dark.css"
      onload="document.documentElement.classList.add('sl-theme-dark');"
    />

    <script
      type="module"
      src="https://cdn.jsdelivr.net/npm/@shoelace-style/shoelace@2.16.0/cdn/shoelace-autoloader.js"
    ></script>

    <style>
      html {
        background-color: var(--sl-color-neutral-0);
        font-family: var(--sl-font-sans);
      }

      :not(:defined) {
        visibility: hidden;
      }
    </style>
  </head>

  <body>
    Hallo, Steen, Papier, Schaar!
  </body>
</html>
```

Toets nu <kbd>Ctrl/Cmd</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd> in en type _liprin_, kort voor _Live Preview: Show Preview (Internal Browser)_, gevolgd door <kbd>Enter</kbd>. Er verschijnt nu een browser venster naast de zojuist getypte code die de pagina laat zien.

![](/images/card-battler/vscode-live-preview.png)

Deze preview kun je open laten staan terwijl je aan het project werkt. De pagina zal automatisch de veranderingen die gemaakt worden in de editor oppikken. Probeer _Hallo_ maar eens te veranderen in _Tot ziens_ en zie hoe de preview updatet terwijl je typt. Mocht je de preview per ongeluk sluiten, dan kun je hem weer openen met de instructies in de vorige paragraaf.

Om de volgende tekst iets begrijpbaarder te houden introduceren we een naam voor de stukjes tekst die in vishaakjes (`<` en `>`) geschreven zijn. Deze stukjes tekst noemen we _tags_. Bijvoorbeeld `<body>` noemen we de "body tag" en `<title>` noemen we de "title tag". De meeste tags hebben een begin (`<body>`, `<title>`) en een eind (`</body>`, `</title>`), wanneer we de tekst tussen deze tags willen aanpassen, dan zeggen we "wijzig de tekst binnen de body-tags".

## Het speelveld

_Steen, papier, schaar_ wordt gespeeld met 2 spelers, met elk 3 acties die gespeeld kunnen worden. We zullen dit visualiseren als 2 spelers die tegenover elkaar zitten, elk 3 kaarten vast hebben met ruimte tussen de sets kaarten in om een kaart te kunnen spelen.

Schematisch ziet dat er als volgt uit

![](/images/card-battler/steen-papier-schaar-speelveld.png)

HTML pagina's worden opgebouwd door middel van "rechthoekige blokken". In de schematische weergave hierboven zijn deze blokken goed zichtbaar. Een veel gebruikte "tag" om deze blokken op te kunnen bouwen is de `div`-tag. Laten we stap voor stap het speelveld opbouwen door gebruik te maken van deze tag.

Als eerste hebben we drie blokken nodig die op elkaar gestapeld staan. Dit zijn het blok waar de kaarten van de tegenstander in liggen, het blok waar de gespeelde kaarten in terecht komen en het blok waar de kaarten van de speler in liggen. Vervang de tekst in de `body`-tag door de volgende drie regels.

```html #2-4
<body>
  <div class="kaarten" id="tegenstander"></div>
  <div class="kaarten" id="gespeelde-kaarten"></div>
  <div class="kaarten" id="speler"></div>
</body>
```

De `id` namen helpen ons later om kaarten tussen de verschillende blokken heen en weer te bewegen en de `class` zorgt er voor dat we de blokken er eenvoudig hetzelfde uit kunnen laten zien.

Door deze verandering is er nu niets meer zichtbaar op de pagina. Laten we de blokken een kleurtje geven zodat we ze weer kunnen zien. Zoek de `style`-tag en voeg gemarkeerde code toe.

```css #5-21
html {
  background-color: var(--sl-color-neutral-0);
  font-family: var(--sl-font-sans);
}

body {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 100dvh;
  margin: 0;
}

#gespeelde-kaarten {
  background-color: var(--sl-color-blue-400);
}

#speler,
#tegenstander {
  background-color: var(--sl-color-red-400);
}
```

```css #4-10
:not(:defined) {
  visibility: hidden;
}

.kaarten {
  align-items: center;
  display: flex;
  flex: 1;
  justify-content: space-around;
}
```

Deze code zorgt er voor dat het spel straks het hele scherm in beslag neemt en dat de kaarten netjes over de beschikbare ruimte worden verdeeld. Het scherm zou er nu als volgt uit moeten zien.

![](/images/card-battler/vscode-speelveld-layout.png)

Nu we gezien hebben hoe alles er ongeveer uit komt te zien, kunnen we de kleuren weer verwijderen en kaarten toevoegen. Verwijder de volgende code.

```css
#gespeelde-kaarten {
  background-color: var(--sl-color-blue-400);
}

#speler,
#tegenstander {
  background-color: var(--sl-color-red-400);
}
```

## De kaarten toevoegen aan het speelveld

Nu we het speelveld hebben opgebouwd kunnen we de kaarten gaan toevoegen. Hiervoor gebruiken we [een speciale "kaart" tag](https://shoelace.style/components/card) waardoor we het spel er eenvoudig goed uit kunnen laten zien.

We gaan in totaal 6 kaarten toevoegen:

1. Een kaart voor steen,
1. Een kaart voor papier,
1. Een kaart voor schaar.

En dat voor 2 spelers. Aan elke kaart gaan we wat informatie toevoegen die aangeeft welke kaart het is, welke andere kaart de kaart verslaat en van wie de kaart is. De "template" voor elke kaart is als volgt:

```html
<sl-card data-eigenaar="<...>" data-type="<...>" data-verslaat="<...>">
  <img src="<de URL naar een plaatje>" slot="image" />

  Tekst voor op de kaart
</sl-card>
```

Deze template gaan we 3 keer toevoegen aan de `div`-tag met `id="tegenstander"` en 3 keer aan de `div`-tag met `id="speler"`. De waardes voor de `data` "attributen" staan in de volgende tabel:

| `data-eigenaar` | `data-type` | `data-verslaat` |
| --------------- | ----------- | --------------- |
| speler          | steen       | schaar          |
| speler          | papier      | steen           |
| speler          | schaar      | papier          |
| tegenstander    | steen       | schaar          |
| tegenstander    | papier      | steen           |
| tegenstander    | schaar      | papier          |

Voor de _Tekst op de kaart_ mag je invullen wat je wilt. Het `src`-attribuut van de `img`-tag moet verwijzen naar een plaatje. Je kunt bijvoorveeld via [Google](https://www.google.com/imghp) zoeken naar een plaatje, met de rechtermuisknop er op klikken en op _Kopieer adres van afbeelding_ te klikken. Het adres kun je dan tussen de quotes van het `src`-attribuut plakken.

Je kunt natuurlijk ook je eigen plaatjes tekenen. Je kunt dan een map aanmaken in de project map met de naam `images` en dan als `src`-attribuut `./images/naam-van-het-plaatje.extensie` gebruiken.

Bijvoorbeeld

```html
<sl-card data-eigenaar="speler" data-type="steen" data-verslaat="schaar">
  <img
    src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcT4NHXKc00snTqu3cBFIltHOvrKBHO-vtC24w"
    slot="image"
  />

  Steen
</sl-card>
```

wordt de kaart

![](/images/card-battler/steen-kaart.png)

Als je klaar bent, dan zou de code er tussen de `body`-tags er ongeveer als volgt uit moeten zien.

```html #2-54
<body>
  <div class="kaarten" id="tegenstander">
    <sl-card
      data-eigenaar="tegenstander"
      data-type="steen"
      data-verslaat="schaar"
    >
      <img src="..." slot="image" />

      Steen
    </sl-card>

    <sl-card
      data-eigenaar="tegenstander"
      data-type="papier"
      data-verslaat="steen"
    >
      <img src="..." slot="image" />

      Papier
    </sl-card>

    <sl-card
      data-eigenaar="tegenstander"
      data-type="schaar"
      data-verslaat="papier"
    >
      <img src="..." slot="image" />

      Schaar
    </sl-card>
  </div>

  <div class="kaarten" id="gespeelde-kaarten"></div>

  <div class="kaarten" id="speler">
    <sl-card data-eigenaar="speler" data-type="steen" data-verslaat="schaar">
      <img src="..." slot="image" />

      Steen
    </sl-card>

    <sl-card data-eigenaar="speler" data-type="papier" data-verslaat="steen">
      <img src="..." slot="image" />

      Papier
    </sl-card>

    <sl-card data-eigenaar="speler" data-type="schaar" data-verslaat="papier">
      <img src="..." slot="image" />

      Schaar
    </sl-card>
  </div>
</body>
```

Om er voor te zorgen dat de kaarten allemaal even groot zijn, voegen we ook nog de gemarkeerde code toe aan de `style`-tag.

```css #4-7
:not(:defined) {
  visibility: hidden;
}

sl-card {
  width: 15%;
}
```

Het spel zou er dan ongeveer als volgt uit moeten zien.

![](/images/card-battler/vscode-kaarten.png)

## Een kaart spelen

Nu we het speelveld hebben vorm gegeven en de kaarten hebben toegevoegd, is het tijd om aan de logica van het spel te beginnen. Als eerste stap gaan het mogelijk maken om een kaart te spelen. Dat houdt in dat we op een kaart in de hand van de "speler" kunnen klikken en dat deze naar het midden van het speelveld bewogen wordt.

De logica voor het spel schrijven we in een `script`-tag. Deze voegen we toe na de `</body>`-tag, maar voor de `</html>`-tag.

```html #2-4
  </body>

  <script>
  </script>
</html>
```

Tenzij anders vermeld kun je er van uitgaan dat vanaf nu alle code binnen de `script`-tags geplaatst wordt. Zodra we de beginselen van de logica van het spel hebben geïmplementeerd, zullen we weer andere delen van de pagina aanpassen.

Als eerste zoeken we alle kaarten van de speler bij elkaar en zorgen er voor dat als er op een kaart geklikt wordt dat er een ronde gespeeld wordt.

```javascript
const spelerContainer = document.getElementById("speler");

spelerContainer
  .querySelectorAll("sl-card")
  .forEach((kaart) =>
    kaart.addEventListener("click", (e) =>
      speelRonde(e.target.closest("sl-card")),
    ),
  );
```

Wanneer er nu op een kaar geklikt wordt de `speelRonde` functie aangeroepen. Maar die hebben we nog niet geschreven, dus gebeurt er nog niets als je klikt. In de volgende stap schrijven we twee nieuwe functies:

1. `speelRonde` waar we de logica gaan schrijven die een hele ronde speelt.
1. `speelKaart` die een enkele kaart van een "hand" naar het midden van het speelveld verplaatst.

```javascript #1-8
  function speelKaart(kaart) {
    kaart.parentNode.removeChild(kaart);
    gespeeldeKaarten.appendChild(kaart);
  }

  function speelRonde(spelerKaart) {
    speelKaart(spelerKaart);
  }
</script>
```

Ook hebben we een referentie nodig naar het midden van het speelveld. Voeg de gemarkeerde code toe.

```javascript #1
const gespeeldeKaarten = document.getElementById("gespeelde-kaarten");
const spelerContainer = document.getElementById("speler");
```

Elke keer als je nu op een kaart in de hand van de speler klikt, wordt deze naar het midden van het speelveld verplaatst.

## De tegenstander een kaart laten spelen

Van in je eentje spelen is natuurlijk snel de lol af, dus wanneer wij een kaart spelen, willen we dat de tegenstander (gespeeld door de computer) ook een kaart kiest. We kunnen hiervoor een functie schrijven die een willekeurige kaart kiest uit de hand van de tegenstander. Deze functie kunnen we dan aanroepen vanuit de `speelRonde` functie. Voeg de volgende functie toe na de definitie van de `speelRonde` functie.

```javascript
function speelTegenstanderKaart() {
  const kaarten = document
    .getElementById("tegenstander")
    .querySelectorAll("sl-card");

  const geselecteerdeKaart =
    kaarten[Math.floor(Math.random() * kaarten.length)];
  speelKaart(geselecteerdeKaart);

  return geselecteerdeKaart;
}
```

En de volgende regel om er voor te zorgen dat de kaarten in de hand van de tegenstander door de functie gevonden kunnen worden.

```javascript #2
const spelerContainer = document.getElementById("speler");
const tegenstanderContainer = document.getElementById("tegenstander");
```

De `speelRonde` functie kunnen we dan als volgt aanpassen.

```javascript #3
function speelRonde(spelerKaart) {
  speelKaart(spelerKaart);
  speelTegenstanderKaart();
}
```

Wanneer we nu een kaart spelen, zal de computer er ook een spelen.

## Een ronde tegelijk spelen

Als er te veel kaarten na elkaar gespeeld worden, dan wordt het midden van het speelveld al snel een rommel. Daarom gaan we het spel aanpassen, zodat je maar 1 kaart per ronde kunt spelen. Waarna de kaarten van iedereen teruggegeven worden.

Om dit mogelijk te maken gaan we eerst de opmaak van het speelveld een klein beetje aanpassen. We gaan een knop toevoegen waar je op kunt klikken om de volgende ronde te starten. Zoek de gemarkeerde regel en vervang de regel door de volgende code.

```html #2
<div id="arena">
  <div class="kaarten" id="gespeelde-kaarten"></div>
  <sl-button class="hidden" id="volgende-ronde">Volgende Ronde</sl-button>
</div>
```

We hebben vervolgens ook wat extra styling nodig om de knop te verbergen als een ronde nog niet klaar is en om ervoor te zorgen dat er wat ruimte is tussen de knop en de gespeelde kaarten.

```css #1-4,9-15
sl-button.hidden {
  display: none;
}

sl-card {
  width: 15%;
}

#arena {
  text-align: center;

  & > * {
    margin-block-start: var(--sl-spacing-large);
  }
}
```

Vervolgens kunnen we de volgende code toevoegen aan de `script`-tags om er voor te zorgen dat de knop wordt weergegeven aan het einde van een ronde.

```javascript #2
const tegenstanderContainer = document.getElementById("tegenstander");
const volgendeRondeKnop = document.getElementById("volgende-ronde");
```

```javascript #2-3
speelTegenstanderKaart();

volgendeRondeKnop.classList.remove("hidden");
```

We kunnen er ook voor zorgen dat er geen nieuwe kaarten gespeeld kunnen worden aan het eind van de ronde.

```javascript #2-5
    function speelRonde(spelerKaart) {
      if (!volgendeRondeKnop.classList.contains("hidden")) {
        return;
      }

      speelKaart(spelerKaart);
```

Tot slot kunnen we er voor zorgen dat als er op de knop geklikt wordt dat alle kaarten terug naar de respectievelijke handen verplaatst worden. Voeg de volgende functie toe vlak voor de `</script>`-tag.

```javascript
function volgendeRonde() {
  gespeeldeKaarten.querySelectorAll("sl-card").forEach((kaart) => {
    kaart.parentNode.removeChild(kaart);
    document.getElementById(kaart.dataset.eigenaar).appendChild(kaart);
  });

  volgendeRondeKnop.classList.add("hidden");
}
```

En roep de functie aan als er op de knop geklikt wordt.

```javascript #2
const volgendeRondeKnop = document.getElementById("volgende-ronde");
volgendeRondeKnop.addEventListener("click", volgendeRonde);
```

## "Klaar"!

Je hebt zojuist een Steen, Papier, Schaar spel gemaakt! Er zijn nog veel uitbreidingsmogelijkheden. Hieronder geven we een paar ideeën, maar je kunt natuurlijk je fantasie de vrije loop laten.
