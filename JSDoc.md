# JSDoc

JSDoc är ursprungligen ett system för att generera dokumentationer utifrån kodkommentarer. Det är fortfarande användbart i det syftet, men har också blivit en standard för att ange extra beskrivande information till JavaScript-objekt, och som editorverktyg för att snabbt kunna få upp information om olika objekt.

[JSDoc 3](https://jsdoc.app/index.html) har ungefär 65 officiella taggar, men det är värt att nämna att de flesta av taggarna är till för att specificera funktionalitet som saknas i äldre versioner av JavaScript, eller typinformation om man inte använder TypeScript. Eftersom vi rekommenderar att använda modern TypeScript kommer vi att skippa överflödiga taggar så som `@class`, `@enum`, `@private`, `@readonly`, `@typedef` och dylikt som redan finns i språket. I det här dokumentet kommer vi att nämna de JSDoc-taggar som är mest användbara.

Med det sagt är det ingen dum idé att [se vilka JSDoc-taggar som finns](https://jsdoc.app/index.html).

## [{@link}](https://jsdoc.app/tags-inline-link.html)

En inline-tagg som används för att infoga en länk i en JSDoc-text.

```javascript
/**
 * Check out {@link http://www.google.com|Google} and {@link https://github.com GitHub}.
 */
function myFunction() {}
```

![@link](./assets/JSDoc_Link.png)

## [@description](https://jsdoc.app/tags-description.html)

Beskriver ett objekt. Om det inte är helt självklart vad en funktion gör eller hur och när den ska användas, eller om det finns implementationsdetaljer som är viktiga att nämna, gör det gärna i denna beskrivning.

```javascript
/**
 * @description Add two numbers.
 */
function add(a: number, b: number) {
  return a + b;
}
```

![@description](./assets/JSDoc_Description.png)

Det går också att med fördel skippa taggen helt (om du inte använder en dokumentationsgenerator som verkar kräva det, exempelvis [TypeDoc](https://typedoc.org/).

```javascript
/**
 * Add two numbers.
 */
function add(a: number, b: number) {
  return a + b;
}
```

![@description](./assets/JSDoc_Description2.png)

## [@deprecated](https://jsdoc.app/tags-deprecated.html)

Denna tagg markerar ett objekt som "deprecated" (utdaterad), som en varning om att det inte bör användas längre.

I VS Code syns detta visuellt genom en vit överstruken linje överallt där objektet används.

```javascript
/**
 * @deprecated since version 2.0
 */
function someOldFunction() {
}
```

![@deprecated](./assets/JSDoc_Deprecated.png)

## [@example](https://jsdoc.app/tags-example.html)

En av de mest tacksamma funktionaliteterna när det kommer till att använda JSDoc som ett kommentarsverktyg.

I `@example`-taggen kan man ange en kodsnutt av JavaScript/TypeScript som illustrerar hur en funktion ska användas. Om man hovrar musen över en funktionsreferens i VS Code så visas exempelkoden som formaterad, highlightad kod.

```javascript
/**
 * Solves equations of the form a * x = b
 *
 * @example <caption>Example usage of divide.</caption>
 * divide(5, 10);
 * // returns 2
 *
 * @returns {Number} Returns the value of x for the equation.
 */
const divide = function (a, b) {
  return b / a;
};
```

![@example](./assets/JSDoc_Example.png)

## [@see](https://jsdoc.app/tags-see.html)

Anger en länk till en URL där man kan läsa mer.

Detta är väldigt användbart om man t.ex. jobbar mot en dokumentation, eller om man följer implementationsdetaljer eller guidelines som anges någon annanstans.

```javascript
/**
 * @see {@link http://example.com|The Example documentation}
 */
function doThing() {}
```

![@see](./assets/JSDoc_See.png)

## [@since](https://jsdoc.app/tags-since.html)

Anger i vilken app-version man införde ett specifikt objekt.

Detta är speciellt användbart om man skapar ett externt API, men kan också vara trevlig information internt i ett versionshanterat projekt.

```javascript
/**
 * Provides access to user information.
 * @since 1.0.1
 */
function UserRecord() {}
```

![@since](./assets/JSDoc_Since.png)

## [@summary](https://jsdoc.app/tags-summary.html)

Anges för att skriva en sammanfattad version av en längre beskrivning.

```javascript
/**
 * A very long, verbose, wordy, long-winded, tedious, verbacious, tautological,
 * profuse, expansive, enthusiastic, redundant, flowery, eloquent, articulate,
 * loquacious, garrulous, chatty, extended, babbling description.
 * @summary A concise summary.
 */
function bloviate() {}
```

![@summary](./assets/JSDoc_Summary.png)

## [@throws](https://jsdoc.app/tags-throws.html)

Eftersom TypeScript ännu inte har något sätt att annotera vilka exceptions en funktion kan kasta så kan `@throws`-taggen vara till nytta.

```javascript
/**
 * @throws {TypeError} Argument x must be non-zero.
 */
function baz(x) {}
```

![@throws](./assets/JSDoc_Throws.png)

## [@todo](https://jsdoc.app/tags-todo.html)

Används för att annotera uppgifter som inte ännu är gjorda.

En stark rekommendation, om du använder VS Code, är att installera extensionen [Todo Tree](https://marketplace.visualstudio.com/items?itemName=Gruntfuggly.todo-tree), och att ställa in den att använda strängen `@todo` som markör. På så sätt kommer varje JSDoc-`@todo` i projektet att samlas i ett och samma fönster, och kommer också att markeras med en tydlig färg i koden.

```javascript
/**
 * @todo Write the documentation.
 * @todo Implement this function.
 */
function foo() {
    // write me
}
```

![@todo](./assets/JSDoc_Todo2.png)

## [@version](https://jsdoc.app/tags-version.html)

Anger vilket versionsnummer ett objekt har. Behöver nog sällan användas, men kan vara användbart om man exempelvis vill annotera ett API.

```javascript
/**
 * Solves equations of the form a * x = b. Returns the value
 * of x.
 * @version 1.2.3
 * @tutorial solver
 */
function solver(a, b) {
    return b / a;
}
```

![@version](./assets/JSDoc_Version.png)
