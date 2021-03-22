## Eventhandlers externaliseren
 
Het zal voorkomen dat je op basis van een event niet één, maar meerdere acties wil uitvoeren. Om dat allemaal in één `onClick` handler te stoppen wordt onoverzichtelijk. We verplaatsen onze code in dat geval naar een aparte functie die wordt aangeroepen als het event wordt afgevuurd.

Stel we maken een button en als je erop klikt dan wordt de counter opgehoogd. Je maakt de button met een `onClick` en die geef je een anonieme functie mee, want anders vuurt hij hem gelijk af hij wacht niet op het event.

Om hem op te hogen moet je de huidige waarde van counter nemen en deze met 1 ophogen.

    function App() {
        const [counter, setCounter] = useState(0);
    
        return (
            <button type="button" onClick={() => setCounter(counter + 1)}>
                Plus 1
            </button>
        );

We willen ook een bericht in de console loggen wanneer we op de button klikken. We gaan de functie externaliseren, dus we verplaatsen het naar een aparte functie, die we `handleClick()` noemen en daar onze `console.log()` aan toevoegen.

Zoals je ziet, wordt op het klik event nu alle code in de handleClick-functie uitgevoerd. We geven alleen de naam van de functie mee en hebben nu geen anonieme functie nodig, omdat onze functie geen parameters verwacht. Aan de handleClick-functie kun je nu zoveel acties aan toevoegen als je wil, terwijl je code netjes en overzichtelijk blijft.

    import React, {useState} from 'react'
    import './App.css';

    function App() {
        const [counter, setCounter] = useState(0);

        function handelClick() {
            setCounter(counter + 1);
            console.log(counter + 1);
        }

        return (
            <button
                type="button"
                onClick={handelClick}>
                Plus 1
            </button>
        );
    }

    // export default App;