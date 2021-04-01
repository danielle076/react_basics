## API
API = communicatie; <br/>
Een vastgestelde set regels waarmee twee applicaties met elkaar kunnen communiceren

API = Asynchroon;<br/>
Het kan wel even duren voor de data teruggestuurd wordt vanaf de server

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
State aanmaken om de data in op te kunnen slaan. 

We beginnen met een lege array, omdat als we hem leeg zouden houden dan gaat hij van type undefined naar op het moment dat hij gevuld is wordt hij een array en dat is niet zo netjes. Het is beter om hem vanaf het begin met hetzelfde type te initialiseren.

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

We laten de array leeg omdat we de mounting cycle gebruiken. Alles wat we willen uitvoeren op het moment dat de pagina laad zet we tussen {}.

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
Installeer axios: npm install axios --save

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
Wat we loggen gaan we in de state zetten: `setCountries(result.data);`. We geven de nieuwe waarde van counries mee, dat was een lege array en dat is nu "response.data", dus de array met 250 landen.

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
We willen de response data weergeven in de return. De 250 landen zit nu in de variabele state "countries" en hier gaan we overheen mappen.

We zetten de state "countries" in return, maken er een lijst van en in de anonieme functie zetten we country, want je roept 1 country op.

Vervolgen return je hem door country.name aan te roepen, want name is wat in het object staat dat dit de naam van het land is.

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
                    return <li key={name}>{country.name}</li>
                })}
            </ul>
        );
    }
    
    export default App;

#### Stap 11 - data controleren
Zorg ervoor dat je contoleert of je data wel binnen krijgt: als we countries hebben (dus als hij waar is) `countries &&` dan gaan we eroverheen mappen `countries.map( (country) => { return <li key={name}>{country.name}</li>`

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
                    return <li key={name}>{country.name}</li>
                })}
            </ul>
        );
    }
    
    export default App;

#### Stap 12 - gebruiksvriendelijkheid voor de gebruiker: error
We maken een state voor error.

In het geval dat we in het catch blok terecht komen `catch (error)`, roepen we de setError aan. Je kan zeggen `setError("error.message")` maar dit is vaak te cryptisch, dus je kan ook zeggen: `setError("Er is iets misgegaan bij het ophalen van de data.")`

De error message zetten we in return: als we een error hebben `{error && ` dan willen we die laten zien `{error && <p>{error}</p>}`.

Wanneer je een error bericht heb gekregen en de website werkt toch, dan blijft het error bericht staan, omdat de error achter de schermen nog op true staat. Om ervoor te zorgen dat we met het opnieuw aanvragen van de fetchData of useEffect beginnen met een schone lei, zetten we de setError terug op 0: `setError("");`.

Test de error: maak een spelfout in de URL.

    import React, {useState, useEffect} from 'react';
    import axios from 'axios'
    import './App.css';
    
    function App() {
    const [countries, setCountries] = useState([]);
    const [error, setError] = useState("");
    
        useEffect(() => {
            async function fetchData() {
                setError("");
    
                try {
                    const result = await axios.get("https://restcountries.eu/rest/v2/all");
                    setCountries(result.data);
                } catch (error) {
                    setError("Er is iets misgegaan bij het ophalen van de data.")
                    console.log(error);
                }
            }
    
            fetchData();
        }, []);
    
        return (
            <ul>
                {error && <p>{error}</p>}
                {countries && countries.map((country) => {
                    return <li key={name}>{country.name}</li>
                })}
            </ul>
        );
    }
    
    export default App;

#### Stap 12 - gebruiksvriendelijkheid voor de gebruiker: loading
We maken een state voor loading.

We maken toggleLoading true aan het begin en ongeacht of we in het try block of in het catch block terecht komen, willen we hoe dan ook ervoor zorgen dat toggleloading op false staat. Want op een gegeven moment is het laden klaar en of het nu gelukt is of niet, of we nu een error hebben gekregen of data, dat loaden is op een gegeven moment klaar.

De loading zetten we in return: als loading true is `{loading &&` dan laten we zien `{loading && <p>Data wordt geladen...</p>}`.

Deze melding krijgen alleen mensen te zien met langzame internet. Je kan dit testen in de console en aangeven dat je "slow 3G" hebt.

    import React, {useState, useEffect} from 'react';
    import axios from 'axios'
    import './App.css';
    
    function App() {
    const [countries, setCountries] = useState([]);
    const [error, setError] = useState("");
    const [loading, toggleLoading] = useState("")
    
        useEffect(() => {
            async function fetchData() {
                setError("");
                toggleLoading("true")
    
                try {
                    const result = await axios.get("https://restcountries.eu/rest/v2/all");
                    setCountries(result.data);
                } catch (error) {
                    setError("Er is iets misgegaan bij het ophalen van de data.")
                    console.log(error);
                }
                toggleLoading(false);
            }
    
            fetchData();
        }, []);
    
        return (
            <ul>
                {error && <p>{error}</p>}
                {loading && <p>Data wordt geladen...</p>}
                {countries && countries.map((country) => {
                    return <li key={name}>{country.name}</li>
                })}
            </ul>
        );
    }
    
    export default App;