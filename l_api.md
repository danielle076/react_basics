## API
API = communicatie <br/>
Een vastgestelde set regels waarmee twee applicaties met elkaar kunnen communiceren.

API = asynchroon<br/>
Het kan even duren voor de data teruggestuurd wordt vanaf de server.

### Voorbeeld rest countries 
We gaan een lijst met alle landen in de wereld ophalen: https://restcountries.eu/rest/v2/all.

#### Stap 1 - App.js

    import React from 'react';
    import './App.css';
    
    function App() {
        return (
            <div>
                Hoi!
            </div>
        );
    }
    
    export default App;

#### Stap 2 - life cycles
We gaan een state aanmaken om de data in op te kunnen slaan. 

We beginnen met een lege array, want het is beter om hem vanaf het begin met hetzelfde type te initialiseren.

    import React, {useState} from 'react';
    import './App.css';
    
    function App() {
    const [countries, setCountries] = useState([]);
    
        return (
            <div>
                Hoi!
            </div>
        );
    }
    
    export default App;

#### Stap 3 - useEffect
We willen dat de landen die we ophalen uit zich zelf op het scherm komen, er hoeft niet eerst op een knop gedrukt te worden. Dus de life cycle die we hier gebruiken is mounting.

We laten de array leeg, omdat we de mounting cycle gebruiken. Alles wat we willen uitvoeren op het moment dat de pagina laad zet we tussen `{}`.

    import React, {useState, useEffect} from 'react';
    import './App.css';
    
    function App() {
    const [countries, setCountries] = useState([]);
    
        useEffect(() => {
    
        }, []);
    
        return (
            <div>
                Hoi!
            </div>
        );
    }
    
    export default App;

#### Stap 4 - asynchrone functie fetchData declareren 

    import React, {useState, useEffect} from 'react';
    import './App.css';
    
    function App() {
    const [countries, setCountries] = useState([]);
    
        useEffect(() => {
            async function fetchData() {
    
            }
        }, []);
    
        return (
            <div>
                Hoi!
            </div>
        );
    }
    
    export default App;

#### Stap 5 - fetchData aanroepen

    import React, {useState, useEffect} from 'react';
    import './App.css';
    
    function App() {
    const [countries, setCountries] = useState([]);
    
        useEffect(() => {
            async function fetchData() {
    
            }
    
            fetchData();
        }, []);
    
        return (
            <div>
                Hoi!
            </div>
        );
    }
    
    export default App;

#### Stap 6 - try en catch

    import React, {useState, useEffect} from 'react';
    import './App.css';
    
    function App() {
    const [countries, setCountries] = useState([]);
    
        useEffect(() => {
            async function fetchData() {
                try {
    
                } catch (error) {
                    console.log(error);
                }
            }
    
            fetchData();
        }, []);
    
        return (
            <div>
                Hoi!
            </div>
        );
    }
    
    export default App;

#### Stap 7 - asynchroon data ophalen + controleren wat de result is
Installeer axios: `npm install axios`

    import React, {useState, useEffect} from 'react';
    import axios from 'axios'
    import './App.css';
    
    function App() {
    const [countries, setCountries] = useState([]);
    
        useEffect(() => {
            async function fetchData() {
                try {
                    const result = await axios.get("https://restcountries.eu/rest/v2/all");
                    console.log(result);
                } catch (error) {
                    console.log(error);
                }
            }
    
            fetchData();
        }, []);
    
        return (
            <div>
                Hoi!
            </div>
        );
    }
    
    export default App;

#### Stap 8 - console bekijken
Wanneer je de console opent, zie je dat het een object is wat we binnen krijgen. In "data" zit de array met de 250 landen.

Data bekijken: `console.log(result.data);`.

    import React, {useState, useEffect} from 'react';
    import axios from 'axios'
    import './App.css';
    
    function App() {
    const [countries, setCountries] = useState([]);
    
        useEffect(() => {
            async function fetchData() {
                try {
                    const result = await axios.get("https://restcountries.eu/rest/v2/all");
                    console.log(result.data);
                } catch (error) {
                    console.log(error);
                }
            }
    
            fetchData();
        }, []);
    
        return (
            <div>
                Hoi!
            </div>
        );
    }
    
    export default App;

#### Stap 9 - setCountries(result.data);
Wat we loggen gaan we in de state zetten: `setCountries(result.data);`. We geven de nieuwe waarde van countries mee, dat was een lege array en dat is nu `response.data`, dus de array met 250 landen.

    import React, {useState, useEffect} from 'react';
    import axios from 'axios'
    import './App.css';
    
    function App() {
    const [countries, setCountries] = useState([]);
    
        useEffect(() => {
            async function fetchData() {
                try {
                    const result = await axios.get("https://restcountries.eu/rest/v2/all");
                    setCountries(result.data);
                } catch (error) {
                    console.log(error);
                }
            }
    
            fetchData();
        }, []);
    
        return (
            <div>
                Hoi!
            </div>
        );
    }
    
    export default App;

#### Stap 10 - data weergeven return
We willen de response data weergeven in de return. De 250 landen zit nu in de variabele state `countries` en hier gaan we overheen mappen.

We zetten de state `countries` in return, maken er een lijst van en in de anonieme functie zetten we country, want je roept 1 country op.

Vervolgens return je hem door `country.name` aan te roepen.

Vergeet de key property niet toe te voegen. Deze heeft een unieke naam.

    import React, {useState, useEffect} from 'react';
    import axios from 'axios'
    import './App.css';
    
    function App() {
    const [countries, setCountries] = useState([]);
    
        useEffect(() => {
            async function fetchData() {
                try {
                    const result = await axios.get("https://restcountries.eu/rest/v2/all");
                    setCountries(result.data);
                } catch (error) {
                    console.log(error);
                }
            }
    
            fetchData();
        }, []);
    
        return (
            <ul>
                {countries.map((country) => {
                    return <li key="name">{country.name}</li>
                })}
            </ul>
        );
    }
    
    export default App;

#### Stap 11 - data controleren
Zorg ervoor dat je contoleert of je data binnen krijgt: als we countries hebben (dus als hij waar is) `countries &&` dan gaan we eroverheen mappen `countries.map( (country) => { return <li key={name}>{country.name}</li>`

    import React, {useState, useEffect} from 'react';
    import axios from 'axios'
    import './App.css';
    
    function App() {
    const [countries, setCountries] = useState([]);
    
        useEffect(() => {
            async function fetchData() {
                try {
                    const result = await axios.get("https://restcountries.eu/rest/v2/all");
                    setCountries(result.data);
                } catch (error) {
                    console.log(error);
                }
            }
    
            fetchData();
        }, []);
    
        return (
            <ul>
                {countries && countries.map((country) => {
                    return <li key="name">{country.name}</li>
                })}
            </ul>
        );
    }
    
    export default App;

#### Stap 12 - environment variables
Wanneer je op verschillende plekken een `apiKey` declareert is dit inefficiënt maar ook onveilig. Je wilt namelijk nooit jouw eigen API key openbaar online hebben staan (op bijvoorbeeld GitHub of live op een webadres). Iedereen die de broncode inspecteert, zou dan namelijk jouw API key kunnen gebruiken. Dit probleem lossen we op met environment variables (omgevingsvariabelen).

Environment variables zijn variabelen die we declareren in een `.env` bestand. Omdat we dit bestand nooit mee pushen naar GitHub (en dus altijd toevoegen aan de `.gitignore`) blijven onze tokens geheim.

- Maak in dezelfde hoogte als de `.gitignore` en `package.json` een `.env` én een `.env.dist` file aan.
- Voeg de `.env` toe aan de `.gitignore`.
- Open de `.env.dist` en zet daar `REACT_APP_API_KEY=`. De waarde laten we hier leeg. Het is conventie om environment variables in hoofdletters te schrijven. Bovendien moeten de namen altijd met REACT_APP beginnen, omdat het framework van Create React App ze anders niet kan vinden.
- Kopieer de naam van deze variabele en plak hem in `.env`. Plak de waarde van de API key er direct achter.
- Run het commando `npm build` in de terminal. Dit doe je omdat de browser geen boodschap aan al die React code heeft. Door middel van Webpack worden al onze losse JavaScript, HTML en CSS bestanden samengevoegd tot één grote statische bundel code. Dit noemen we de build. Environment variables zijn geen onderdeel van het project, maar worden pas uitgelezen tijdens de build. Als wij tijdens runtime (wanneer je aan het developen bent) environment variabelen wil uitlezen, gaat dit niet werken. <b>Iedere keer wanneer je iets aanpast in het .env bestand, zul je opnieuw moeten builden.</b>
- We kunnen de variabele gebruiken. Open `App.js` en gebruik de apiKey door `process.env.REACT_APP_API_KEY` in te vullen.

Bijvoorbeeld:

    try {
     const result = await axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${location},nl&appid=${process.env.REACT_APP_API_KEY}&lang=nl`);
     setWeatherData(result.data);
    } catch (e) {
     console.error(e);
     setError(true);
    }