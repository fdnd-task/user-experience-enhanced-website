# Enhanced Website

## Performant Images
Over hoe je images kunt gebruiken in je website volgens het principe van Progressive Enhancement.

Je bent vast wel eens deze twee punten tegengekomen in de lighthouse test:

⚠️ [Serve images in next-gen formates](https://developer.chrome.com/docs/lighthouse/performance/uses-webp-images)

⚠️ [Properly size images](https://developer.chrome.com/docs/lighthouse/performance/uses-responsive-images)

Door gebruik te maken van _Responsive Images_ kan je dit voorkomen.

## Wat zijn responsive images

Responsive images helpen de browser om het beste plaatje te kiezen voor de eindgebruiker. Daarmee houdt de browser rekening met de internet snelheid, het device en de grootte van het scherm. Wij geven de browser een aantal opties en de browser kiest dan zelf wat de beste is met alle variabelen voor de eindgebruiker. We hebben hiervoor drie opties: `srcset`, `picture` in html en `image-set` in CSS (voor backgrounds).

Dit zorgt voor een betere _User Experience_ en performance. Zie [#21 Do we use adaptive media loading and client hints](https://www.smashingmagazine.com/2021/01/front-end-performance-2021-free-pdf-checklist/#assets-optimizations) van de Frontend Performance Checklist.

### Picture

`<picture>` is een HTML element waar we verschillende `<source>` elementen aan kunnen meegeven en een default, zodat we de browser op weg helpen met de juiste afbeelding te kiezen. Picture wordt ook veel voor _art direction_ gebruikt. Denk aan een portrait foto die goed werkt op mobiel, maar een andere ratio moet krijgen op desktop. 

[MDN documentatie `<picture>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/picture)

### Srcset

We kunnen het `srcset` attribuut gebruiken in `<img>` en in `<source>` elementen. Hiermee kunnen we de browser vertellen dat we verschillende afbeeldingsformaten hebben, zodat die zelf de juiste keuze kan maken. In combinatie met het `sizes` attribuut kun je de browser ook op weg helpen met verschillende media queries. Dit wordt wel [snel ingewikkeld](https://cloudfour.com/thinks/responsive-images-the-simple-way/).

[MDN documentatie `srcset`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLImageElement/srcset)

### Image-set

We kunnen in CSS backgrounds ook responsive images gebruiken dmv `image-set`. Hier kun je een ook weer een lijstje aan formats meegeven, zodat de browser zelf kan kiezen welke het gebruikt.

[MDN documentatie `image-set`](https://developer.mozilla.org/en-US/docs/Web/CSS/image/image-set)

### 👉 Opdracht: Formaten en browserondersteuning
- Ga op zoek naar de verschillende image formats die we kunnen gebruiken op het web
- Schrijf ze op het bord, bijv .jpg en hoe goed ze ondersteund worden door browsers


## Hoe gebruiken we responsive images

Before:
```html
  <img src="plaatje.png" alt="Plaatje" width="400" height="300">
```

After:
```html
  <picture>
    <source type="image/avif" srcset="plaatje.avif">
    <source type="image/webp" srcset="plaatje.webp">
    <img src="plaatje.png" alt="Plaatje" width="400" height="300">
  </picture>
```

### 👉 Opdracht: `<picture>` element

🛠️ Maak een demo, in je learning journal, met het picture element, waar je verschillende formaten gebruikt. Kijk in de network tab welke afbeelding er wordt gekozen. Test dit ook met een oude browser via Browserstack. Wat zijn de verschillen?

💪 **Voor de hardlopers**

👉 Je kunt met JavaScript en de [`currentSrc` property](https://developer.mozilla.org/en-US/docs/Web/API/HTMLImageElement/currentSrc) de source van het gekozen plaatje console.loggen.

### 👉 Opdracht: Resolution switching

Je kunt met het `media` attribuut in het `<source>` element verschillende varianten van dezelfde afbeelding laten tonen. Een extra laag van _Progressive Enhancement_. Dit gaat verder dan alleen de width media query, je kunt de hele lijst aan [media queries](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_media_queries/Using_media_queries) gebruiken. Daarnaast kun je ook rekening houden met de hoeveelheid _DPR_ van de eindgebruiker.

```html
  <picture>
    <source media="(min-width: 600px)" type="image/avif" srcset="plaatje-groot.avif">
    <source type="image/avif" srcset="plaatje.avif">
    <source type="image/webp" srcset="plaatje.webp">
    <img src="plaatje.png" alt="Plaatje" width="400" height="300">
  </picture>
```

🛠️ Maak een tweede demo waar je ten minste drie verschillende media queries toepast.

💪 **Voor de hardlopers**

👉 Je kunt met `.currentSrc` en het [MediaQueryList change](https://developer.mozilla.org/en-US/docs/Web/API/MediaQueryList/change_event) event de source van het gekozen plaatje tonen, terwijl je je scherm resized. 


### 👉 Opdracht: Art direction

We hebben nu voornamelijk gekeken naar dezelfde afbeelding serveren op verschillende formaten voor performance en Progressive Enhancement redenen. Waar het `<picture>` element ook veel voor wordt gebruikt is _art direction_. Een afbeelding die op een breed _landscape_ scherm goed werkt, werkt misschien juist op een smal _portrait_ scherm weer minder goed. Door goed na te denken over de art direction van je afbeeldingen kun je de beste versie meegeven voor de eindgebruiker.

```html
  <picture>
    <source media="(orientation: portrait)" type="image/avif" srcset="plaatje-portait.avif" width="300" height="400">
    <source type="image/avif" srcset="plaatje.avif">
    <source type="image/webp" srcset="plaatje.webp">
    <img src="plaatje.png" alt="Plaatje" width="400" height="300">
  </picture>
```

🛠️ Maak een derde demo waarin je art direction toepast.

### 👉 Opdracht: performant attributes

🛠️ Er zijn nog een aantal optimalisaties die je kunt toepassen om images nog meer performant te maken. Ga op zoek welke `attributen` (zijn er meerdere) je hiervoor kunt gebruiken en schrijf ze op het bord. Maak een issue en beschrijf daar waar je deze attributen wilt gaan toepassen.

### Bronnen

- [Do we use adaptive media loading and client hints?- Frontend Performance Checklist #21](https://www.smashingmagazine.com/2021/01/front-end-performance-2021-free-pdf-checklist/#21)
- [MDN: Using responsive images in HTML](https://developer.mozilla.org/en-US/docs/Web/HTML/Guides/Responsive_images)
- [Responsive Images 101, Part 1: Definitions](https://cloudfour.com/thinks/responsive-images-101-definitions/)
- [Responsive Images the Simple Way](https://cloudfour.com/thinks/responsive-images-the-simple-way/)


## Responsive Images met de Directus API in je project

Je kunt met de Directus API verschillende bestandsformaten en groottes opvragen om met responsive images aan de slag te gaan. Waarschijnlijk heb je nu zoiets als:

```html
  <img src="https://fdnd-agency.directus.app/assets/{{ photo.id }}" alt="Alternatieve tekst">
```

Dat kun je nu gaan upgraden, met de info uit de demo's die je hierboven hebt gemaakt, naar:

```html
<picture>
   <source type="image/avif" srcset="https://fdnd-agency.directus.app/assets/{{ photo.id }}?format=avif">
   <source type="image/webp" srcset="https://fdnd-agency.directus.app/assets{{ photo.id }}?format=webp">
   <img src="https://fdnd-agency.directus.app/assets/{{ photo.id }}" width="{{ photo.width }}" height="{{ photo.height }}" alt="Alternatieve tekst">
</picture>
```

### Performant images toepassen op je leertaak
Lees in de documentatie van Directus hoe je de `width`, `height`, `quality` en meer kunt opvragen. Zie de workshop [layout-shift](https://github.com/fdnd-task/user-experience-enhanced-website/blob/main/docs/layout-shift.md) hoe je dat ook alweer doet in Liquid. 

🛠️ Ga in je project aan de slag met responsive images om de user experience te verbeteren op een performant en Progressively Enhanced manier.

👉 Maak een issue over performant images, analyseer het 'probleem' in je project.

👉 Doe een Lighthouse performance test vooraf, en een test achteraf.

👉 Documenteer de verbetering. Hiermee pas je standaarden op het gebied van performance toe (hint hint, DoD 😉).

### Bronnen

- [Image optimization in Directus](https://learndirectus.com/image-optimization-in-directus/)
- [Transform files with Directus](https://directus.io/docs/guides/files/transform)
