## Wat is React?

React is een efficiënte en flexibele JavaScript-bibliotheek voor het bouwen van gebruikersinterfaces (React zelf is geschreven met JavaScript). Het splitst complexe UI's op in kleine, geïsoleerde code die "componenten" wordt genoemd. Door deze componenten te gebruiken, houdt React zich alleen bezig met wat je op de voorpagina van een website ziet.

Componenten zijn onafhankelijk en herbruikbaar. Het kunnen JavaScript-functies of -klassen zijn. In beide gevallen retourneren ze een stukje code dat een deel van een webpagina weergeeft.

Hier is een voorbeeld van een functiecomponent die een `<h2>`-element op de pagina rendert:

    function Name() {
    return <h2>Hi, my name is Daniëlle!</h2>;
    }

En hier is een klasse component die dezelfde rendering doet:

    class Person extends React.Component {
    render() {
    return <h2>Hi again from Daniëlle!</h2>;
      }
    }

Klasse componenten worden bijna niet meer gebruikt en het zijn vooral functions die je zult tegenkomen.

Het is je misschien opgevallen dat er een vreemde mengeling van HTML en JavaScript in elk onderdeel zit. React gebruikt een taal genaamd JSX die het mogelijk maakt HTML te mengen met JavaScript.

Het is misschien verrassend om te leren dat de HTML-code die met React wordt gekoppeld heel eenvoudig is:

    <div id="root"></div>

Het is een `<div>` element met een id dat dient als een container voor een React app. Wanneer React zijn componenten rendert, zoekt het naar dit id om naar te renderen. De pagina is leeg voor deze rendering.

## De applicatie starten
Als je een project gecloned hebt naar jouw locale machine, installeer je eerst de node_modules door het volgende commando in de terminal te runnen:

`npm install`

Wanneer dit klaar is, kun je de applicatie starten met behulp van:

`npm start`

of gebruik de WebStorm knop (npm start). Open http://localhost:3000 om de pagina in de browser te bekijken.
Begin met het maken van wijzigingen in `src/App.js`: elke keer als je een bestand opslaat, zullen de wijzigingen te zien zijn op de webpagina.

##Codesandbox.io

Wanneer je React niet via een lokale machine wilt uitvoeren kun je dit online doen via https://codesandbox.io/. Dit is een webtool waar je React in kan schrijven en oefenen.

