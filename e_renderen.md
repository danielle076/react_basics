## Conditioneel renderen en stijlen

    function App() {
        const condition = true
    
        return (
            <div>
                {condition ? <p>Het klopt</p> : <p>Het klopt niet</p>}
            </div>
        );
    }

Op basis van de waarde in een bepaalde conditie (hier is hij true), willen wij wel of niet een `<p>`-element laten zien.

Als de condition waar is dan willen we een `<p>`-element met het klopt en als het niet zo is : dan wil ik een `<p>`-element met het klopt niet.

    function App() {
        const condition = true
    
        return (
            <div>
                {condition && <p>Het klopt</p>}
            </div>
        );
    }

Als de condition waar is dan willen we `<p>`-element het klopt zien.

Conditioneel renderen: componenten of elementen alléén weergeven wanneer er voldaan wordt aan een bepaalde conditie.

    {
        messageValue.length > 20 && <p className="error-message">Dit bericht is te lang!</p>
    }

Wanneer we data of condities tussen onze JSX willen plaatsen, gebruiken we {} om dit te omwikkelen. In bovenstaand voorbeeld hebben we een conditie gedefiniëerd, gevolgd door een logica operator. Wanneer de conditie true is, wordt het element na de && automatisch weergegeven op de pagina.