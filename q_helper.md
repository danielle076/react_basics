## Helper functie

We noemen iets een helper functie als het een pure JavaScript functie is en wanneer het niets met React te maken heeft.

Deze helper functies hebben bijvoorbeeld geen state nodig, daar zijn ze namelijk niet afhankelijk van. Je kunt zo'n functie extern neerzetten en hergebruiken.

### Voorbeeld 1
Een voorbeeld is een weather app die een weersverwachting terugkrijgt. Dit kan in Farhenheit of in Celsius. Om deze berekening te maken kun je JavaScript gebruiken die alleen een berekening doet. Dus in de helper functie gooien we een hoeveelheid Celsius en we verwachten een omgerekende eenheid terug. Deze functie heeft alleen JavaScript en verder niets.

- Maak een map `helpers` aan in de src map
- Maak in die map een bestand genaamd `kelvinToCelcius.js`
- Maak daarin een functie waaraan je een getal in kelvin mee kunt geven en de temperatuur (afgerond) in Celcius teruggeeft. Dus een input van 276.35 geeft 3° C. De formule hiervoor is: Celcius = kelvin - 273.15.

      function kelvinToCelcius(kelvin) {
        return `${Math.round(kelvin - 273.15)}° C`;
      }
      
      export default kelvinToCelcius;
  

- Exporteer deze functie als default uit het bestand
- Importeer het in het bestand waarin je het gaat gebruiken

      import kelvinToCelcius from './helpers/kelvinToCelcius';   
  
### Voorbeeld 2

We hebben een functie die ervoor zorgt dat cijfers achter de komma niet worden getoond.

<i>Digits.js</i>

    function Digits(num){
      return num?.toFixed(0);
    }
    
    export default Digits;

<i>Nutrients.js</i>

    import Digits from '../../components/digits/Digits'

