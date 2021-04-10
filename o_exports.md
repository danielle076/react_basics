## Exports
Exports doen we met volledige componenten en pagina's.

### Default export

Aan het einde van je Component HomePage zie je `export default HomePage;` staan en deze kun je gebruiken in je App.js met import.

Het maakt niet uit hoe je de import noemt, met die naam kun je in App.js de import gebruiken.

Default exports importeren we altijd zonder snorretjes `{}`.

<i>HomePage.js</i>

    const HomePage = () => {
        //.. code
    }

    export default HomePage;

<i>App.js</i>

    import HomePage from './HomePage.js'
    
    import Bananen from './HomePage.js'


### Named export

Het verschil met default export is dat je alleen het woord export ziet staan, zonder het woord default.

Wanneer je alleen `export` ziet staan, dan moet je het met snorretjes `{}` importeren.

Je mag het geen andere naam geven zoals bijvoorbeeld 'Bananen', maar je kan het wel hernoemen.

<i>HomePage.js</i>

    export const HomePage = () => {
        //.. code
    }

<i>App.js</i>

    import {HomePage} from './HomePage.js'
    
    import {Bananen} from './HomePage.js' // dit werkt niet
    
    import {HomePage as Bananen} from './HomePage.js' // hernoemen kan wel


### Named & default export 

`useState` en `useEffect` moeten binnen `{}` en React staat los.

<i>React</i>

    export const useState(() => {
        // ..
    });
    
    export const useEffect(() => {
        // ..
    });
    
    export default React;

<i>App.js</i>

    import React, {useState, useEffect} from 'react';

### Conclusie
- <b>export default:</b> zonder {} importeren, want je hebt altijd maar 1 export default.
- <b>export:</b> met {} importeren, want je kan meerdere exports in een bestand hebben staan.