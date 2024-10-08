# Tailwind CSS
[Tailwind CSS](https://tailwindcss.com/) ist ein opinionated CSS Framework. 

> "a **utility-first CSS framework** packed with utility classes like flex, text-center and rotate-90 that can be composed to build any design, directly in your markup (HTML or JSX)"

**utility-first CSS approach**: Man schreibt (bzw. nutzt) viele CSS Klassen, die jede für sich nur eine einzige Aufgabe erfüllen und kombiniert diese dann nach Bedarf um die Elemente entsprechend zu stylen und das gesamte Layout daraus zu machen.

Die Idee ist, dass man viele CSS Klassen zu einem Element zuweist und sich jede Klasse nur um ein Detail des Stylings kümmert. Dadurch kann man sehr granular das Styling festlegen. Der Nachteil dieses Ansatzes ist, dass man sehr viele einzelne Klassen zu einem Element hinzufügen muss um es "komplett" zu stylen.

## Vorteile von Tailwind
- Man muss sich keine Gedanken um die Benennung der Klassen machen
- Markup und Styles werden in einem File bearbeitet (kein "Herumspringen")
- Wenn man Tailwind einmal verstanden hat, versteht man das Styling aller Projekte, die Tailwind verwenden
- Tailwind kann auch als Designsystem angesehen werden - das führt zu besser aussehenden und konsistenten UIs
- Spart viel Zeit
- Die Dokumentation und Integration in VS Code ist hervorragend

## Nachteile von Tailwind
- Das Markup wird "überladen" (im Extremfall "unlesbar"), weil man viele Klassen angeben muss um ein einziges Element zu stylen (Es gibt VS Code Extensions, die die Klassen bei einem Element "ausblenden", wenn man dieses gerade nicht bearbeitet (d. h. der Cursor nicht in der Klassenliste ist), z. b. [Tailwind Fold](https://marketplace.visualstudio.com/items?itemName=stivo.tailwind-fold), aber ich finde den "springenden" Code störender wie die vielen Klassennamen, die man sieht.
- Man muss die ganzen Tailwind-Klassennamen (die man verwendet) lernen
- Man muss Tailwind für jedes Projekt neu installieren und einrichten

## Installation von Tailwind CSS (Stand Oktober 2024)
Dabei muss man zwischen den Schritten, die in jedem Projekt erneut notwendig sind (die Installation von Tailwind im Projekt) und den Schritten, die einmalig notwendig sind (die "Erweiterung von VSCode für Tailwind") unterscheiden.

### Paketinstallation (pro Projekt)
Zuerst muss man Tailwind CSS mittels npm installieren
```
npm install -D tailwindcss
npx tailwindcss init
```

### Konfig anpassen (pro Projekt)
Dann muss man die tailwind.config.js anpassen:
```
  content: ['./index.html', './src/**/*.{js,ts,jsx,tsx}'],
```

### Tailwind CSS includes eintragen (pro Projekt)
Dann muss man die "Includes" in die index.css eintragen:
```
@tailwind base;
@tailwind components;
@tailwind utilities;
```

### vite.config.js anpassen (pro Projekt)
Und zum Schluss muss man noch den PostCSS Prozessor in der vite.config.js eintragen

```
export default defineConfig({
  plugins: [react()],
  css: {
    postcss: {
      plugins: [tailwindcss()],
    },
  },
});
```

### Tailwind CSS IntelliSense Extension (einmalig in VS Code)

Durch diese [Extension](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss) sieht man als Tooltip, was die jeweilige Tailwind-Klasse in nativem CSS macht. Das ist einerseits gut, weil man "nebenbei" CSS lernt/vertieft - und wenn man CSS schon kann eben genau sieht, was mit der jeweiligen Tailwind-Klasse genau passiert. 

**TIP**: Das kann man auch verwenden, um zu prüfen, ob man den Klassennamen richtig geschrieben hat. Wenn beim drüberhovern eine "Übersetzung" in normales CSS kommt, ist er richtig geschrieben - wenn nicht, ist er falsch geschrieben.

Einfach in VS Code die entsprechende Extension suchen und auf Install klicken (oder über die Webseite der Extension auf Install klicken)

### Tailwind Prettier Extension (einmalig in VS Code)

Mit dieser [Extension](https://github.com/tailwindlabs/prettier-plugin-tailwindcss) werden die Tailwind Klassennamen in der von Tailwind empfohlenen Reihenfolge geschrieben. Die Installation muss nur einmalig erfolgen. Einfach in VS Code die entsprechende Extension suchen und auf Install klicken (oder über die Webseite der Extension auf Install klicken)

### Einbinden der Tailwind Prettier Extension (pro Projekt)

Damit die Extension in dem jeweiligen Projekt arbeitet muss man eine .prettierrc Datei im Root-Verzeichnis des Projekts anlegen und diesen Inhalt einfügen:
```
{ "plugins": [ "prettier-plugin-tailwindcss" ] }
```
Bzw. (wenn es die Datei schon gibt die Datei entsprechend ergänzen).

## Tipps und Tricks

### focus: und ring gemeinsam verwenden

Oft wird focus: und ring gemeinsam verwendet, womit fokusierte Elemente eine Umrandung erhalten (was dazu führt, dass man leichter erkennen kann, dass das entsprechende Element den Fokus hat - insbesondere wenn man ring sonst nicht verwendet - oder aber zumindest eine bestimmte Farbe der Umrandung nur für focus: verwendet).

### Klassen zusammenfassen

In Tailwind  schreibt man relativ schnell relativ viele Klassen für ein einzelnes Element. Oft wiederholen sich diese Klassen für verschiedene (gleichartige) Elemente immer wieder. Man kann in solchen Fällen über das CSS-File layer definieren. Diese können dann mehrere solcher wiederholten Klassen zu einer Klasse neuen zusammenfassen:

```
    @layer components {
      .input {
        @apply w-full rounded-full ... md:py-3;
      }
    }
```

Im JSX weist man dann nur noch die Klasse `input` zu, nicht mehr die einzelnen Teile:

``<input className="input w-72" />``

Es handelt sich dabei dann um eine normale "Tailwind-Klasse", d. h. man kann sie auch weiterhin mit anderen Klassen kombinieren - und man kann auch Settings überschreiben (im Beispiel ersetzt `w-72` das `w-full`).

Das macht nur "Sinn" wenn es viele Klassen sind und diese an "vielen" Stellen verwendet werden - sonst ist man wieder dort, wo man vor Tailwind war (*besser wäre es eine React Komponente zu schreiben und diese immer wieder zu verwenden*).

### Zugriff aus CSS auf Farben in Tailwind

Manchmal ist es notwendig, direkt in CSS auf Farben als Teil eines Property Wertes zuzugreifen, das kann man dann mit theme(`colors.`**`farbe`**`.`**`intensität`**) machen, z. b. theme(`colors.stone.600`) oder theme(`colors.blue.200`).

### Defaults von Tailwind ändern/überschreiben

Man kann die Defaults von Tailwind ändern/überschreiben. Dazu muss man das File **tailwind.config.js** editieren. In der [Dokumentation](https://tailwindcss.com/docs/configuration) sieht man, was man da alles angegeben kann. Wenn man eine Einstellung direkt unter theme macht, überschreibt man die Standardeinstellung bzw. die Standardwerte für diese Einstellung. Wenn man es unter extend angibt, werden die eigenen Angaben hinzugefügt.

```
    theme: {
      colors: {
        pizza: '#123456',
      }
    }
```

Damit gibt es nur noch die Farbe #123456 (mit dem Namen pizza), alle anderen Farben (z. b. stone-300) werden "gelöscht".

Wenn man es statt dessen so schreibt:

```
    theme: {
      extend: {
        colors: {
          pizza: '#123456',
        }
      }
    }
```

Wird eine zusätzliche Farbe pizza erzeugt, alle anderen Standardfarben von Tailwind bleiben aber erhalten.

## Erklärungen zur Verwendung von Tailwind

### Farben in Tailwind

In der [Tailwind CSS Dokumentation](https://tailwindcss.com/docs/customizing-colors) findet man die vordefinierten Farben in Tailwind. Ihr Klassenname setzt sich aus einer "Grundfarbe" und der "Sättigung" zusammen. Die "Grundfarben" sieht man eben auf der Dokumentationsseite, z. b. Slate, Gray, Yellow, Fuchsia ...

Die Sättigung geht von 50 (fast weiß) bis 950 (fast schwarz), wobei von 100 bis 900 nur die 100er existieren (also beispielsweise kein 250).

Die Farbe heißt dann beispielsweise yellow-300 oder slate-50 oder fuchsia-950.

Der Klassennamen ist dann vorne noch ergänzt wofür die Farbe verwendet wird, z. b. text-yellow-300 (Textfarbe, also `color:`), bg-slate-50 (Hintergrundfarbe, also `background-color:`) , shadow-fuchsia-950 (Schattenfarbe, also `shadow-color:`).

Und "natürlich" kann man die Tailwind Klassen genauso in normalem HTML (z. b. in der index.html) verwenden (falls man beispielsweise eine Klasse auf den gesamten Body anwenden will).

### Größenangaben in Tailwind (size-)

Es gibt verschiedene Größenangaben (die auch auf unterschiedlichen Maßeinheiten beruhen). Entweder wird die Größe als Zahl angegeben (dann wird sie auf rem umgerechnet), oder als Bruchzahl (dann wird sie auf % umgerechnet). Daneben gibt es noch `px` (1 Pixel), `full` (100%), `min` (`min-content`), `max` (`max-content`) und `fit` (`fit-content`).

Eine vollständige Auflistung der sizes findet man in der [Tailwind Doku](https://tailwindcss.com/docs/size).

### Breite / Höhe
Die Breite wird in Tailwind mit **w-** abgekürzt, die Höhe mit **h-**. Prinzipiell unterstützen beide die Größenangaben, aber zusätzlich haben sie noch ein paar spezielle Möglichkeiten `-screen` (entspricht `100vw` bzw. `100vh`), `-sv[w|h]` (entspricht `100sv[w|h]`, also -svw entspricht 100svw). `-lv[w|h]` (entspricht `100lv[w|h]`) und `-dv[w|h]` (entspricht `100dv[w|h]`).

### "Ausbrechen" aus den Vorgaben der Werte

Wenn man mit den angebotenen Auswahlmöglichkeiten nicht auskommt, kann man aus dem Tailwind CSS Desginsystem "ausbrechen". Dazu verwendet man [ und ] (dort, wo normalerweise die Größenangabe steht. Zwischen den [ ] schreibt man dann den Wert, so wie man es in CSS machen würde, z. b. `max-h-[225px]` (ergibt im CSS `max-height: 225px`) oder `tracking-[1em]` (ergibt im CSS `letter-spacing: 1em`).

### Stylen von Text in Tailwind

Die Größe des Texts (wird in Tailwind in rem "übersetzt") gibt man mit `text-*groesse*` an. Gebräuchliche groesse Werte sind `xs`, `sm`, `base`, `lg` , `xl` - also zb `text-xs` oder `text-lg`. Diese setzen auch eine "passende" line-height. (Spannenderweise nicht font-, obwohl die CSS-Eigenschaft font-size heißt).

Die Strichstärke wird mit `font-*stärke*` angegeben. Gebräuchliche stärke Werte sind `thin` (100), `light` (300), `normal` (400), `bold` (700) oder `black` (900). Warum die dickste Stärke black heißt, wissen maximal die Götter ... (alle möglichen Werte findet man wieder in der [Tailwind CSS Doku](https://tailwindcss.com/docs/font-weight))

Außerdem kann man beispielsweise den ganzen Text in Großbuchstaben schreiben, indem man die Klasse `uppercase` verwendet.

`letter-spacing` (in CSS) wird auf `tracking` übersetzt (Basis ist rem), z. b. `tracking-tighter`, `tracking-normal`, `tracking-wide` oder `tracking-widest` ([Vollständige Liste](https://tailwindcss.com/docs/letter-spacing) der letter-spacing). 

### Spacing in Tailwind

Margin wird mit `m` abgekürzt, padding mit `p`.

Danach kommt entweder ein Bindestrich (dann gilt das Setting für alle vier Seiten) oder weiterer Buchstabe, der die Seiten festlegt, für die es gilt. Gebräuchlich sind `x` (`-left` und `-right`), `y` (`-top` und `-bottom`), `t` (`-top`), `r` (`-right`), `b` (`-bottom`) und `l` (`-left`) und dann der Bindestrich.

Man kann leicht ein Spacing für die child-Elemente festlegen. Dafür gibt es space-richtung-groesse. Die richtung kann dabei x oder y sein. Und für groesse gibt es diverse Werte (die gleichen wie auch für margin und padding), Beispiele: space-x-3 oder space-y-0.5. Das dahinterliegende CSS ist etwas kompliziert (aber das versteckt Tailwind "zum Glück").

Nach dem Bindestrich kommt die "Größe". Mögliche Werte für die Größe sind u. a. 0, 0.5, 1, 1.5, ..., 4, 5, ... 12, 14. 96 ist das Maximum (wobei die Lücken nach oben immer größer werden). Außerdem gibt es noch auto Die vollständige Liste findet man wieder in der [Tailwind Doku](https://tailwindcss.com/docs/customizing-spacing).

### CSS Attribut display
Für das CSS Attribut `display` gibt es auch entsprechende Klassen. Diese sind so gebräuchlich, dass die Tailwind Klassennamen de facto aus dem Wert des display-Attributs bestehen, d. h. `block` ergibt `display: block`, `grid` ergibt `display: grid`. Ausnahme: `hidden` ergibt `display: none`.

### Rahmen

Um einen Border hinzuzufügen, muss man normalerweise `border-seite-staerke` und `border-color` angeben. Bei `border-seite` kann man `-staerke` weglassen, wenn man den Default (1px) will, z. b. `border-b-3 border-slate-500` (macht unten einen 3px Rahmen in slate-500).

### ring ("Umrandung")

Tailwind CSS bietet ein eigenes Utility für "Umrandungen" - nämlich **`ring`** (technisch wird dazu ein box-shadow verwendet). Die Zahl nach ring- gibt die Breite der Umrandung an (0, 1, 2, 4 und 8 - das ist die Breite in px). Außerdem gibt es auch noch nur ring (das entspräche ring-3).

Der Abstand zwischen der Umrandung und dem Element wird mit der Klasse **`ring-offset-`** festgelegt. Dem folgt eine Zahl (0,1,2,4 oder 8). Die Zahl gibt den Abstand in px an. Daneben gibt es auch die Klasse **`ring-inset`** (da befindet sich die Umrandung innerhalb des Elements).

### Responsive Design in Tailwind

Tailwind kommt mit einem mobile-first Ansatz, d. h. man designed die App für die "kleinstmögliche Auflösung" und verändert sie falls die Anzeige größer wird. Tailwind hat 5 vorgegebene media Query breakpoints (`min-width` - ergibt sich aus dem mobile-first Ansatz, d. h. im Normalfall werden Elemente vergrößert oder eingeblendet, wenn die Anzeige eine gewisse Mindestbreite hat).

Die 5 vorgegebenen Breakpoints sind `sm` (>=640px), `md` (>=768px), `lg` (>=1024px), `xl` (>=1280px) und `2xl` (>=1536px).

Und man kann jede der Tailwind-Klassennamen mit dem Breakpoint-Namen und einem : prefixen (und dann gilt das nur für eine Anzeigebreite die zumindest dem Breakpoint entspricht). Beispiel: `sm:my-16` oder `lg:text-xl`. Wenn man mehrere Breakpoints verwenden will (für das gleiche Attribut), muss man sie in "aufsteigender" Reihenfolge angeben (darum kümmert sich aber auch der Prettier).

### Flexbox

Der Flex-Container bekommt die Klasse `flex` (das setzt das CSS `display:flex`). CSS "align-items" wird zu `items-`, CSS "justify-content" wird zu `justify-`.

Details siehe die [Tailwind CSS Doku](https://tailwindcss.com/docs/display#flex)

### Grid

Der Grid-Container bekommt die Klasse `grid`. Um die Zahl der Zeilen festzulegen, gibt man noch `grid-rows-zeilenzahl` an (grid-rows-3 ergibt 3 Zeilen). Analog für die Spalten `grid-cols-spaltenzahl` (grid-cols-2 ergibt 2 Spalten). Das Gap gibt man mit `gap-gapgroesse` an.

Details siehe die [Tailwind CSS Doku](https://tailwindcss.com/docs/display#grid)

### Pseudoklassen

Pseudoklassen werden in Tailwind am Anfang der Klasse geschrieben, also `hover:bg-yellow-500` (um die Hintergrundfarbe im gehoverten Zustand auf yellow-500 zu setzen). Will man mehrere Klassen nur in einem bestimmten Zustand anwenden, muss man den Zustand vor jeder betroffenen Klasse angeben!

