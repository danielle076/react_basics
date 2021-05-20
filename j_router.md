## Router

Componenten vormen het hart van React's krachtige, declaratieve programmeermodel. React Router is een verzameling navigatiecomponenten die samen met je applicatie declaratief kunnen worden samengesteld. Of je nu bookmarkable URL's voor je webapp wilt hebben of een samenstelbare manier om te navigeren in React Native, React Router werkt overal waar React rendert. Je kunt de documentatie van React Router hier vinden: [React Router](https://reactrouter.com/web/guides/quick-start)

### Installeren
`npm install react-router-dom` <br/>

### Navigatie
We beginnen met een simpele navigatie + inhoud pagina.

    function App() {
        return (
            <>
                <nav>
                    <ul>
                        <li>
                            Link 1
                        </li>
                        <li>
                            Link 2
                        </li>
                    </ul>
                </nav>
                <section>
                    <h1>Dit is een titel</h1>
                    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Distinctio, eligendi nihil nostrum omnis
                        quia recusandae tenetur? Ad alias, architecto dolor eius, iure maxime minima necessitatibus quae
                        quia ratione saepe tenetur.</p>
                </section>
            </>
        );
    }

### Routing importeren
Wanneer je routing wilt gebruiken moet je hem importeren.

    import {
        BrowserRouter as Router,
        Switch,
        Route,
        Link,
        NavLink
    } from "react-router-dom";

### Router
Router is het buitenste element, die moet eromheen worden gewrapped.

    function App() {
        return (
            <Router>
                <nav>
                    <ul>
                        <li>
                            Link 1
                        </li>
                        <li>
                            Link 2
                        </li>
                    </ul>
                </nav>
                <section>
                    <h1>Dit is een titel</h1>
                    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Distinctio, eligendi nihil nostrum omnis
                        quia recusandae tenetur? Ad alias, architecto dolor eius, iure maxime minima necessitatibus quae
                        quia ratione saepe tenetur.</p>
                </section>
            </Router>
        );
    }

Bovenstaand voorbeeld is niet juist. Het is nu namelijk niet mogelijk om in de App.js dingen te gebruiken zoals bijvoorbeeld `useHistory`, omdat de dingen van React Router beschikbaar zijn BINNEN het Router component. Het beste is dus om de `<Router>` op een hoger niveau te zetten, namelijk in index.js.

    ReactDOM.render(
        <React.StrictMode>
            <Router>
                <App/>
            </Router>
        </React.StrictMode>,
        document.getElementById('root')
    )

### Switch en route
Je zet de `<Switch>` en `<Route>` om de section heen en niet om de navigatie want de navigatie blijft altijd staan.

    function App() {
        return (
            <>
                <nav>
                    <ul>
                        <li>
                            Link 1
                        </li>
                        <li>
                            Link 2
                        </li>
                    </ul>
                </nav>
                <Switch>
                    <Route>
                        <section>
                            <h1>Dit is een titel</h1>
                            <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Distinctio, eligendi nihil nostrum
                                omnis quia recusandae tenetur? Ad alias, architecto dolor eius, iure maxime minima
                                necessitatibus quae quia ratione saepe tenetur.</p>
                        </section>
                    </Route>
                </Switch>
            </>
        );
    }

### Route component
Een `<Route>` component geeft je altijd een path mee. De home pagina ziet er als volgt uit: `<Route path="/">`.

    <Switch>
        <Route path="/">
            <section>
                <h1>Dit is een titel</h1>
                <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Distinctio, eligendi nihil nostrum
                    omnis quia recusandae tenetur? Ad alias, architecto dolor eius, iure maxime minima
                    necessitatibus quae quia ratione saepe tenetur.</p>
            </section>
        </Route>
    </Switch>

### Meerdere Route componenten pagina's

    <Switch>
        <Route path="/">
            <section>
                <h1>Dit is een home pagina</h1>
                <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Distinctio, eligendi nihil nostrum
                    omnis quia recusandae tenetur? Ad alias, architecto dolor eius, iure maxime minima
                    necessitatibus quae quia ratione saepe tenetur.</p>
            </section>
        </Route>
        <Route path="/food">
            <section>
                <h1>Dit is een food pagina</h1>
                <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Distinctio, eligendi nihil nostrum
                    omnis quia recusandae tenetur? Ad alias, architecto dolor eius, iure maxime minima
                    necessitatibus quae quia ratione saepe tenetur.</p>
            </section>
        </Route>
        <Route path="/food-pizza">
            <section>
                <h1>Dit is een food-pizza pagina</h1>
                <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Distinctio, eligendi nihil nostrum
                    omnis quia recusandae tenetur? Ad alias, architecto dolor eius, iure maxime minima
                    necessitatibus quae quia ratione saepe tenetur.</p>
            </section>
        </Route>
    </Switch>

Wanneer je in de browser de pagina bekijkt en de URL aanpast naar /food, dan zou je naar de pagina van food moeten gaan. React router werkt volgens een principe dat partial matching heet. De routes worden van boven naar beneden gelezen, en als de URL voor een gedeelte overeenkomt met één van de paden, stopt React Router met zoeken en geeft altijd de eerste match terug. Dus de pagina die hij laat zien is de home pagina, want het eerste wat hij tegenkomt is "/".

Om dit te fixen kun je een `exact-attribuut` toevoegen aan de routes die gedeeltelijk overeenkomen met andere routes, zoals bij de home pagina en de food pagina (exact zet je bij de kortste link).

    <Switch>
        <Route exact path="/">
            <section>
                <h1>Dit is een home pagina</h1>
                <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Distinctio, eligendi nihil nostrum
                    omnis quia recusandae tenetur? Ad alias, architecto dolor eius, iure maxime minima
                    necessitatibus quae quia ratione saepe tenetur.</p>
            </section>
        </Route>
        <Route exact path="/food">
            <section>
                <h1>Dit is een food pagina</h1>
                <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Distinctio, eligendi nihil nostrum
                    omnis quia recusandae tenetur? Ad alias, architecto dolor eius, iure maxime minima
                    necessitatibus quae quia ratione saepe tenetur.</p>
            </section>
        </Route>
        <Route path="/food-pizza">
            <section>
                <h1>Dit is een food-pizza pagina</h1>
                <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Distinctio, eligendi nihil nostrum
                    omnis quia recusandae tenetur? Ad alias, architecto dolor eius, iure maxime minima
                    necessitatibus quae quia ratione saepe tenetur.</p>
            </section>
        </Route>
    </Switch>

### Navlink
Navigatie toevoegen doe je met `<NavLink>`. Je kan alleen verwijzen naar URL's die je in je Switch/Route heb gedefinieerd. Met `activeClassName="active-link"` kun je CSS stylen dat de pagina waar je op zit gehighlight word.

    <nav>
        <ul>
            <li>
                <NavLink to="/food" activeClassName="active-link">Food</NavLink>
            </li>
            <li>
                <NavLink to="/food-pizza" activeClassName="active-link">Food-Pizza</NavLink>
            </li>
        </ul>
    </nav>

CSS: wanneer een link actief is wordt hij de kleur `pink`.

    .active-link{
        background-color: pink;
        color: white;
    }

### Link
Link toevoegen doe je met `<Link>`.

    <Route exact path="/food">
        <section>
            <h1>Dit is een food pagina</h1>
            <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Distinctio, eligendi nihil nostrum
                omnis quia recusandae tenetur? Ad alias, architecto dolor eius, iure maxime minima
                necessitatibus quae quia ratione saepe tenetur.</p>
            <Link to="/">Ga terug naar de homepagina</Link>
        </section>
    </Route>

### Components
Om het geheel overzichtelijk te maken maak je een map components aan en maak je van de drie sections een component. Bijvoorbeeld voor component Food.

    function Food() {
        return (
            <section>
                <h1>Dit is een food pagina</h1>
                <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Distinctio, eligendi nihil nostrum
                    omnis quia recusandae tenetur? Ad alias, architecto dolor eius, iure maxime minima
                    necessitatibus quae quia ratione saepe tenetur.</p>
                <Link to="/">Ga terug naar de homepagina</Link>
            </section>
        );
    }

    export default Food;

In de App.js gebruik je het component als volgt.

    <Route exact path="/food">
        <Food/>
    </Route>

### Dynamische parameters
Dynamische parameters doe je met `useParams`. Je hebt bijvoorbeeld een blog en daar heb je een template-pagina van hoe een blogpost eruit moet komen te zien. Je hoeft niet voor elke blogpost een nieuwe pagina-component te maken. 

`useParams` zorgt ervoor dat we de dynamische parameter uit de URL kunnen halen. De `useParams` zet je in de `<Route>` door een `/:` + `naam`. Op basis van die naam haal je de gegevens eruit die je nodig heb. Zo maak je een dynamische URL.

    <Route exact path="/food/:id">
        <Food/>
    </Route>

Vervolgens gebruik je in Food.js de useParams `id`.

    function Food() {
    const {id} = useParams();
    
        return (
            <section>
                <h1>Dit is een food pagina met gerecht {id}</h1>
                <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Distinctio, eligendi nihil nostrum
                    omnis quia recusandae tenetur? Ad alias, architecto dolor eius, iure maxime minima
                    necessitatibus quae quia ratione saepe tenetur.</p>
                <Link to="/">Ga terug naar de homepagina</Link>
            </section>
        );
    }

### Doorlinken
Wanneer je iemand wilt doorlinken naar een andere pagina met niet een link, maar met het klikken op een button dan doe je dit met `useHistory()`.

In dit voorbeeld wil je naast het klikken op de button ook dat er andere dingen gebeuren zoals dat er iets in de console wordt gelogd.

In de functie `handleClick` heb je geen toegang meer tot het link-component. Met gebruik van de `push` van `useHistory()` kun je pushen naar de link waar je naartoe wilt gaan.

    function App() {
    const history = useHistory();
    
        function handleClick() {
            console.log("Je hebt mij geklikt");
            // de gebruiker doorlinken naar de homepagina
            history.push("/");
        }
    
        return (
            <Route path="/food-pizza">
                <section>
                    <h1>Dit is een food-pizza pagina</h1>
                    <button onClick={handleClick} type="button"></button>
                    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Distinctio, eligendi nihil nostrum
                        omnis quia recusandae tenetur? Ad alias, architecto dolor eius, iure maxime minima
                        necessitatibus quae quia ratione saepe tenetur.</p>
                </section>
            </Route>
        );
    }

### Privateroute
Privateroute gebruik je om content af te schermen van specifieke gebruikers. Bijvoorbeeld je moet admin rechten hebben om ergens bij te kunnen of je moet ingelogd zijn om content te kunnen bekijken.

We doen met `state` alsof de gebruiker is ingelogd = true en niet ingelogd = false. <br/>
Met conditioneel renderen bepalen we of iemand de pagina mag zien wanneer de state true is.

    function App() {
    const [isLoggedIn, toggleIsLoggedIn] = useState(false);
    
        return (
            <>
                <nav>
                    <ul>
                        {isLoggedIn === true &&
                        <li>
                            <NavLink to="/private-page" activeClassName="active-link">Private page</NavLink>
                        </li>}
                    </ul>
                </nav>
    
                <Route path="/private-page">
                    <section>
                        <h1>Dit is een verborgen pagina</h1>
                        <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Distinctio, eligendi nihil nostrum
                            omnis quia recusandae tenetur? Ad alias, architecto dolor eius, iure maxime minima
                            necessitatibus quae quia ratione saepe tenetur.</p>
                    </section>
                </Route>
            </>
        );
    }

Als je hem op `true` zet dan zie je de verborgen pagina bij de navigatie staan.

    const [isLoggedIn, toggleIsLoggedIn] = useState(true);

Wanneer je nu de state op false zet, dan kan de gebruiker nog bij de link waar hij net op zat. Dit is niet de bedoeling.

In plaats van een normale `<Route>` moet je er een private route van maken door middel van het `<Redirect>` component: `<Redirect to="/"/>`.<br/>
Als je ingelogd bent ? dan ga je naar de section en ben je niet ingelogd : dan ga je naar de homepagina.

    <Route path="/private-page">
        {isLoggedIn === true
            ? <section>
                <h1>Dit is een verborgen pagina</h1>
                <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Distinctio, eligendi nihil nostrum
                    omnis quia recusandae tenetur? Ad alias, architecto dolor eius, iure maxime minima
                    necessitatibus quae quia ratione saepe tenetur.</p>
            </section>
            : <Redirect to="/"/>}
    </Route>