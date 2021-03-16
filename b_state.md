## State

React werkt de UI bij op basis van de toestand van de toepassing. Deze toestand wordt eigenlijk opgeslagen als een eigenschap van een functiecomponent:

    // visualisatie van de state
    state = {
        value: 0
    }

Stel we hebben een teller en 3 knoppen die verhogen, verlagen of resetten. De waarde van de teller wordt weergegeven op de pagina via JSX.

De weergegeven tellerwaarde is gebaseerd op de status en we veranderen de status door op een van de knoppen te klikken. Vanilla JS behandelt een klik op een knop als een gebeurtenis en dat doet React ook. Wanneer zo'n gebeurtenis plaatsvindt, roepen we functies aan die de teller verhogen of verlagen op basis van de knop waarop is geklikt. Deze functies bevatten de code die de toestand van de component verandert.

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

We hebben de state bijgewerkt door setState aan te roepen in elk van de functies die een klik op een knop afhandelen. De teller die op de pagina wordt weergegeven, wordt in real time bijgewerkt. Zo krijgt React zijn naam omdat het reageert op state veranderingen.

Kortom, React controleert automatisch elke componentstatus op wijzigingen en werkt het DOM op de juiste manier bij.