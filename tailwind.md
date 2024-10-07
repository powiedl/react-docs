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

Durch diese [Extension](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss) sieht man als Tooltip, was die jeweilige Tailwind-Klasse in nativem CSS macht. Das ist einerseits gut, weil man "nebenbei" CSS lernt/vertieft - und wenn man CSS schon kann eben genau sieht, was mit der jeweiligen Tailwind-Klasse genau passiert. Einfach in VS Code die entsprechende Extension suchen und auf Install klicken (oder über die Webseite der Extension auf Install klicken)

### Tailwind Prettier Extension (einmalig in VS Code)

Mit dieser [Extension](https://github.com/tailwindlabs/prettier-plugin-tailwindcss) werden die Tailwind Klassennamen in der von Tailwind empfohlenen Reihenfolge geschrieben. Die Installation muss nur einmalig erfolgen. Einfach in VS Code die entsprechende Extension suchen und auf Install klicken (oder über die Webseite der Extension auf Install klicken)

### Einbinden der Tailwind Prettier Extension (pro Projekt)

Damit die Extension in dem jeweiligen Projekt arbeitet muss man eine .prettierrc Datei im Root-Verzeichnis des Projekts anlegen und diesen Inhalt einfügen:
```
{ "plugins": [ "prettier-plugin-tailwindcss" ] }
```
Bzw. (wenn es die Datei schon gibt die Datei entsprechend ergänzen).

## Farben in Tailwind

In der [Tailwind CSS Dokumentation](https://tailwindcss.com/docs/customizing-colors) findet man die vordefinierten Farben in Tailwind. Ihr Klassenname setzt sich aus einer "Grundfarbe" und der "Sättigung" zusammen. Die "Grundfarben" sieht man eben auf der Dokumentationsseite, z. b. Slate, Gray, Yellow, Fuchsia ...

Die Sättigung geht von 50 (fast weiß) bis 950 (fast schwarz), wobei von 100 bis 900 nur die 100er existieren (also beispielsweise kein 250).

Die Farbe heißt dann beispielsweise yellow-300 oder slate-50 oder fuchsia-950.

Der Klassennamen ist dann vorne noch ergänzt wofür die Farbe verwendet wird, z. b. text-yellow-300 (Textfarbe, also `color:`), bg-slate-50 (Hintergrundfarbe, also `background-color:`) , shadow-fuchsia-950 (Schattenfarbe, also `shadow-color:`).


Und "natürlich" kann man die Tailwind Klassen genauso in normalem HTML (z. b. in der index.html) verwenden (falls man beispielsweise eine Klasse auf den gesamten Body anwenden will).

## Größenangaben in Tailwind (size-)

Es gibt verschiedene Größenangaben (die auch auf unterschiedlichen Maßeinheiten beruhen). Entweder wird die Größe als Zahl angegeben (dann wird sie auf rem umgerechnet), oder als Bruchzahl (dann wird sie auf % umgerechnet). Daneben gibt es noch `px` (1 Pixel), `full` (100%), `min` (`min-content`), `max` (`max-content`) und `fit` (`fit-content`).

Eine vollständige Auflistung der sizes findet man in der [Tailwind Doku](https://tailwindcss.com/docs/size).

## "Ausbrechen" aus den Vorgaben der Werte

Wenn man mit den angebotenen Auswahlmöglichkeiten nicht auskommt, kann man aus dem Tailwind CSS Desginsystem "ausbrechen". Dazu verwendet man [ und ] (dort, wo normalerweise die Größenangabe steht. Zwischen den [ ] schreibt man dann den Wert, so wie man es in CSS machen würde, z. b. `max-h-[225px]` (ergibt im CSS `max-height: 225px`) oder `tracking-[1em]` (ergibt im CSS `letter-spacing: 1em`).

## Stylen von Text in Tailwind

Die Größe des Texts (wird in Tailwind in rem "übersetzt") gibt man mit `text-*groesse*` an. Gebräuchliche groesse Werte sind `xs`, `sm`, `base`, `lg` , `xl` - also zb `text-xs` oder `text-lg`. Diese setzen auch eine "passende" line-height. (Spannenderweise nicht font-, obwohl die CSS-Eigenschaft font-size heißt).

Die Strichstärke wird mit `font-*stärke*` angegeben. Gebräuchliche stärke Werte sind `thin` (100), `light` (300), `normal` (400), `bold` (700) oder `black` (900). Warum die dickste Stärke black heißt, wissen maximal die Götter ... (alle möglichen Werte findet man wieder in der [Tailwind CSS Doku](https://tailwindcss.com/docs/font-weight))

Außerdem kann man beispielsweise den ganzen Text in Großbuchstaben schreiben, indem man die Klasse `uppercase` verwendet.

`letter-spacing` (in CSS) wird auf `tracking` übersetzt (Basis ist rem), z. b. `tracking-tighter`, `tracking-normal`, `tracking-wide` oder `tracking-widest` ([Vollständige Liste](https://tailwindcss.com/docs/letter-spacing) der letter-spacing). 
