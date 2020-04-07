# Opdracht FAQ Component
Jullie gaan een FAQ Component maken. Zodra je op een vraag klikt dan moet hij openvouwen met het antwoord op de vraag.
Voor deze opdracht moet je de twee videos hebben bekeken over componenten de theorie video en praktijk video.

__Leerdoelen__
* Jullie kunnen HTML omzetten in een Component
* Jullie kunnen EventListeners gebruiken om de component in- en uit te klappen.
* Jullie kunnen een Array maken met data
* Jullie kunnen een for-of loop gebruiken
* Jullie kunnen door de Array heen loop-en en meerdere Components genereren op basis van Array data
* Jullie kunnen classList.toggle gebruiken

##### Maak voor elke opdracht een bijpassende commit message

De HTML van de component bevatten twee `p` elementen als childelement in de parent element `div`, deze is vrij simpel.
```html
<div class="faqComponent">
    <p>Is dit wel een veilige website?</p>
    <p class="hidden">Nee wij kunnen niet garanderen dat dit een veilige website is.</p>
</div>
```

## Opdracht 1: 
* Maak een bestand aan in de map `js\components\` en noem dat bestand `QuestionComponent.js`.
* Vervolgens erf je de `QuestionComponent` over van `Component` met het `extends`-keyword. In de constructor van een subklasse moet altijd de constructor van de hoofdklasse worden aangeroepen met de `super`-keyword.
* Maak van dit alles een commit

## Opdracht 2:
* Bekijk de HTML en maak de component zo compleet mogelijk na met de juiste innerHTML.
* Test met `console.log` in de controller of de `rootElement` de juiste HTML maakt. Zie video's voor meer details.
* Zodra dit het geval is commit de code

## Opdracht 3:
* Zorg ervoor dat je in de contructor de vraag en antwoord ontvangt zodat je dit in de innerHTML kan zetten
```javascript
// Voorbeeld constructor QuestionComponent.js
constructor(vraag, antwoord) {
    ...

    this.vraag = vraag;
    this.antwoord = antwoord;

    ...
}

// Voorbeeld initView() variabele overzetten naar innerHTML
initView() {
    this.rootElement.innerHTML = `
        <p>${this.vraag}</p>
        <p>${this.antwoord}</p>
    `
    ...
}

```

* Test de component door hem in de `IndexController.js` aan te maken en plaats hem in de `<section id="faqSection">` gebruik hiervoor bijvoorbeeld: `getElementById()`. Zie video's voor meer details. Ook als je een component wilt toevoegen moet je de `getView()`-methode gebruiken om de rootElement met de HTML op te halen. Dit kan je vervolgens toevoegen aan de section.

```javascript
// Aanmaken van een object waarvan de constructor parameters heeft
let qComponent = new QuestionComponent("Argument 1: Vraag", "Argument 2: Antwoord"); 
```
* Zodra alles werkt kan je een commit maken

## Opdracht 4:
Zodra je één werkende component hebt kunnen we de klik functionaliteit toevoegen.
Onderaan de `initView`-methode kunnen wij een EventListener gaan toevoegen. Hiervoor moeten wij de eerste `<p>`-element op halen en daar de `click`-event aan koppelen.
* Geeft de eerste `<p>`-element een `id` in de innerHTML
* Maak een functie aan in de class `QuestionComponent` en noem deze `onClick`, zorg dat de functie het volgende bericht logt in de console: "onClick functie wordt aangeroepen."
* Maak onderaan in de `initView`-methode de `click` eventListener en koppel de `onClick`-methode die je eerder hebt gemaakt
```javascript
// Event listener koppelen
let el = this.getElementById('jouwId');
el.addEventListerner('click', (event) => {this.onClick(event)});
```

* Test of de `onClick`-methode wordt aangeropen door in de console te controleren of je het bericht "onClick functie wordt aangeroepen." ziet zodra je op de vraag klikt. 
* Als de test succesvol is commit je code.

## Opdracht 5:
Zodra er geklikt wordt op een vraag willen wij de de `<p>`-element tonen of onzichtbaar afhankelijk van van de zichtbaarheid van het antwoord.
* Declareer een variabele `awnser` en sla het `<p>`-element op met het antwoord. Probeer met verschillende DOM-selectors(`getElementById` of `querySelector`). Geef als het nodig is het `<p>`-element met het antwoord een ID
* In de methode onClick van de QuestionComponent willen wij een class toevoegen aan de `<p>`-element met het antwoord met `hidden`. Deze klasse in CSS geeft het element de eigenschap `display: none;` wat hem niet zichtbaar maakt. Zorg dat hij bij het klikken de class toevoegd of weghaald afhankelijk van of hij de class `hidden` vindt.

```javascript
// Een class toevoegen of verwijderen van een element
let awnser = this.getElementById('jouId');
// Toevoegen van een class
answer.classList.add('hidden');

// Verwijderen van een class
answer.classList.remove('hidden');

// Toevoegen of verwijderen van een class
answer.classList.toggle('hidden'); // Zodra hij hidden class vind haalt hij hem weg, en zodra hij hem niet vind voegt hij hem toe.
```

* Test je code of hij zichtbaar en niet-zichtbaar wordt tijdens het klikken.
* Als alles werkt maak een commit.

## Opdracht 6:
Je hebt nu een component maar we moeten voor elke vraag en antwoord een component hebben.
* Maak alle QuestionComponenten met alle vragen die in de HTML staan.
* Bedenkt zelf nog twee vragen en antwoorden en verwerk deze ook in de QuestionComponent.
* Voeg alle componenten toe aan de `faqSection`

## Opdracht 7:
Je hebt nu alle componenten gemaakt en als het goed is 6 QuestionComponents. Voor elke QuestionComponent heb je waarschijnlijk het volgende gedaan:
```javascript
let qComponent = new QuestionComponent('vraag', 'antwoord');
```
en dat deze toegevoegd aan de section. 
Hierbij gebruik je best vaak dezelfde regels code en dat kan veel korter gemaakt worden door gebruik te maken van een `Array`.
```javascript
let questions = [{
        question: 'vraag1',
        answer: 'antwoord1'
    },{
        question: 'vraag2',
        answer: 'antwoord2' 
    }
    ... enzo
];
```

Zodra je deze `Array` maakt met de simple object notatie van Javascript kan je gemakkelijk een `Array` vullen met informatie. Uiteindelijk zou deze Array gemakkelijk vervangen kunnen worden door een database/API die vraag aan antwoord vasthoud op dezelfde manier. In javascript is een array te herkennen aan de brackets `[ ]` en een object aan de accolades `{ }`.

* Maak een `Array` voor alle vraag en antwoorden.
* Loop door de `Array` en maak met de gegevens uit de Array de objecten en voeg deze toe aan de `section`
```javascript
for(let i = 0; i < questions.length; i++) {
    const q = questions[i];
    let qComponent = new QuestionComponent(q.question, q.answer);
    // Voeg vervolgens de qComponent toe aan de section
    ...
}

//OF

for(const q of questions) {
    let qComponent = new QuestionComponent(q.question, q.answer);
    // Voeg vervolgens de qComponent toe aan de section
    ...
}
```

* Verwijder de oude codes en mogelijke `console.log`'s en test of alles nog werkt
* Zodra je code opgeschoont is en alles nog werkt maak een commit

## Challenges:
* Nu heb je kleine QuesionComponents en deze zijn geplaatst in een `section` via de controller. Maak van die `section` ook een component en noem deze `FAQSection`. Zorg dat de Array die je hebt gemaakt in de controller in de `FAQSection` komt. Het wordt dus een `FAQSection`  die alle `QuestionComponents` genereerd.

##### Disclaimer
_Alle voorbeeld code in dit bestand zijn voorbeelden. Het kan dus zijn dat jou code er anders uitziet of_
_dat je de code op een andere manier moet toepassen. Verder kan het zijn dat er in de voorbeeld onderdelen nog missen. Je moet daarom zelf goed kijken voor je de code zomaar overneemt en ergens neerzet._
_Met 3 puntjes wordt aangegeven dat er in jou code misschien wel iets staat wat voor het voorbeeld niet relevant is._
```javascript
function() {
    ...
    // hierboven staat mogelijk nog code wat niet relevant is voor dit voorbeeld
    // Hieronder staat mogelijk nog code wat niet relevant is voor dit voorbeeld
    ...
}
```