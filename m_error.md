## Gebruikersfeedback: error
We moeten ervoor zorgen dat we in iedere situatie feedback geven over wat er gebeurt, of wat er dus juist niét gebeurt.

Wanneer er door de gebruiker iets gedaan wordt dat niet juist is zal de API een errorcode teruggeven, dit wordt opgevangen in het catch-blok.

    async function fetchData() {
    
        try {
            const result = await axios.get("https://restcountries.eu/rest/v2/all");
            setCountries(result.data);
        } catch (error) {
            console.log(error);
        }
    }        

We zien dat wanneer er iets fout gaat dit alleen in de console wordt weergegeven. We willen dit ook op de website weergeven.

We maken een state aan met `useState()` en noemen de variabele `error`.

In het geval dat we in het catch blok terecht komen `catch (error)`, roepen we de setError aan. Je kan zeggen `setError("error.message")` maar dit is vaak te cryptisch, dus je kan ook zeggen: `setError("Er is iets misgegaan bij het ophalen van de data.")`

    function App() {
    const [countries, setCountries] = useState([]);
    const [error, setError] = useState("");
    
        async function fetchData() {
        
            try {
                const result = await axios.get("https://restcountries.eu/rest/v2/all");
                setCountries(result.data);
            } catch (error) {
                setError("Er is iets misgegaan bij het ophalen van de data.")
                console.log(error);
            }
        }      

Wanneer je een error bericht heb gekregen en de website werkt toch, dan blijft het error bericht staan, omdat de error achter de schermen nog op true staat. Om ervoor te zorgen dat we met het opnieuw aanvragen van de fetchData of useEffect beginnen met een schone lei, zetten we de setError terug op 0: `setError("");`.

    function App() {
    const [countries, setCountries] = useState([]);
    const [error, setError] = useState("");
    
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


De error message zetten we in return: als we een error hebben `{error && ` dan willen we die laten zien `{error && <p>{error}</p>}`.

    return (
        <ul>
            {error && <p>{error}</p>}
        </ul>
    );

Wanneer je de error wilt testen, kun je dit doen door een spelfout te maken in de URL.

De volledige code is als volgt.

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
                    return <li key="name">{country.name}</li>
                })}
            </ul>
        );
    }
    
    export default App;