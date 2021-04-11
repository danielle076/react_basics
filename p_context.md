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
- Stap 18: Buttons abonneren op de context functies door `useContext` te gebruiken

#### Stap 7 - map context aanmaken + CounterContext.js
Ook al heb je maar 1 context, zet hem altijd in de map context en niet in de map components, dit is verwarrend.

Het is netjes wanneer je altijd een leeg object `{}` aan de `createContext` meegeeft.

    import {createContext} from 'react';
    
    export const CounterContext = createContext({});

#### Stap 8 - App.js context importeren
Normaliter wikkelen we context om het app component in index.js, maar omdat we ook nog wat data willen gaan maken, gaan we hem voor nu in de App.js zetten.

    import {CounterContext} from './context/CounterContext';

#### Stap 9 - App.js context provider + omwikkelen op het hoogste element (voor nu om App.js, later om index.js)

    import React from 'react';
    import Result from './components/Result';
    import DecrementButton from './components/DecrementButton';
    import IncrementButton from './components/IncrementButton';
    import {CounterContext} from './context/CounterContext';
    import './App.css';
    
    function App() {
    return (
        <CounterContext.Provider>
            <Result/>
            <DecrementButton/>
            <IncrementButton/>
        </CounterContext.Provider>
    );
    }
    
    export default App;

#### Stap 10 - App.js data maken die via Provider in context gaat
We maken een data object aan waarin count staat.

Als we dat data object willen meegeven aan de provider dan doen we dit via de property `value`.

    import React from 'react';
    import Result from './components/Result';
    import DecrementButton from './components/DecrementButton';
    import IncrementButton from './components/IncrementButton';
    import {CounterContext} from './context/CounterContext';
    import './App.css';
    
    function App() {
    const data = {
    count: 0,
    }
    
        return (
            <CounterContext.Provider value={data}>
                <Result/>
                <DecrementButton/>
                <IncrementButton/>
            </CounterContext.Provider>
        );
    }
    
    export default App;

#### Stap 11 - Result.js context importeren

    import {CounterContext} from '../context/CounterContext';

#### Stap 12 - Result.js componenten “abonneren” op de context met useContext

We gaan `CounterContext` gebruiken en daar hebben we `useContext` functie voor nodig.

We maken een variabele const aan en we moeten iets destructuren uit dat data object. Wat willen we uit de CounterContext halen, wat hebben we in dat dat object gezet: `count`.

In `return` gaan we `count` gebruiken.

    import React, {useContext} from 'react';
    import {CounterContext} from '../context/CounterContext';
    
    function Result() {
    const {count} = useContext(CounterContext);
    
        return (
            <h1>{count}</h1>
        );
    }
    
    export default Result;

#### Stap 13 - App.js state aanmaken
We hebben vaak geen vaste data, maar data dat elke keer veranderd. Dit doen we met state: `const [count, setCount] = useState(0)`

    import React, {useState} from 'react';
    import Result from './components/Result';
    import DecrementButton from './components/DecrementButton';
    import IncrementButton from './components/IncrementButton';
    import {CounterContext} from './context/CounterContext';
    import './App.css';
    
    function App() {
    const [count, setCount] = useState(0)
    const data = {
    count: 0,
    }
    
        return (
            <CounterContext.Provider value={data}>
                <Result/>
                <DecrementButton/>
                <IncrementButton/>
            </CounterContext.Provider>
        );
    }
    
    export default App;

#### Stap 14 - App.js logica state
Als we de logica hier willen houden in App.js, dan zorgen we dat de waarde van `count` in het dataobject wordt gezet.

De `setCount` functie willen we beschikbaar maken, deze zet je onder de property count. Nu kunnen we ons gaan abonneren op het setCount functie.

Deze logica die we creëren wilt App.js niets mee te maken hebben. Deze logica willen we beheren in de provider.

    import React, {useState} from 'react';
    import Result from './components/Result';
    import DecrementButton from './components/DecrementButton';
    import IncrementButton from './components/IncrementButton';
    import {CounterContext} from './context/CounterContext';
    import './App.css';
    
    function App() {
    const [count, setCount] = useState(0)
    const data = {
    count: count,
    setCount: setCount,
    }
    
        return (
            <CounterContext.Provider value={data}>
                <Result/>
                <DecrementButton/>
                <IncrementButton/>
            </CounterContext.Provider>
        );
    }
    
    export default App;

#### Stap 15 - Aparte functie component voor de provider gemaakt, zodat de logica daar naartoe kan. De oude weggehaald uit App.js en omwikkelt in index.js
<i> CounterContext.js</i>

    import React, {createContext, useState} from 'react';
    
    export const CounterContext = createContext({});
    
    function CounterContextProvider() {
    const [count, setCount] = useState(0)
    
        const data = {
            count: count,
            setCount: setCount,
        }
    
        return (
            <CounterContext.Provider value={data}>
                <Result/>
                <DecrementButton/>
                <IncrementButton/>
            </CounterContext.Provider>
        );
    }
    
    export default CounterContextProvider;

<i> App.js </i>

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

<i> index.js</i>

    import React from 'react';
    import ReactDOM from 'react-dom';
    import './index.css';
    import App from './App';
    import CounterContextProvider from './context/CounterContext'
    import reportWebVitals from './reportWebVitals';
    
    ReactDOM.render(
        <React.StrictMode>
            <CounterContextProvider>
                <App/>
            </CounterContextProvider>
        </React.StrictMode>,
        document.getElementById('root')
    );
    
    reportWebVitals();

#### Stap 16 - CounterContext.js
Door te zeggen dat `CounterContextProvider` een property `children` kan ontvangen, kunnen we zeggen dat we datzelfde `CounterContext` component ergens omheen willen wrappen. Waar we hem ook omheen zetten, dat moet bij de return `children` binnenkomen: dat zijn straks onze 3 elementen.

`CounterContext.Provider` is het echt component en `CounterContextProvider` is het jasje dat we erom hebben gewikkeld

In de CounterContextProvider doe je ook de error afhandeling en loading.

    import React, {createContext, useState} from 'react';
    
    export const CounterContext = createContext({});
    
    function CounterContextProvider({children}) {
        const [count, setCount] = useState(0)
    
        const data = {
            count: count,
            setCount: setCount,
        }
    
        return (
            <CounterContext.Provider value={data}>
                {children}
            </CounterContext.Provider>
        );
    }

    export default CounterContextProvider;

#### Stap 17 - CounterContext.js twee functies gemaakt die de waarde in de state aanpassen

De CounterContext provider houden we slim en alle andere componenten houden we dom door alle logica in de CounterContext te zetten.

We maken twee functies voor decrementCount en incrementCount aan.

We geven deze functies mee aan het dat object, zodat die buttons dat straks uit de context kunnen halen.

De gegevens staan nu in het data object en dat geven we mee aan `CounterContext.Provider`. Alle children die daarin zitten hebben daar toegang toe. Op dit moment zijn alle children `<App/>` die in index.js staat. En in dit App component zitten Result, DecrementButton en IncrementButton.

    import React, {createContext, useState} from 'react';
    
    export const CounterContext = createContext({});
    
    function CounterContextProvider({children}) {
    const [count, setCount] = useState(0);
    
        function decrementCount() {
            setCount(count - 1);
        }
    
        function incrementCount() {
            setCount(count + 1);
        }
    
        const data = {
            count: count,
            decrementCountFunction: decrementCount,
            incrementCountFunction: incrementCount,
        }
    
        return (
            <CounterContext.Provider value={data}>
                {children}
            </CounterContext.Provider>
        );
    }
    
    export default CounterContextProvider;

#### Stap 18 - Buttons geabonneerd op de context functies door useContext te gebruiken

Importeren van CounterContext en useContext functie.

Hetgeen dat we gaan destructuren uit de CounterContext is `decrementCountFunction` en `incrementCountFunction`.

Je kan de functies `decrementCountFunction` en `incrementCountFunction` nu gebruiken alsof we hem als property hebben ontvangen

Je zet een `onClick` op de buttons met de naam van de functie erin.

<i> DecrementButton.js</i>

    import React, {useContext} from 'react';
    import {CounterContext} from '../context/CounterContext';
    
    function DecrementButton() {
        const {decrementCountFunction} = useContext(CounterContext);
    
        return (
            <button type="button" onClick={decrementCountFunction}>
                Decrement
            </button>
        );
    }
    
    export default DecrementButton;

<i>IncrementButton.js</i>

    import React, {useContext} from 'react';
    import {CounterContext} from '../context/CounterContext';
    
    function IncrementButton() {
        const {incrementCountFunction} = useContext(CounterContext);
    
        return (
            <button type="button" onClick={incrementCountFunction}>
                Increment
            </button>
        );
    }
    
    export default IncrementButton;