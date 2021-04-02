## Gebruiksvriendelijkheid voor de gebruiker: error
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
                    return <li key="name">{country.name}</li>
                })}
            </ul>
        );
    }
    
    export default App;