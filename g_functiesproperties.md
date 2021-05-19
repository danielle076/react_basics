## Functies doorgeven als properties

Wanneer je een component aanmaakt in React kun je daar properties aan meegeven.

We maken een `logConsole` functie en een button aan. Wanneer je op de button klikt, geeft de console "hey there banaan".

    import React from 'react'
    import './App.css';
    
    function App() {
        function logConsole() {
            console.log("Hey there banaan")
        }
    
        return (
            <button type="button" onClick={logConsole}>
                Log me!
            </button>
        );
    }
    
    export default App;

Vervolgens maken we een map "components" aan en een file "Loggen.js" met de volgende gegevens.

    import React from 'react';

    function Loggen(){
        return (
            <button type="button">
                Log me!
            </button>
        );
    }

    export default Loggen;

In App.js importeer je Loggen.

    import Loggen from './components/Loggen'

Stel we willen de button text "Log me!" meegeven aan ons Loggen component. De volgende code zet je in App.js.

    return (
            <Loggen buttonText="Log mij" />
    );

Wanneer "Loggen.js" deze `buttonText` wilt ontvangen, moet je hem destructureren met bijvoorbeeld `buttonText`.

    import React from 'react';

    function Loggen({ buttonText }){
        return (
            <button type="button">
                {buttonText}
            </button>
        );
    }

    export default Loggen;

We kunnen waardes doorgeven zoals hierboven, maar we kunnen ook functies doorgeven, zoals functie `logConsole` die we "banaan" noemen.

    return (
            <Loggen
                buttonText="Log mij"
                banaan={logConsole}
            />
    );

Nu moeten we hem alleen nog in "Loggen.js" zetten en gebruiken met een `onClick` (wanneer je de pagina refresht komt de melding in de console).

    import React from 'react';

    function Loggen({ buttonText, banaan }){
        return (
            <button type="button" onClick={banaan}>
                {buttonText}
            </button>
        );
    }

    export default Loggen;