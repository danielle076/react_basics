## Context

Als je een React applicatie bouwt, zul je regelmatig data doorgeven via properties. Je kunt data echter alleen doorgeven van boven naar beneden, <b>niet terug omhoog</b>. Daarbij kan het voorkomen, door de complexiteit van de applicatie, dat je sommige data door ontzettend veel componenten moeten laten stromen. Terwijl misschien alleen die button - 5 niveau's diep - de data nodig heeft. In sommige situaties moeten zelfs bijna alle componenten toegang hebben tot een stukje data. Dit soort situaties doen zich vaak voor wanneer je:

- Een applicatie hebt die tweetalig is, waardoor bijna alle componenten zich bewust moeten zijn van de huidige geselecteerde taal.
- Een light- en dark-mode interface hebt, waarbij alle componenten met één druk op de knop moeten wisselen van styling.
- Een applicatie hebt waarbij ingelogde gebruikers afgeschermde content kunnen bekijken. Alle pagina's moeten dan weten of de gebruiker ingelogd en geautoriseerd is om de content te bekijken.

`React Context` lost dit probleem voor ons op. Er wordt een overkoepelend stukje state aangemaakt waar ieder component in de applicatie bij zou kunnen. Als een component de informatie uit de context nodig heeft, kan het dit direct aanspreken (<i>consumer</i>), omdat een top-level component deze data in de context aanbied (<i>provider</i>).

Dus context geeft ons een manier om data door de componenten-tree door te geven, zonder dat we properties moeten doorgeven op ieder niveau.

Wanneer je context op de verkeerde manier implementeert zorg je voor veel onnodige re-renders van veel componenten.

### Hoe pak je context?
Je maakt een aparte "context" voor elk stukje data dat gebundeld kan worden.

Daarmee bedoelen we, stel we hebben een dark en een light UI thema daar maak je dan een `ThemeContext` voor.

Stel je hebt ook nog taal selectie in de applicatie, dan maak je daar een aparte `LanguageContext` voor.

Waarom stop je niet alle context bijelkaar: dat komt omdat alle elementen die gebruik maken van de data uit de context opnieuw worden gerenderd op het moment dat een klein stukje data uit die context veranderd. Al die re-renders willen we voorkomen.

### Voorbeeld context

Een context aanmaken voor een click-counter is alsof je een tosti doorsnijdt met een kettingzaag. Probeer je voor te stellen dat dit een ingewikkeldere applicatie zou zijn en dat we daarom Context gaan implementeren.

Er komen drie componenten in deze applicatie die allemaal toegang moeten hebben tot dezelfde data:
1. Button component die de count verhoogt
2. Button component die de count verlaagt
3. Result component die de count laat zien

#### Stap 1 - App.js

    import React from 'react';
    import './App.css';
    
    function App() {
        return (
            <div>
                Hoi!
            </div>
        );
    }
    
    export default App;

#### Stap 2 - map components aanmaken + Result.js

    import React from 'react';
    
    function Result() {
         return (
            <h1>
                0
            </h1>
        );
    }
    
    export default Result;

#### Stap 3 - IncrementButton.js in map components
    
    import React from 'react';
    
    function IncrementButton() {
        return (
            <button type="button">
                Increment
            </button>
        );
    }
    
    export default IncrementButton;

#### Stap 4 - DecrementButton.js in map components

    import React from 'react';
    
    function DecrementButton() {
        return (
            <button type="button">
                Decrement
            </button>
        );
    }
    
    export default DecrementButton;

#### Stap 5 - pagina's van map components implementeren in App.js

    import React from 'react';
    import Result from './components/Result';
    import DecrementButton from './components/DecrementButton';
    import IncrementButton from './components/IncrementButton';
    import './App.css';
    
    function App() {
        return (
            <>
                <Result/>
                <DecrementButton/>
                <IncrementButton/>
            </>
        );
    }
    
    export default App;

#### Stap 6 - Stappenplan context
- Stap 7: Context maken en exporteren: `CounterContext`
- Stap 8: Context importeren
- Stap 9: Context Provider maken en omwikkelen om het hoogste element
- Stap 10: Stukje data maken die via Provider in Context gaat
- Stap 11: Context importeren
- Stap 12: Componenten “abonneren” op de context met `useContext`
- Stap 13: Apart functie component voor de provider maken zodat de logica daar naartoe kan. De oude weghalen uit App.js en omwikkelen in index.js
- Stap 14: CounterContext.js state toevoegen in de provider en twee functies maken die de waarde in de state aanpassen
- Stap 15: Buttons abonneren op de context functies door `useContext` te gebruiken