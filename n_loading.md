## Gebruikersfeedback: loading

We moeten rekening houden met gebruikers die geen goede wifi verbinding hebben of bijvoorbeeld met hun telefoon op een 3G netwerk zitten.

We maken een state aan met `useState()` en noemen de variabele `loading`.

    const [loading, toggleLoading] = useState("")

We maken toggleLoading true aan het begin en ongeacht of we in het try block of in het catch block terecht komen, willen we hoe dan ook ervoor zorgen dat toggleloading op false staat. Want op een gegeven moment is het laden klaar en of het nu gelukt is of niet, of we nu een error hebben gekregen of data, dat loaden is op een gegeven moment klaar.

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

De loading zetten we in return: als loading true is `{loading &&` dan laten we zien `{loading && <p>Data wordt geladen...</p>}`.

    return (
        <ul>
            {error && <p>{error}</p>}
            {loading && <p>Data wordt geladen...</p>}
            {countries && countries.map((country) => {
                return <li key="name">{country.name}</li>
            })}
        </ul>
    );

Deze melding krijgen alleen mensen te zien met langzame internet. Je kan dit testen in de console en aangeven dat je "slow 3G" hebt.

De volledige code is als volgt.

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
                    return <li key="name">{country.name}</li>
                })}
            </ul>
        );
    }
    
    export default App;