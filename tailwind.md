# Tailwind CSS
[Tailwind CSS](https://tailwindcss.com/) ist ein opinionated CSS Framework. 

> "a **utility-first CSS framework** packed with utility classes like flex, text-center and rotate-90 that can be composed to build any design, directly in your markup (HTML or JSX)"

**utility-first CSS approach**: Man schreibt (bzw. nutzt) viele CSS Klassen, die jede für sich nur eine einzige Aufgabe erfüllen und kombiniert diese dann nach Bedarf um die Elemente entsprechend zu stylen und das gesamte Layout daraus zu machen.

Die Idee ist, dass man viele CSS Klassen zu einem Element zuweist und sich jede Klasse nur um ein Detail des Stylings kümmert. Dadurch kann man sehr granular das Styling festlegen. Der Nachteil dieses Ansatzes ist, dass man sehr viele einzelne Klassen zu einem Element hinzufügen muss um es "komplett" zu stylen.

## Installation von Tailwind CSS (Stand Oktober 2024)

### Paketinstallation
Zuerst muss man Tailwind CSS mittels npm installieren
```
npm install -D tailwindcss
npx tailwindcss init
```

### Konfig anpassen
Dann muss man die tailwind.config.js anpassen:
```
  content: ['./index.html', './src/**/*.{js,ts,jsx,tsx}'],
```

### Tailwind CSS includes eintragen
Dann muss man die "Includes" in die index.css eintragen:
```
@tailwind base;
@tailwind components;
@tailwind utilities;
```

### vite.config.js anpassen
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
