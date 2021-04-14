## React lifecycles
- Initialisation: het component wordt klaargezet (state wordt gemaakt en gevuld)
- Mounting: pagina/component wordt voor de eerste keer geladen (in de DOM geplaatst)
- Updating: op basis van nieuwe data wordt het component opnieuw "gerenderd"
- Unmounting: het component wordt uit de DOM verwijderd (gebruiker gaat naar een andere pagina)

Dit is belangrijk om te weten, omdat je dingen op een bepaald moment wilt uitvoeren.

Voor elke lifecycle is er eigenlijk een aparte functie. Voorheen hadden we Class en deze components zaten wat moeilijker in elkaar, met hooks is alles versimpelt.
- Initialisation: `useState()`
- Mounting: `useEffect()`
- Updating: `useEffect()`
- Unmounting: `useEffect()`

We gebruiken overal dezelfde functie maar door middel van wat we de useEffect meegeven geven we aan in welke lifecycle hij zit.

### Voorbeeld lifecycle mounting en updating

#### Stap 1 - App.js

    import React from 'react';
    import './App.css';
    
    function App(){
        return(
            <div>
                Hello!
            </div>
        );
    }
    
    export default App;    

#### Stap 2 - App.js
State aangemaakt die count bijhouden.

    import React, {useState} from 'react';
    import './App.css';
    
    function App(){
    const [count, setCount] = useState(0);
    
        return(
            <div>
                Hello!
            </div>
        );
    }
    
    // export default App;

#### Stap 3 - Buttons.js
Een component met buttons + en - aangemaakt.

    import React from 'react';
    
    function Buttons(){
        return (
            <>
                <button type="button">
                    -
                </button>
                <button type="button">
                    +
                </button>
            </>
        );
    }
    
    export default Buttons;

#### Stap 4 - Count.js
Een component die count laat zien.

    import React from 'react';
    
    function Count(){
        return(
            <h1>Aantal kliks:</h1>
        );
    }
    
    export default Count;

#### Stap 5 - App.js
Importeren van Buttons.js en Count.js + components gebruiken in return.

    import React, {useState} from 'react';
    import Buttons from './components/Buttons'
    import Count from './components/Count'
    import './App.css';
    
    function App(){
    const [count, setCount] = useState(0);
    
        return(
            <>
                <Count/>
                <Buttons/>
            </>
        );
    }
    
    // export default App;

#### Stap 6 - App.js
We willen dat het aantal kliks in Count.js wordt weergegeven met `count` en dat Button.js `count` en `setCount` meekrijgt, zodat we die kunnen aanpassen.

    import React, {useState} from 'react';
    import Buttons from './components/Buttons'
    import Count from './components/Count'
    import './App.css';
    
    function App(){
    const [count, setCount] = useState(0);
    
        return(
            <>
                <Count count={count}/>
                <Buttons count={count} setCount={setCount()}/>
            </>
        );
    }
    
    // export default App;

#### Stap 7 - Count.js
Je ontvangt de count in de props en die geef je weer in de return. <br/>

    import React from 'react';
    
    function Count( {count}){
        return(
            <h1>Aantal kliks: {count}</h1>
        );
    }
    
    export default Count;

#### Stap 8 - Buttons.js
Je ontvangt de `count` (huidige waarde) en `setCount` in de props, die zet je in de `onClick` van de button.

    import React from 'react';

    function Buttons({count, setCount}){
        return (
            <>
                <button type="button" onClick={() => setCount(count - 1)}>
                    -
                </button>
                <button type="button" onClick={() => setCount(count + 1)}>
                    +
                </button>
            </>
        );
    }
    
    export default Buttons;

#### Stap 9 - Buttons.js + Count.js
We gaan zowel in het Buttons component als het Count component een console plaatsen. <br/>
Stel je zou data aanroepen en je wilt dit hebben wanneer het Component geladen is, dan kun je dit op deze manier doen. Echter wanneer je op de button klikt gaat de pagina zich refreshen waardoor de data van beide Componenten elke keer opnieuw opgeroepen: Count wordt opnieuw gerenderd omdat de waarde omhoog gaat met 1 en Buttons wordt opnieuw gerenderd omdat hij ook count gebruikt.

    import React from 'react';
    
    function Buttons({count, setCount}){
        console.log("BUTTONS: Ik ben buiten de useEffect aangeroepen")
    
        return (
            <>
                <button type="button" onClick={() => setCount(count - 1)}>
                    -
                </button>
                <button type="button" onClick={() => setCount(count + 1)}>
                    +
                </button>
            </>
        );
    }

&
    
    import React from 'react';

    function Count( {count}){
        console.log("COUNT: Ik ben buiten de useEffect aangeroepen")
    
        return(
            <h1>Aantal kliks: {count}</h1>
        );
    }
    
    export default Count;

#### Stap 10 - Buttons.js + Count.js
We willen dat de data zich alleen laat zien wanneer hij de eerste keer in de DOM wordt geplaatst. 

De oplossing: `useEffect()`. Importeer useEffect in React. useEffect heeft altijd 2 parameters: een anonieme/lege functie en een lege dependency array. Dus als volgt: `useEffect(() => {}, []);`. Wanneer je de dependency array vergeet kun je een oneindige loop krijgen. Met het meegeven van de lege dependency array zeggen we: ik wil dat je wordt afgevuurd op het moment dat ons component voor de allereerste keer gemount is.<br/>

Wanneer je nu op de +/- knoppen drukt zal "binnen useEffect" maar 1 keer worden afgevuurd. Dus mounting useEffect: haalt de data alleen op als het component voor de eerste keer wordt gebruikt, daarna niet meer. 

    import React, {useEffect} from 'react';
    
    function Buttons({count, setCount}){
        console.log("BUTTONS: Ik ben buiten de useEffect aangeroepen")
    
        useEffect(() => {
            console.log("⚠ BUTTONS: Ik ben binnen de useEffect aangeroepen")
        }, []);
    
        return (
            <>
                <button type="button" onClick={() => setCount(count - 1)}>
                    -
                </button>
                <button type="button" onClick={() => setCount(count + 1)}>
                    +
                </button>
            </>
        );
    }
    
    import React, {useEffect} from 'react';

&

    function Count( {count}){
        console.log("COUNT: Ik ben buiten de useEffect aangeroepen")
    
        useEffect(() => {
            console.log("⚠ COUNT: Ik ben binnen de useEffect aangeroepen")
        }, []);
    
        return(
            <h1>Aantal kliks: {count}</h1>
        );
    }
    
    export default Count;

#### Stap 11 - Count.js
We gaan useEffect updaten. Stel count is hoger dan 4, dan willen we dat useEffect wordt geupdate. 

Je weet dat het hier gaat om een update omdat je in de lege dependency array `count` hebt gezet. Je hoeft overigens geen voorwaarde erin te zetten om useEffect te updaten.

    import React, {useEffect} from 'react';
    
    function Count( {count}){
        console.log("COUNT: Ik ben buiten de useEffect aangeroepen")
    
        useEffect(() => {
            console.log("⚠ COUNT: Ik ben binnen de useEffect aangeroepen")
        }, []);
    
        useEffect(() => {
            if (count > 4 ) {
                console.log("⚠ COUNT: Ik ben binnen de useEffect geupdate")
            }
        }, [count])
    
        return(
            <h1>Aantal kliks: {count}</h1>
        );
    }
    
    export default Count;