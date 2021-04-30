## Class component vs Function component

### State initialiseren
<i>Class component</i>

    constructor()
    {
        this.state = {
            counter: 0;
         };
    }

<i>Function component</i>

    [counter, setCounter] = useState(0);

### State aanspreken
<i>Class component</i>

    return (
        <p>
            {this.state.counter}
        </p>
    );

<i>Function component</i>

    return (
        <p>
            {counter}
        </p>
    );

### State wijzigen
<i>Class component</i>

    () => this.setState({
        counter: 1,
    });

<i>Function component</i>

    () => setSounter(1);

### Wanneer weet je dat je met een class component te maken heb
- door het woordje this: dit keyword kan niet gebruikt worden in een function component
- render