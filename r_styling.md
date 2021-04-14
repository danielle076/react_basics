## CSS

CSS kan soms lastig zijn. Men heeft verschillende systemen verzonnen om CSS duidelijker en de handiger te maken.

De technieken van CSS staan op zichzelf en zijn van toepassing op meerdere systemen (dus niet alleen voor React). SASS is bijvoorbeeld wat minder vriendelijk voor React, omdat er een hoop oplossingen in zitten die niet handig zijn voor React en BEM is heel fijn wanneer je met Angular werkt.
 
### CSS: Styling toevoegen 
Voor elk .js bestand heb je een .css bestand. 

    components (hoofdmap) 
      button (map)
        Button.js 
        Button.css 
      input (map) 
        Input.js 
        Input.css 

## CSS MODULES
Stel je hebt een `className` "error" in Button.js staan en je gebruikt toevallig dezelfde `classname` "error" in Input.js. Als deze "error" alleen in Input.css wordt aangemaakt, dan werkt dit ook voor Button.js. 

Het lijkt wanneer we alles in aparte .css bestanden zetten dat het uniek is voor die ene .js file is, maar dit is niet zo: bij React worden alle CSS globaal samengevoegd (in één file) en toegepast.

Om te voorkomen dat alles wordt samengevoegd kun je een module gebruiken:
- naam bestand: Button.module.css
- in onze import zet je niet `import './Button.css';` maar `import styles from '.Button.module.css'`
- bij het gebruik van een className "error" geef je het object mee: `className={styles.error}`

Let op: je kunt geen `-` meer neerzetten in je `className` omdat het een JavaScript object is geworden: `{styles.error}`. Stel je CSS class heet `.default-button` en je maakt er een CSS modules van dan kun je niet zeggen: `className={styles.default-button}`. Zodra er een teken in de key staat dan gebruik je blokhaken en maak je er een String van: `className={styles.["default-button"]}`.

Let op: Wanneer je een type selector gebruik in je CSS, bijvoorbeeld een `button` of `h1` dan wordt dit globaal voor alles toegepast.

### Voorbeeld
Map components > button > Button.js

    import React from 'react';
    import styles from './Button.module.css';
    
    function Button({ children, clickHandler, type }) {
        return (
            <button
                type="button"
                className={type === styles.outline ? styles.outline : styles.default}
                onClick={clickHandler}
            >
                { children }
            </button>
        );
    }
    
    export default Button;
 
Map components > button > Button.module.css

    .default {
        padding: 16px;
        border-radius: 16px;
        border: none;
        background-color: #f7f7f7;
        margin: 20px 0;
    }
    
    .outline {
        margin: 40px 0;
        padding: 16px;
        border: 1px solid black;
        border-radius: 16px;
        background-color: white;
    }

## BEM
BEM is een populaire naming convention voor classen in HTML en CSS. Naming convention: regels voor het verzinnen van namen voor je CSS classen

BEM zorgt ervoor dat het de relatie tussen HTML en CSS beter te begrijpen is voor developers, omdat er een duidelijke structuur inzit.

BEM lost meerdere dingen op:
- je kan meerdere classes hebben met dezelfde naam
- dat we CSS schrijven waarvan we eigenlijk later niet meer zo goed weten waarvoor het was
- heel veel dingen niet meer dubbel hoeven te schrijven

BEM staat voor Block Element Modifier
*  Block (basis klasse die op het hoofd element staat): Artikel, Searchbar en Menu (de componenten in React), die krijgen een block-klasse: `.article .search-bar` en `.menu`.
* Element (hoofd element die elementen bevatten): Artikel titel, Search Input veld en Menu item, die krijgen een element-klasse: `.article__title .search-bar__input` en `.menu__item`.
* Modifier (verschillende versies): Featured artikel, Input with error en Highlighted menu item, die krijgen een modifier-klasse: `.article--featured .search-bar__input--error` en `.menu__item--highlighted`.

Wat moet je niet doen met BEM:
- geen diepere lagen creëren
- ook niet bedoelt om de structuur te beschrijven, dus .content__article__title mag niet
- zet nooit ergens een modifier class op zonder de basis (block) class
- nest zo min mogelijk elementen in elkaar

### Voorbeeld
Map components > button > Button.js

    import React from 'react';
    import styles from './Button.module.css';
    
    function Button({ children, clickHandler, type }) {
        return (
            <button
                type="button"
                className={type === styles[`button__outline`] ? styles[`button__outline`] : styles[`button`]}
                onClick={clickHandler}
            >
                { children }
            </button>
        );
    }
    
    export default Button;

Map components > button > Button.module.css

    .button {
        padding: 16px;
        border-radius: 16px;
        border: none;
        background-color: #f7f7f7;
        margin: 20px 0;
    }
    
    .button__outline {
        margin: 40px 0;
        padding: 16px;
        border: 1px solid black;
        border-radius: 16px;
        background-color: white;
    }

## SASS
Sass zorgt ervoor dat we de CSS mooi kunnen opsplitsen, dat we variabele makkelijker kunnen gebruiken en dat we alles beter kunnen organiseren. Zonder dat we `className` of dergelijke voor hoeven te gebruiken is SASS een manier om dat te structureren.

Sass staat voor Syntactically Awesome Style Sheets en is een design systeem. 

Sass is the most mature, stable, and powerful professional grade CSS extension language in the world.

Sass is iets wat je moet installeren (net zoals met axios): `npm install sass --save-dev`.<br/>
De dev betekend dat we het alleen maar gebruiken tijdens het developen, het is alleen maar om ons leven als developer makkelijker te maken

### Voorbeeld
1. installeer: npm install sass --save-dev
2. Vervang alle .css naar.scss
3. Nieuwe map maken: scss. We maken een plekje waar we alle algemene css in willen opslaan, dingen die we kunnen hergebruiken, die niet specifiek bij een component horen maar globaal toegepast kunnen worden
4. Nieuwe file in map scss: _variables.scss
5. Variabele maken in _variables.scss, bijv. een kleur die vaak gebruikt word: `$color-primary: #D6FFF6;`, `$color-secundary: #4DCCBD;` en `$color-white: #FFF;`
6. Variabele gebruiken, die moet je eerst importeren: `@import '../scss/variables';` en vervolgens in de file zetten, bijvoorbeeld: `background-color: $color-secundary;`

Map scss > _variables.scss

    $color-primary: #d6fff6;
    $color-button: #f7f7f7;
    $color-white: #fff;

Map components > button > Button.css

    @import '../../scss/variables';
    
    .default {
        padding: 16px;
        border-radius: 16px;
        border: none;
        background-color: $color-button;
        margin: 20px 0;
    }
    
    .outline {
        margin: 40px 0;
        padding: 16px;
        border: 1px solid black;
        border-radius: 16px;
        background-color: $color-white;
    }