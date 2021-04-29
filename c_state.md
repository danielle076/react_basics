## State

React components heeft een ingebouwd state object. Het state object is waar je de waarden van eigenschappen die bij de component horen opslaat. Wanneer het state object verandert, wordt de component opnieuw gerenderd.

Het ingebouwde state object van React heet `.useState();` en kun je als volgt gebruiken.

    function App() {
        React.useState();
    }

Om niet elke keer `.useState` uit te typen kun je hem importeren.

    import React, {useState} from 'react'

Wanneer we state maken, bijvoorbeeld wanneer we een counter bijhouden die `counter` heet, slaan we de waarde op in `setCounter` (dit mag ook `toggleCounter` heten). Aan `useState` geven we de initiale waarde mee. In het voorbeeld staat de counter op 0 (nul).

    function App() {
        const [counter, setCounter] = useState(0);
    }

Wanneer je de counter wilt gaan gebruiken kun je deze bijvoorbeeld in een `<div>` zetten.

    return (
        <div>
            {counter}
        </div>
    );

De `setCounter` kunnen we overal aanroepen, bijvoorbeeld met een button klik.

Stel we hebben een teller met 3 knoppen die verhogen, verlagen of resetten. De waarde van de teller wordt weergegeven op de pagina via JSX.

De weergegeven tellerwaarde is gebaseerd op de status en we veranderen de status door op één van de knoppen te klikken. Vanilla JS behandelt een klik op een knop als een gebeurtenis en dat doet React ook. Wanneer zo'n gebeurtenis plaatsvindt, roepen we functies aan die de teller verhogen of verlagen op basis van de knop waarop is geklikt. Deze functies bevatten de code die de toestand van de component verandert.

Hier is een voorbeeld van zo'n teller:

    import React, { useState } from 'react';

    function App() {
        const [count, setCount] = useState(0);
    
        const addCount = () => {
            setCount(count + 1);
            console.log("Increment count");
        }
    
        const subtractCount = () => {
            setCount(count - 1);
            console.log("Decrement count");
        }
    
        const resetCount = () => {
            setCount(0);
            console.log("Reset count");
        }
    
        return (
            <>
                <h1>{count}</h1>
                <div>
                    <button onClick={addCount}>+</button> <span>&nbsp;</span>
                    <button onClick={subtractCount}>-</button> <span>&nbsp;</span>
                    <button onClick={resetCount}>reset</button>
                </div>
            </>
        );
    }

    export default App;

We hebben de `state` bijgewerkt door `setState` aan te roepen in elk van de functies die een klik op een knop afhandelen. De teller die op de pagina wordt weergegeven, wordt real time bijgewerkt.