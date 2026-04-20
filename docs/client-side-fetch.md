# Interactive functionality

## Client-Side Fetch met Server-side partials 
Over het client-side fetchen van data volgens het principe van Progressive Enhancement

### Aanpak

Deze sprint ontwerp en bouw je een interactie met een POST request. Om ervoor te zorgen dat je website het altijd doet, leer je dit te bouwen met de coding strategie _Progressive Enhancement_.

Als je goed weet wat je gaat bouwen (laag 1) en je hebt de POST server-side gebouwd, met een HTML formulier en eenvoudige CSS (laag 2) dan kan je de User Experience verbeteren met client-side JavaScript (laag 3 van Progressive Enhancement). Nu wordt het leuk!

Vandaag ga je eerst bedenken en schetsen hoe je de interactie kan verbeteren met states van de UI stack.
Daarna ga je leren hoe je met client-side JavaScript kunt fetchen, om de gebruiker goede feedback te geven.

<!--
Deze workshop de POST interactie helemaal laten schetsen, inclusief client-side enhancement. laag 3 van PE. 

UI stack en states toevoegen: loading state, success state

Opdracht: Schets een UML diagram met de routing en pseudo-code voor de data-flow en control-flow van de Node-code

Teken de interactie voor de user story in een wireflow. Zorg dat je de verschillende states van het formulier uitwerkt
(het versturen van data, een success state en mogelijke errors, etc…)
Noteer per state de routing
Voeg aan de wireflow een control-flow toe:
Noteer welke data wordt ge-POST, welke data wordt opgehaald met een fetch en welke data wordt doorgegeven aan een volgende functie of methode

Control Flow
Met een Control Flow beschrijf je de logica / structuur van je code. De Control Flow (of Flow of Control) toont de volgorde van methodes en functies die worden uitgevoerd in de code. Zo krijg je een duidelijk overzicht van hoe de code werkt en in welke volgorde.
-->

## Enhancement

<!-- Volgens de *Hierarchy of User Needs* moet je ervoor zorgen dat jouw interactie eerst *functional* en *reliable* is, voordat je het *usable* en *pleasurable* kan maken.

![Hierarchy of User Needs](aarron-walter-user-needs.png)  -->

‼️ Dit betekent dat je jouw interactie eerst met een HTML formulier, POST en Server-side betrouwbaar moet bouwen, zodat je website het altijd doet. Hiervoor heb je de _Empty state_ en _Ideal state_ nodig in je Liquid code. Heb je dat nog niet, zorg dan eerst dat je dat werkend hebt, voordat je verder gaat met client-side enhancements. Gebruik hiervoor de [UI states workshop](https://github.com/fdnd-task/the-web-is-for-everyone-interactive-functionality/blob/main/docs/ui-states.md) uit de eerste week van deze sprint.


_Daarna_ kan je de interface verbeteren—“enhancen”—met client-side JavaScript. Stel dat een (oude) browser zonder dat je het weet bepaalde CSS of JavaScript die je gebruikt niet ondersteunt, dan zal deze 'terugvallen' naar een werkende versie, waardoor de core functionaliteit (jouw interactie) altijd werkt, voor iedereen.

### Loading state en Success state

Met behulp van de UI-Stack kan je verschillende states van een pagina ontwerpen als je met dynamische data werkt. De _Empty state_ heb je al, die kan je tonen als er bijvoorbeeld nog geen Berichten zijn toegevoegd. Of als er nog geen Like is gegeven. Of als je een product nog niet tot Favoriet hebt gemaakt. De _Ideal state_ heb je ook; een gevuld hartje, een lijstje met reacties, of een gevuld winkelmandje.

<!--Een _Loading state_ en _Success state_ komen er in deze stap bij. Of eigenlijk: we gaan de default states die de browser hiervoor biedt _enhancen_.-->
Standaard laat een browser een _loading_ indicator zien terwijl een pagina laadt (vaak in of naast de adresbalk). En als de pagina geladen is, wordt de hele pagina getoond: de _Success state_ (vaak uitgebreid met een extra melding op de pagina). Dat werkt prima, browsers doen dit al jaren, en bezoekers zijn dit gewend.

Maar de volledige pagina verversen als we alleen één Like veranderen, of één reactie toevoegen, of één product aan een winkelmandje toevoegen, dat is wat overdreven. Het werkt overal, maar in veel browsers kunnen we dit prettiger maken voor onze eindgebruikers. Waarschijnlijk ben je inmiddels zelf ook wel toe aan deze stap.

Goed nieuws! We kunnen de standaard formulier _submit_ van de browser tegenhouden, de formuliervelden uit het formulier met client-side JavaScript versturen, en met het antwoord van de server _iets doen_. Hoe precies gaan we verderop in deze workshop leren, maar we moeten ons eerst bewust worden van de extra verantwoordelijkheid die we hiermee krijgen. Als we de _default_ Loading en Success states van de browser niet gebruiken, moeten we hiervoor een alternatief ontwerpen _en_ bouwen.

Beschouw het als een micro-interactie, net als in Sprint 5: op het moment dat een gebruiker bijvoorbeeld op een knop klikt, en er data naar de server wordt verstuurd, kun je een _Loading state_ tonen op die plek. Hiermee geef je _meteen_ op de relevante plek feedback dat er iets gebeurt:

![Loading state](loading-state.gif) 
*Door het tonen van een loading state weet de gebruiker dat er iets gebeurt*

Als het versturen van de data gelukt is, en de browser heeft antwoord gekregen van de server, kun je feedback tonen met een _Success state_:

![Success state](success-state.gif) 
*Door het tonen van een success state weet een gebruiker dat het versturen van data is gelukt*

#### 👉 Loading states en Success states onderzoeken

Zoek met je tafel verschillende voorbeelden van loading states en success states. Gebruik bijvoorbeeld [Codepen](https://codepen.io/) ter inspiratie, waarop je ook kunt zoeken.

Post in Teams mooie voorbeelden van Loading states en Success states.

Bedenk ook hoe je het ontwerp van jouw interactie kunt uitbreiden met deze twee nieuwe states. Voeg hints en relevante bronnen toe aan jouw User Story issue.

#### 👉 Wireflow schetsen met states

<!--Schets de Wireflow van jouw interactie, als je dat nog niet gedaan hebt in [de eerste week](https://github.com/fdnd-task/the-web-is-for-everyone-interactive-functionality/blob/main/docs/user-generated-content.md#wireflow-breakdown-met-urls-routes-en-post). Toon eerst de *Ideal state*, de flow dat alles goed gaat, en de *e*mpty state*, voor als er nog niets is. -->

Voeg de *Loading state* en *Success state* toe toe aan je Wireflow. Ontwerp hoe je de gebruiker goede feedback kan geven als er data wordt verstuurd en geladen, en wat je kan tonen als dit gelukt is. Bijvoorbeeld met een animatie op de Like, of een highlight op een nieuw bericht, zorg ervoor dat de gebruiker weet dat de interactie is gelukt.
<!--Gebruik hiervoor [de states van de UI-Stack](https://github.com/fdnd-task/the-web-is-for-everyone-interactive-functionality/blob/main/docs/ui-states.md): Empty state, Loading state en Success state.--> Voeg deze nieuwe states toe aan je User Story issue.


## Server-side vs. Client-side

In Semester 2 leer je over zowel de server (NodeJS/Express) als de client (de browser). Deze “praten” met elkaar via HTTP en URLs. Een client kan bij een server data ophalen via een `GET` method, en data versturen via een `POST` method.

Server-side weet je precies welke programmeertaal (NodeJS), packages (Express, Liquid) en hardware (via Render bijvoorbeeld) je tot je beschikking hebt. Client-side weet je dat niet; je weet nooit welke browser (versie) of welk apparaat je website bezoekt.

### Client-side Fetch

Server-side heb je in NodeJS al gewerkt met `fetch()`, om data op te halen uit en op te slaan in Directus. Via `fetch()` kun je HTTP requests uitvoeren: `GET`, `POST`, `DELETE`, etc. Fetch is een _standaard_.

Client-side heb je in de meeste browsers met JavaScript ook beschikking over `fetch()`! Alles wat je hierover geleerd hebt de afgelopen weken, werkt dus ook in veel browsers.

Weet je wat dit betekent? De JavaScript code die je in NodeJS hebt geschreven, kun je vrijwel één-op-één in browsers gebruiken. 🤯 Probeer deze code maar eens in je browser Console:

```javascript
const teamResponse = await fetch('https://fdnd.directus.app/items/person/?fields=team&filter[team][_neq]=null&sort=team&groupBy=team')
const teamResponseJSON = await teamResponse.json()
console.log(teamResponseJSON)
```

👉 Probeer een paar van je eigen server-side fetches naar Directus uit in je browser Console, en `console.log()` de resultaten.

Vet hè?

Je kunt niet zomaar naar elke andere website een `fetch()` doen vanuit JavaScript in een browser. Daarvoor is dit te krachtig. Standaard werkt dit alleen voor URLs van hetzelfde _origin_ (domein). Als websites dit wel toe willen staan, moeten ze dit expliciet aangeven, via zogenaamde _Cross-Origin Resource Sharing (CORS) headers_. Directus laat dit bijvoorbeeld wel toe, waardoor bovenstaand voorbeeld werkt.

Het goede nieuws is vooral dat we een `fetch()` in onze client-side JavaScript kunnen gebruiken om bijvoorbeeld een `POST` te doen naar onze eigen Express server. Naar de routes die we dus zelf aangemaakt hebben. Precies dat wat we nodig hebben voor onze interactie!

👉 Onderzoek onderstaand voorbeeld, lees de code comments, en pas de code aan naar jouw eigen project. Zorg dat je met client-side JavaScript jouw formulier kunt versturen.

```html
<!-- Bijvoorbeeld voor deze HTML, maar waarschijnlijk is die van jou net anders -->

{% if liked %}
  <!-- Ideal state -->
  <form method="POST" action="/detail/{{ id }}/unlike" data-enhanced="formulier-{{ id }}">
    <button type="submit">Unlike</button>
  </form>
{% else %}
  <!-- Empty state -->
  <form method="POST" action="/detail/{{ id }}/like" data-enhanced="formulier-{{ id }}">
    <button type="submit">Like</button>
  </form>
{% endif %}

<script type="module">

  // Als er ergens op de pagina een formulier wordt gesubmit..
  // (We maken hier gebruik van Event Delegation)
  document.addEventListener('submit', async function(event) {

    // Hou in een variabele bij welk formulier dat was
    const form = event.target

    // Als dit formulier geen data-enhanced attribuut heeft, doe dan niks speciaals (laat het formulier normaal versturen)
    // Dit doen we, zodat we sommige formulieren op de pagina kunnen 'enhancen'
    // Door ze bijvoorbeeld data-enhanced="true" of data-enhanced="formulier-3" te geven.
    // Data attributen mag je zelf verzinnen: https://developer.mozilla.org/en-US/docs/Learn_web_development/Howto/Solve_HTML_problems/Use_data_attributes
    if (!form.hasAttribute('data-enhanced')) {
      return
    }

    // Voorkom de standaard submit van de browser
    // Let op: hiermee overschrijven we de default Loading state van de browser...
    event.preventDefault()

    // Verzamel alle formuliervelden van het formulier
    let formData = new FormData(form)

    // En voeg eventueel de name en value van de submit button toe aan die data
    // https://developer.mozilla.org/en-US/docs/Web/API/SubmitEvent/submitter
    if (event.submitter) {
      formData.append(event.submitter.name, event.submitter.value)
    }

    // Doe een fetch naar de server, net als hoe de browser dit normaal zou doen
    // Gebruik daarvoor het action en method attribuut van het originele formulier
    // Inclusief alle formuliervelden
    const response = await fetch(form.action, {
      method: form.method,
      body: new URLSearchParams(formData)
    })

    // De server redirect op de normale manier, en geeft HTML terug
    // (De server weet niet eens dat deze fetch via client-side JavaScript gebeurde)
    const responseText = await response.text()

    // Normaal zou de browser die HTML parsen en weergeven, maar daar moeten we nu zelf iets mee
    // Parse de nieuwe HTML en maak hiervan een nieuw Document Object Model in het geheugen
    const parser = new DOMParser()
    const responseDOM = parser.parseFromString(responseText, 'text/html')

    // Zoek in die nieuwe HTML DOM onze nieuwe UI state op, die we via Liquid hebben klaargemaakt
    // We gebruiken hiervoor het eerdere data-enhanced attribuut, zodat we weten waar we naar moeten zoeken
    // In de nieuwe HTML zoeken we bijvoorbeeld naar data-enhanced="true" of data-enhanced="formulier-3"
    // (Hierdoor kunnen we ook meerdere formulieren op dezelfde pagina gebruiken)
    const newState = responseDOM.querySelector('[data-enhanced="' + form.getAttribute('data-enhanced') + '"]')

    // Overschrijf ons formulier met de nieuwe HTML
    // Hier wil je waarschijnlijk de Loading state vervangen door een Success state
    form.outerHTML = newState.outerHTML

  })

</script>
```

#### Bronnen

- [Using the Fetch API @ MDN](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)
- [Using data attributes @ MDN](https://developer.mozilla.org/en-US/docs/Learn_web_development/Howto/Solve_HTML_problems/Use_data_attributes)
- [Retrieving a FormData object from an HTML form @ MDN](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest_API/Using_FormData_Objects#retrieving_a_formdata_object_from_an_html_form)
- [Fetch Standard @ WHATWG](https://fetch.spec.whatwg.org/)
- [Cross-Origin Resource Sharing (CORS) @ MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/CORS) (geavanceerd)

### Extra states toevoegen

👉 Breid bovenstaande JavaScript code aan met een Loading state en Success state, zoals je hebt ontworpen. Gebruik hiervoor de technieken die je in Sprint 5 hebt geleerd, zoals de `classList`.

💪 De View Transition API leent zich erg goed voor deze enhancement, met name voor de Success state. Onderzoek hoe je deze met Progressive Enhancement in kunt zetten in bovenstaande code. Hou rekening met ondersteuning in verschillende browsers.

#### Bronnen

- [classList property @ MDN](https://developer.mozilla.org/en-US/docs/Web/API/Element/classList)
- [Using the View Transition API @ MDN](https://developer.mozilla.org/en-US/docs/Web/API/View_Transition_API/Using)
- [View Transitions @ 12 Days of Web](https://12daysofweb.dev/2023/view-transitions/)