## Conditioneel renderen en stijlen

Conditioneel renderen: componenten of elementen alléén weergeven wanneer er voldaan wordt aan een bepaalde conditie.

Wanneer we data of condities tussen onze JSX willen plaatsen, gebruiken we `{}` om dit te omwikkelen. In onderstaand voorbeeld hebben we een conditie gedefinieerd, gevolgd door een logica operator. Wanneer de conditie waar is, wordt het element na de `&&` automatisch weergegeven op de pagina.

    {
        messageValue.length > 20 && <p className="error-message">Dit bericht is te lang!</p>
    }

### Condition

Op basis van de waarde in een bepaalde conditie (in dit voorbeeld is hij `true`), willen wij wel of niet een `<p>`-element laten zien.

Als de condition waar is dan willen we een `<p>`-element met 'het klopt' zien en als het niet zo is : dan willen we een `<p>`-element met 'het klopt niet' zien.

    function App() {
        const condition = true
    
        return (
            <div>
                {condition ? <p>Het klopt</p> : <p>Het klopt niet</p>}
            </div>
        );
    }

Bovenstaand voorbeeld geeft: Het klopt

Met onderstaand voorbeeld is als de condition waar is dan krijgen we `<p>`-element `het klopt` te zien. Wanneer het niet waar is dan krijg je niets te zien.

    function App() {
        const condition = true
    
        return (
            <div>
                {condition && <p>Het klopt</p>}
            </div>
        );
    }