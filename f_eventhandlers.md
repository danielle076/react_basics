## Eventhandlers externaliseren
 
Het kan voorkomen dat je op basis van een event niet één, maar meerdere acties wil uitvoeren. Dit allemaal in één `onClick` handler stoppen is onoverzichtelijk. We verplaatsen de code in dat geval naar een aparte functie, die wordt aangeroepen als het event wordt afgevuurd.

Stel we maken een button en als je erop klikt dan wordt de counter opgehoogd. Je maakt de button met een `onClick` en die geef je een anonieme functie mee, want anders vuurt hij hem gelijk af (hij wacht niet op het event).

Om hem op te hogen moet je de huidige waarde van `counter` nemen en deze met 1 ophogen.

    function App() {
        const [counter, setCounter] = useState(0);
    
        return (
            <button type="button" onClick={() => setCounter(counter + 1)}>
                Plus 1
            </button>
        );

We willen ook een bericht in de console loggen wanneer we op de button klikken. We gaan dus de functie externaliseren (verplaatsen naar een aparte functie), die we `handleClick()` noemen en daar de `console.log()` aan toevoegen.

Zoals je in het voorbeeld hieronder ziet, wordt op het klik event alle code in de `handleClick` functie uitgevoerd. We geven alleen de naam van de functie mee en hebben geen anonieme functie nodig, omdat onze functie geen parameters verwacht. Aan de `handleClick` functie kun je zoveel acties aan toevoegen als je wil, terwijl je code netjes en overzichtelijk blijft.

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

    export default App;