## Components

Met componenten kunnen we een groot bestand of een complexe webstructuur in kleinere componenten opsplitsen. Bijkomend voordeel is dat we de componenten kunnen hergebruiken wanneer ze dezelfde functionaliteit hebben. 

We gaan de volgende website in kleinere componenten splitsen.

    import React from "react";
    import ReactDOM from "react-dom";
    
    ReactDOM.render(
      <div>
        <h1>My Favourite Foods</h1>
        <ul>
          <li>Bacon</li>
          <li>Jamon</li>
          <li>Noodles</li>
        </ul>
      </div>,
      document.getElementById("root")
    );

Als eerste gaan we een Heading component maken, dit doe je door middel van een functie. De naam van de functie is in React altijd met een hoofdletter. De Heading functie geeft een HTML element terug met behulp van Javascript.

    function Heading() {
      return <h1>My Favourite Foods</h1>;
    }

Nu kun je deze aangepaste Heading component in de React-code gebruiken alsof het een HTML-element is: <Heading />

    ReactDOM.render(
      <div>
        <Heading />
        <ul>
          <li>Bacon</li>
          <li>Jamon</li>
          <li>Noodles</li>
        </ul>
      </div>,
      document.getElementById("root")
    );

Heading staat nog binnen hetzelfde bestand index.js en dat maakt het niet overzichtelijk. We gaan een ES6 functie gebruiken waarbij we onze Heading component importeren vanuit een apart bestand.

We maken een nieuw bestand aan in de src folder genaamd Heading.jsx, dit wordt een custom component. We kopiëren de functie in dit bestand. 

Bestanden index.js en Heading.jsx moeten met elkaar gelinkt worden. Voor index.js is dit import en voor Heading.jsx export.
 
Heading.jsx
    
    import React from "react";
    
    function Heading() {
      return <h1>My Favourite Foods</h1>;
    }
    
    export default Heading;

index.js

    import React from "react";
    import ReactDOM from "react-dom";
    import Heading from "./Heading";
    
    ReactDOM.render(
      <div>
        <Heading />
        <ul>
          <li>Bacon</li>
          <li>Jamon</li>
          <li>Noodles</li>
        </ul>
      </div>,
      document.getElementById("root")
    );

We maken ook een custom component voor de lijst.

index.js

    import React from "react";
    import ReactDOM from "react-dom";
    import Heading from "./Heading";
    import List from "./List";
    
    ReactDOM.render(
      <div>
        <Heading />
        <List />
      </div>,
      document.getElementById("root")
    );

List.jsx

    import React from "react";
    
    function List() {
      return (
        <ul>
          <li>Bacon</li>
          <li>Jamon</li>
          <li>Noodles</li>
        </ul>
      );
    }
    
    export default List;

Wat je normaal ziet in het bestand index.js van veel React apps is dat ze geen HTML elementen zoals een div of een h1 hebben. In plaats daarvan zie je een aangepaste component met de naam App. 
Wat je nu in de index.js ziet staan, wil je in het bestand genaamd App.jsx hebben. Daarnaast worden de bestanden opgeslagen in een directory map genaamd components.

index.js

    import React from "react";
    import ReactDOM from "react-dom";
    import App from "./components/App";
    
    ReactDOM.render(<App />, document.getElementById("root"));

Directory map “components”: App.jsx

    import React from "react";
    import Heading from "./Heading";
    import List from "./List";
    
    function App() {
      return (
        <div>
          <Heading />
          <List />
          <List />
        </div>
      );
    }
    
    export default App;

Directory map “components”: Heading.jsx

    import React from "react";
    
    function Heading() {
      return <h1>My Favourite Foods</h1>;
    }
    
    export default Heading;

Directory map “components”: List.jsx

    import React from "react";
    
    function List() {
      return (
        <ul>
          <li>Bacon</li>
          <li>Jamon</li>
          <li>Noodles</li>
        </ul>
      );
    }
    
    export default List;