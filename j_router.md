## Router

Componenten vormen het hart van React's krachtige, declaratieve programmeermodel. React Router is een verzameling navigatiecomponenten die samen met je applicatie declaratief kunnen worden samengesteld. Of je nu bookmarkable URL's voor je webapp wilt hebben of een samenstelbare manier om te navigeren in React Native, React Router werkt overal waar React rendert.

### Installeren
`npm install react-router-dom` <br/>
of<br/>
`npm install react-router-dom --save` (zorgt ervoor dat hij in package.json staat en voor iemand die hem dan binnenhaalt via bijvoorbeeld github staat hij er al in)

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
Wanneer je routing wilt gaan gebruiken moet je hem importeren.

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

Dit voorbeeld is niet juist. Het is nu niet mogelijk om in de App.js dingen te gebruiken zoals bijvoorbeeld `useHistory`, omdat de dingen van React Router beschikbaar zijn BINNEN het Router component. Het beste is dus om de `<Router>` op een hoger niveau te zetten, namelijk in index.js.

    ReactDOM.render(
        <React.StrictMode>
            <Router>
                <App/>
            </Router>
        </React.StrictMode>,
        document.getElementById('root')
    )

### Switch en route
Je zet de `<Switch>` en `<Route>` om de section heen en niet de navigatie want de navigatie blijft altijd staan.

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

Om dit te fixen kun je een exact-attribuut toevoegen aan de routes die gedeeltelijk overeenkomen met andere routes, zoals bij de home pagina en de food pagina (exact zet je bij de kortste link).

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
Navigatie toevoegen doe je met `<NavLink>`. Je kan alleen verwijzen naar URL's die je in je Switch/Route heb gedefinieerd. Met `activeClassName="active-link"` kun je in je CSS stylen.

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

CSS toevoegen, wanneer een link actief is wordt hij de kleur `coral`.

    .active-link{
        background-color: coral;
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