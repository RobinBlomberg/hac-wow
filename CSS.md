# CSS

## Namngivning av klasser

Vi namnger våra CSS-klasser enligt **PascalCase**-formatet:

**`NavigationBar`**
**`Footer__CopyrightText`**

Även om det allmänt vedertagna formatet för CSS-klasser är **kebab-case** (t.ex. "footer__copyright-text") så är min (Robins) erfarenhet att PascalCase är mer lättläst, och ser trevligare ut (smaksak).

## BEM (Block/Element/Modifier)

För att skriva logisk, strukturerad och lätthanterad CSS finns en metodologi som heter BEM (står för "Block/Element/Modifier"). Den innebär att varje klassnamn får innehålla följande delar, med följande syntax:

- **`Block`**: En klass som beskriver ett logiskt block. Ett sidelement som kan innehålla andra sidelement, exempelvis en komponent i React.
- **`__Element`**: En klass som beskriver ett sidelement som finns inuti ett block.
- **`--Modifier`**: En klass som kan läggas till ett block eller element för att förändra dess utseende eller funktion.

Exempel på giltiga klassnamn enligt BEM-modellen:
**`LoginForm`**
**`ProfilePicture__StatusIcon`**
**`Button--Red`**
**`NavBar__MenuItems--Expanded`**

Du kan läsa mer om metodologin här:
http://getbem.com/naming/

### Exempel på användning

```html
<style>
  .Button { background-color: yellow; }
  .Button--Highlighted { background-color: lime; }
  .Button__Icon { font-family: 'Font Awesome'; }
  .Button__Text { font-family: 'Helvetica'; }
  .Button__Text--Bold { font-weight: bold; }
</style>
<button class="Button Button--Highlighted">
  <i class="Button__Icon"></i>
  <span class="Button__Text Button__Text--Bold">
    Settings
  </span>
</button>
```

### ⚠️ Utelämna inte BEM-element när du använder BEM-modifiers

En modifier ska enbart "lägga till" till ett elements existerande utseende, men elementets grundstyling ska alltid finnas.

```html
❌ <button class="Form__Button--Big">Click me</button>
✔️ <button class="Form__Button Form__Button--Big">Click me</button>
```

### ⚠️ Nästla inte BEM-element/-modifiers i klassnamn

Varje klassnamn ska ha exakt ett block, max ett element, och max en modifier.

```html
<button class="Form__Button">
  <i class="❌ Form__Button__Icon"></i>
  <i class="✔️ Form__ButtonIcon"></i>
</button>
<button class="Button">
  <i class="✔️ Button__Icon"></i>
</button>
```

## SASS

För att skriva CSS-kod använder vi ett språk (en preprocessor) som heter SASS (med SCSS-syntax som liknar CSS). Det är en utökning av hur CSS funkar, som tillåter en att skriva CSS-liknande kod på ett effektivare sätt, som sedan kompilerar ner till vanlig CSS-kod.

Läs mer här:
https://sass-lang.com/documentation

### Nesting

För att förenkla skrivandet av regler för när sidelement är inuti varandra, introducerar SASS konceptet nesting, som kombinerar nästlade regler till en platt CSS-struktur. Det går att använda **&**-selectorn för att stoppa in förälderns selector.

**SCSS:**

```scss
nav {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }

  button {
    display: block;
    padding: 6px 12px;
    text-decoration: none;
    
    &.Link--Hidden {
      display: none;
    }
  }
}
```

**CSS:**

```css
nav ul {
  margin: 0;
  padding: 0;
  list-style: none;
}
nav button {
  display: block;
  padding: 6px 12px;
  text-decoration: none;
}
nav button.Link--Hidden {
  display: none;
}
```

### ⚠️ Var försiktig med att nästla för djupt

Ju djupare man nestar, desto större tenderar risken att bli att man genererar väldigt mycket CSS-kod. Om man använder BEM på ett bra sätt går det ofta bra med minimal nesting.

**SCSS:**

```scss
.Section {
  .Form, &.Section__Login {
    ⚠️ button, input[type="button"], input[type="submit"] {
      border: 1px solid black;
    }
  }
}
```

**CSS:**

```css
.Section .Form button,
.Section .Form input[type="button"],
.Section .Form input[type="submit"],
.Section.Section__Login button,
.Section.Section__Login input[type="button"],
.Section.Section__Login input[type="submit"] {
  border: 1px solid black;
}
```

### Variabler

SASS tillåter variabler.

**SCSS:**
```scss
$base-color: #c6538c;
$border-dark: rgba($base-color, 0.88);

.alert {
  border: 1px solid $border-dark;
}
```

**CSS:**
```css
.alert {
  border: 1px solid rgba(198, 83, 140, 0.88);
}
```

### Importering av filer

SASS tillåter importering av filer.

**SCSS:**

```scss
// stylesheets/Button.scss
.Button { background-color: $button-color; }

// stylesheets/index.scss
$button-color: yellow;
body { margin: 0; }
@import "./Button";
```

**CSS:**

```css
body { margin: 0; }
.Button { background-color: yellow; }
```

Detta är de viktigaste funktionerna i SASS, men det finns många fler, exempelvis funktioner. Läs mer på https://sass-lang.com/documentation.

## Stylelint

För att säkerställa en lätthanterad, enhetlig CSS-kodbas som också följer rekommendationer och best practices använder vi [Stylelint](https://stylelint.io/).

För att installera Stylelint i ett projekt:

```
npm install --save-dev stylelint
```

Vi har en egen Stylelint-konfiguration för HAC:

https://github.com/RobinBlomberg/hac-stylelint

I länken ovan finns också instruktioner för hur du installerar konfigurationen i projektet och i VS Code.
