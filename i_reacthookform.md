## React hook form

Naast controlled components hebben we React hook form. Deze is gemaakt voor grote formulieren. Om hook form uit te leggen gaan we eerst een basis formulier maken en daarna React hook form toepassen.

De voornaamste reden waarom men liever React hook form gebruikt in plaats van controlled components bij grote formulieren is omdat het minder schrijfwerk is.

### Basis formulier
We gaan een plain standaard html formulier maken waarbij we het weer kunnen bestellen.

    import React from 'react'
    import './App.css';
    
    function App() {
        return (
          <>
            <h1>Weer bestellen</h1>
            <form onSubmit={}>
              <button type="submit">
                Verzenden
              </button>
            </form>
          </>
        );
    }
    
    export default App;

We maken een functie die wordt aangeroepen op het moment dat we het formulier willen verzenden.

    function onSubmitButton() {
        console.log("Jij wilt versturen")
    }

De `onSubmit()` is een eventHandler, dus als we daar direct een `console.log` in hadden gezet hadden we de anonieme functie moeten gebruiken. Maar we hebben een externe functie "onSubmitButton" gemaakt dus kunnen we die gebruiken.

    import React from 'react'
    import './App.css';
    
    function App() {
    
        function onSubmitButton() {
            console.log("Jij wilt versturen")
        }
    
        return (
            <>
                <h1>Weer bestellen</h1>
                <form onSubmit={onSubmitButton}>
                    <button type="submit">
                        Verzenden
                    </button>
                </form>
            </>
        );
    }
    
    export default App;

Wanneer je de `console.log` bekijkt zie je dat het bericht erin staat, maar ook weer gelijk verdwijnt. Hij ververst de pagina en dat komt doordat we bij `type` submit hebben staan. Om ervoor te zorgen dat dit niet gebeurd kun je aan de functie "onSubmitButton" een event object (e of event) meegeven. Op dat event object staat een functie en die noemen we `preventDefault()`. Met deze functie gaan we de default behavior van het formulier preventen zodat de pagina niet ververst.

    function onSubmitButton(e) {
        e.preventDefault();
        console.log("Jij wilt versturen")
    }
 
We geven het formulier een input met naam en woonplaats. De volgende acties geef je mee.
- type
- name: is verplicht, want hieronder worden de waardes opgeslagen
- placeholder
- id: deze is uniek

Dat ziet er als volgt uit.

    return (
        <>
          <h1>Weer bestellen</h1>
          <form onSubmit={onSubmitButton}>
            <input
              type="text"
              name="fullName"
              placeholder="Naam en achternaam"
              id="name"
          />
            <input
              type="text"
              name="plaatsnaam"
              placeholder="Plaatsnaam"
              id="plaatsnaam"
          />
          <button type="submit">
            Verzenden
          </button>
          </form>
        </>
    );

Het type weer wat we gaan bestellen zetten we in radio buttons.
- htmlFor: deze wordt altijd gekoppeld aan de id, zo begrijpen ze dat ze bijelkaar horen
- type
- name: moeten allemaal hetzelfde zijn
- value
- id: deze is uniek

Dat komt er als volgt uit te zien.

    return (
        <>
          <p>Ik wil graag:</p>
          <label htmlFor="field-rain">
            <input
              type="radio"
              name="weather"
              value="rain"
              id="field-rain"
            />
            Regen
          </label>
          <label htmlFor="field-wind">
            <input
              type="radio"
              name="weather"
              value="wind"
              id="field-wind"
            />
            Lekker veel wind
          </label>
          <label htmlFor="field-sun">
            <input
              type="radio"
              name="weather"
              value="sun"
              id="field-sun"
            />
            Zonnig
          </label>
        </>
    );

Nu komen alle fields naast elkaar te staan, met CSS kun je dit aanpassen: `display: block`.

    label
    {
        display: block;
    }

Ons basis formulier ziet er als volgt uit.

    import React from 'react'
    import './App.css';
    
    function App() {
        function onSubmitButton(e) {
            e.preventDefault();
            console.log("Jij wilt versturen")
    }

    return (
        <>
            <h1>Weer bestellen</h1>
            <form onSubmit={onSubmitButton}>
                <input
                    type="text"
                    name="fullName"
                    placeholder="Naam en achternaam"
                    id="name"
                />
                <input
                    type="text"
                    name="plaatsnaam"
                    placeholder="Plaatsnaam"
                    id="plaatsnaam"
                />
                <p>Ik wil graag:</p>
                <label htmlFor="field-rain">
                    <input
                        type="radio"
                        name="weather"
                        value="rain"
                        id="field-rain"
                    />
                    Regen
                </label>
                <label htmlFor="field-wind">
                    <input
                        type="radio"
                        name="weather"
                        value="wind"
                        id="field-wind"
                    />
                    Lekker veel wind
                </label>
                <label htmlFor="field-sun">
                    <input
                        type="radio"
                        name="weather"
                        value="sun"
                        id="field-sun"
                    />
                    Zonnig
                </label>
                <button type="submit">
                    Verzenden
                </button>
            </form>
        </>
    );}

    export default App;

### Hook form formulier
Installeer React hook form: `npm install react-hook-form`

Implementeer React hook form.

    import {useForm} from "react-hook-form";

We gaan React hook form initialiseren.

    function App() {
        const {} = useForm();
    }

Op de website van React hook form staat wat je kunt doen met deze library: https://react-hook-form.com/.

Je kunt bijvoorbeeld de volgende dingen doen: const `{ register, handleSubmit, watch, errors } = useForm();`
- `handleSubmit` zal de invoer valideren voordat "onSubmit" wordt aangeroepen
- registreer je invoer in de hook door de `register` functie aan te roepen

`e.preventDefault();` hoeven we niet meer te doen, want dat doet React hook form voor ons.

    function App() {
        const {register, handleSubmit} = useForm();

        function onSubmitButton() {
            console.log("Jij wilt versturen")
        }

        return (
            <form onSubmit={handleSubmit(onSubmitButton)}>
            </form>
        );
    }

Je kunt velden registreren door op de invoervelden `{...register('value')}` te zetten.

    return (
        <>
            <h1>Weer bestellen</h1>
            <form onSubmit={handleSubmit(onSubmitButton)}>
                <input
                    {...register("fullName")}
                    type="text"
                    name="fullName"
                    placeholder="Naam en achternaam"
                    id="name"
                />
                <input
                    {...register("plaatsnaam")}
                    type="text"
                    name="plaatsnaam"
                    placeholder="Plaatsnaam"
                    id="plaatsnaam"
                />
                <p>Ik wil graag:</p>
                <label htmlFor="field-rain">
                    <input
                        {...register("field-rain")}
                        type="radio"
                        name="weather"
                        value="rain"
                        id="field-rain"
                    />
                    Regen
                </label>
                <label htmlFor="field-wind">
                    <input
                        {...register("field-wind")}
                        type="radio"
                        name="weather"
                        value="wind"
                        id="field-wind"
                    />
                    Lekker veel wind
                </label>
                <label htmlFor="field-sun">
                    <input
                        {...register("field-sun")}
                        type="radio"
                        name="weather"
                        value="sun"
                        id="field-sun"
                    />
                    Zonnig
                </label>
                <button type="submit">
                    Verzenden
                </button>
            </form>
        </>
    );

Wanneer we op de submit knop drukken krijgen we het data object mee in de `console.log`.

    function onSubmitButton(data) {
        console.log(data)
    }

> <span style="color:red">Let op: radio log hij niet in de console, aan het uitzoeken!</span>.

We gaan validatie toevoegen. De ondersteunde validatieregels zijn:
- required (velden zijn verplicht)
- min (minimale hoogte cijfers)
- max (maximale hoogte cijfers)
- minLength (minimale lengte)
- maxLength (maximale lengte)
- pattern (een patroon waarop je moet valideren)
- valideren

Bij register vul je in wat je voor validatie voor dat veld wilt hebben. Het is een object, dus je kunt meerdere dingen toevoegen.

    <input
        {...register("fullName", {required: true, maxLength: 10})}
        type="text"
        name="fullName"
        placeholder="Naam en achternaam"
        id="name"
    />

Als er niet voldaan wordt aan de validaties dan wordt de naam van het veld in het errors object gezet.

    const {register, handleSubmit, formState: {errors}} = useForm();
    
    return (
       <>
         <h1>Weer bestellen</h1>
         <form onSubmit={handleSubmit(onSubmitButton)}>
           <input
                    {...register("fullName", {required: true, maxLength: 10})}
                    type="text"
                    name="fullName"
                    placeholder="Naam en achternaam"
                    id="name"
                />
                {errors.fullName && (
                    <span role="alert">
                        This field is too long
                    </span>
                )}
            <input
                    {...register("plaatsnaam")}
                    type="text"
                    name="plaatsnaam"
                    placeholder="Plaatsnaam"
                    id="plaatsnaam"
                />
         </form>
       </>
    )

Wanneer je een naam dat langer is dan 10 karakters invult krijg je de melding "This field is too long". De gebruiker moet de naam aanpassen en dan pas kan hij het formulier opsturen.