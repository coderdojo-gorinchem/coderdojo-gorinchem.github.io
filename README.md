# De website voor CoderDojo Gorinchem

Deze repository bevat de broncode voor de website van de CoderDojo in Gorinchem.

# De website wijzigen

De inhoud van de website wordt hoofdzakelijk in Markdown files geschreven. Markdown is een eenvoudige opmaaktaal. Indien je niet bekend met Markdown kun je naar [The Markdown Guide](https://www.markdownguide.org/) gaan om meer te leren. Vooral het [Basic Syntax](https://www.markdownguide.org/basic-syntax/) hoofdstuk zal waarschijnlijk nuttig zijn.

De inhoud van de website bevindt zich in de `src` map. Om de website aan te passen kun je eenvoudig bestaande bestanden aanpassen of nieuwe bestanden toevoegen (eventueel in sub-mappen).

De website wordt beheerd door middel van [ReType](https://retype.com/). Indien je meer geavanceerde veranderingen wilt maken aan de website of directe feedback wilt, kun je Retype lokaal draaien door de [quick start](https://retype.com/#quick-start) te volgen. Als je Retype lokaal draait heb je ook de beschikking over een Markdown editor direct in de website. Dit maakt het makkelijker om direct terugkoppeling te krijgen omtrent je veranderingen, zonder dat je die eerst op moet slaan.

## Afbeeldingen gebruiken

Alle afbeeldingen dienen in de `/src/images` map geplaatst te worden. Eventueel in een sub-map die specifiek is voor een bepaald deel van de site, zodat gerelateerde afbeeldingen bij elkaar geordend zijn.

Wanneer een afbeelding vanuit een Markdown file gerefereerd wordt, kan dat door een relatief pad te gebruiken ten opzichte van de Markdown file, bijvoorbeeld `../images/coderdojo-logo.png`, of een absoluut pad, bijvoorbeeld `/images/coderdojo-logo.png`. Absolute paden zijn relatief ten opzichte van de "deployment" van de website. In de praktijk komt dit neer op dat de paden relatief zijn ten opzichte van de `src` map. Retype zorgt er automatisch voor dat het juiste pad gebruikt wordt als de website gepubliceerd wordt.

Elke manier van refereren heeft voor en nadelen. Relatieve paden zorgen ervoor dat afbeeldingen ook blijven werken als de Markdown files direct op GitHub bekeken worden, maar de paden zijn soms vervelender te lezen door alle `../` instructies en zijn minder robuust bij het verplaatsen van Markdown files. Absolute paden zijn daarentegen doorgaans korter en hoeven niet verandert te worden als de Markdown file verplaatst, maar ze werken niet wanner de Markdown bestanden direct op GitHub bekeken worden.

## Wijzigingen publiceren

De website is opgeslagen in een Git repository en gehost op [GitHub](https://github.com). Git is een versiebeheersysteem. Wanneer er wijzigingen worden gedetecteerd in de Git repository wordt de website automatisch gepubliceerd.

Voor eenvoudige veranderingen kunnen bestanden direct op GitHub aangepast worden. Navigeer in GitHub naar het bestand wat je wilt aanpassen of naar de locatie waar je een nieuw bestand wilt toevoegen en klik op de gewenste actie, bijvoorbeeld het potlood icoon of de _Add file_ knop. Wanneer je tevreden bent met je wijzigingen klik je op _Commit changes&hellip;_ en laat je een beschrijving achter.
