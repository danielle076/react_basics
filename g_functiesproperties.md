## Functies doorgeven als properties

Wanneer je een component aanmaakt in React kun je daar properties aan meegeven.

We maken een nieuwe functie.

    function App() {
        function logConsole() {
            console.log("Hey there banaan")
        }

We maken een map "components" aan en een file "Loggen.js"

    import React from 'react';

    function Loggen(){
        return (
            <button type="button">
                Log me!
            </button>
        );
    }

    export default Loggen;

Stel we willen de button text "Log me!" meegeven aan ons Loggen component.

    return (
            <Loggen buttonText="Log mij" />
    );

Wanneer "Loggen.js" deze `buttonText` wilt ontvangen, moet je hem destructureren met `buttonText`.

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
                banaan={logConsole()}
            />
    );

In "Loggen.js" moeten we hem nog zetten en gebruiken een `onClick` (wanneer je pagina refresht komt de melding in de console).

    import React from 'react';

    function Loggen({ buttonText, banaan }){
        return (
            <button type="button" onClick={banaan}>
                {buttonText}
            </button>
        );
    }

    export default Loggen;