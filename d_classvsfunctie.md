## Class component vs Function component

### Voorbeeld #1 - state initialiseren
Class component

    constructor()
    {
        this.state = {
            counter: 0;
         };
    }

Function component

    [counter, setCounter] = useState(0);

### Voorbeeld #2 - state aanspreken
Class component

    return (
        <p>
            {this.state.counter}
        </p>
    );

Function component

    return (
        <p>
            {counter}
        </p>
    );

### Voorbeeld #3 - state wijzigen
Class component

    () => this.setState({
        counter: 1,
    });

Function component

    () => setSounter(1);

### Wanneer weet je dat je met een class component te maken heb
- this, want dit keyword kan niet gebruik worden in een function component
- render