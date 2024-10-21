# react-docs

Dieses Repository enthält meine Dokumentation/Mitschrift zum Thema React. Hier sammle ich die Notizen der verschiedenen React-Kurse, die ich gemacht habe und ergänze es im Laufe der Zeit mit sonstigen (für mich bemerkenswerten) Erkenntnissen zum Thema React (inkl. "üblicher" Zusatzlibraries, die bei React Verwendung finden).

## Allgemeines / Grundlagen

### Tools um real world React Apps zu schreiben

- CREATE-REACT-APP: Gut für kleine Experimente und Lernen, für Realworld Apps veraltet und langsman
- VITE: Gut für realworld Apps (ist ein modernes build Tool), aber man muss einige Dinge selbst erledigen (z.b. ESLint integrieren, Test Framework einrichten)

## Komponenten - die "Grundbausteine" einer React App

Components sind die Building Blocks von React Apps bzw. von den dadurch erstellten Webseiten. Jede Component hat ihre eigenen Daten, Logiken und Erscheinungsformen.

Komplexe UIs werden dann erstellt, indem man einfach verschiedene Components verwendet. Dazu werden auch sehr oft Components in weiteren Components geschachtelt.

Oft hilft es während der Entwicklung indem man einen Component Tree erstellt (wie hängen die Komponenten zusammen und welche gibt es).

Eine Komponente in React ist eine Javascript-Funktion, die zwei Bedinungen erfüllen muss:
- Der Funktionsname muss mit einem Großbuchstaben beginnen
- Die Funktion muss ein JSX markup zurückgeben und ein JSX markup darf nur ein root-Element enthalten (```return <h1>Heading</h1><p>Absatz</p>;``` ist **nicht** gültig!).

Will man mehr als ein root-Element zurückgeben, kann man das erreichen, indem man die root-Elemente in ein sogenanntes Fragment (```<></>```) einbettet. Dieses Fragment schlägt sich nicht im erzeugten HTML bzw. DOM-Tree nieder, sondern dient nur dazu die Forderung, dass nur ein root-Element zurückgegeben werden darf, zu erfüllen.

Man kann zwar Komponenten ineinander nesten (und macht das sehr oft), aber man nested **niemals** die Funktionen (die die Komponenten eigentlich sind) ineinander (u. a. wegen der Wiederverwendbarkeit von Komponenten)!

React rendert kein true und kein false, aber es rendert 0, daher funktioniert dieses **&&** nicht:

```js
const num=0;
num && <p>Eine Zahl vorhanden</p>; // 0
```

Wegen diesem Verhalten gibt es Entwickler die sagen man soll den **&&** nie zum conditional rendern verwenden (sondern statt dessen den terniery operator) - aber wenn man sicher ist, dass vor dem && ein wirklicher boolean steht - spricht nichts dagegen (und kann kürzer sein).

Man kann in einer Komponente mehrere return statements verwenden (so wie eben im normalen Javascript - das wird dann als "early return" bezeichnet) - und diese von Bedingungen abhängig machen. Natürlich kann eine Komponente dann im jeweiligen Aufruf nur genau ein return ausführen, sprich sobald man in dem konkreten Aufruf ein return erreicht wird die Komponente verlassen und der return ausgeführt.

```js
    function Test(props) {
      if(props.b) { 
        return <div>b ist true!</div> 
      } else {
        return <div> b ist false!</div>
      }
    }
```

Das Beispiel ist zwar "schwachsinnig", aber es zeigt die Idee.

## JSX 

JSX ist eine Erweiterung von Javascript, die es erlaubt Javascript, CSS und HTML in einer React Komponente einzubetten. Auf den ersten Blick sieht es HTML sehr ähnlich (aber es ist Javascript). Und JSX ist nicht "Teil" von React, sondern eine spezielle "Auszeichnungsspache" (die auch von anderen Technologien verwendet wird).

Mit Hilfe des "Tools" Babel wird JSX in entsprechende Javascript Funktionsaufrufe konvertiert. Diese Funktionsaufrufe bestehen aus vielen (geschachtelten) React.createElement() Funktionsaufrufen, die ihrerseits das DOM manipulieren. Dieses manipulierte DOM kann dann vom Browser verstanden und dargestellt werden.

Der "Aufruf" von Babel passiert dabei transparent für den Entwickler - er muss sich also nicht selbst darum kümmern.

JSX ist eine deklarative Sprache, d. h. es wird beschrieben, wie etwas aussehen soll, nicht wie man das erreicht. Im Gegensatz dazu ist der imperative Ansatz - hier wird beschrieben, wie etwas gemacht werden soll (das Aussehen entsteht dann durch die Befolgung der "Arbeitsanweisungen").

JSX Tags müssen **immer auch geschlossen** werden (im Gegensatz zu HTML, wo es möglich ist, bestimmte self closing Tags ohne schließenden Tag zu verwenden). Wenn zwischen dem opening und closing Tag nichts sein soll/muss, kann man das Tag auch "sofort" schließen - aber es muss geschlossen werden, z. b. ```<br />```.

HTML Tags in JSX müssen **immer in Kleinbuchstaben** geschrieben werden! (z. b. ```<h1>``` - nicht ```<H1>```)

Es gibt in HTML Attributnamen, die in Javascript eine (andere) Bedeutung haben. In diesen Fällen heißen die korrespondierenden Attribute in JSX "anders". Die beiden häufigsten abweichenden Attributnamen sind class (wird zu className) und for (wird zu htmlFor).

Um in JSX in den "Javascript-Modus" zu kommen, braucht man **{**, um ihn wieder zu beenden **}**. Man kann das überall dort verwenden, wo Ausdrücke erlaubt sind (weil das Ergebnis von dem Javascript Modus ein "Wert" sein muss). Nicht erlaubt sind hingegen Anweisungen. Innerhalb des Javascript Modus kann man einfach wieder JSX verwenden (ebenfalls dort wo ein Ausdruck erlaubt ist).

### Teilstring in Abhängigkeit von einer Bedingung

Um einen Teil eines String in JSX in Abhängigkeit von einer Bedingung zu erstellen, verwendet man am besten einen Template String für den gesamten String. Dabei wird der fixe Teil einfach hineingeschrieben und für den variablen Teil wechselt man in Javascript und erstellt dort eine entsprechende Bedingung, z. b. `` `7 ist ${7 % 2 === 0 ? 'gerade' : 'ungerade'}` `` (ergibt "7 ist ungerade").

### Stylen von Komponenten

Styles in JSX: Man kann Elemente in JSX stylen (ähnlich wie inline Style in HTML). Das macht man, indem man den gewünschten Style als Javascript-Objekt angibt. Da ein Javascript-Objekt in {} geschrieben wird, ist für die Angabe von Styles eine "doppelte" geschwungene Klammerung notwendig, bzw. richtiger formuliert "sie ergibt sich":

```<h1 style={{ color: 'red' }}>Heading</h1> // da man sich im style in Javascript befindet, kann man ' oder " für die String-Begrenzung verwenden```

In React ist es "fein", inline Styles zu verwenden - weil die "Separation Of Concerns" Komponentenbasiert - und nicht wie bei konventionellem HTML5 technologiebasiert ist.

Viele Style-Attribute (z. b .**font-size** sind keine gültigen Identifier für Javascript, daher wurden diese auf **camel case** Schreibweise umgeändert: das **-** wird entfernt und der erste Buchstabe nach dem - wird groß geschrieben, also **fontSize**).

**Wenn man inline Style in JSX verwendet, ist es wichtig, diesen nur bei Elementen zu verwenden, die sich so dann auch im DOM Tree wiederfinden, d. h. in HTML Elementen.**

## Komponenten Props

props sind eine Möglichkeit um Daten zwischen Komponenten auszutauschen. Sie werden vom Parent zum Child kommuniziert - nie umgekehrt.

Man kann sich props als Argumente für die Komponente vorstellen - das passt auch gut zum Bild, dass die Kommunikation mit props nur von "oben nach unten" geht. Und da man auch "alles" (z. b. Funktionen, andere React Komponenten, ...) als Parameter für Javascript-Funktionen verwenden kann, kann man das auch mit props. Props sind Daten "von außerhalb" der Komponente und dürfen in der Komponente nicht verändert werden!

### Destructuring props

Im Normalfall definiert man eine Komponente nicht so:

```js
    function Komponente(props) {
    ...
    }
```

sondern mit Destructuring

```js
    function Komponente({prop1,prop2}) {
    ...
    }
```


Wenn die Komponente so verwendet wird

```<Komponente prop1="erste Prop" prop2=2 />```

Einerseits ist es dann in der Komponente kürzer zu schreiben (aus props.prop1 wird prop1), andererseits sieht man in der Deklaration sofort welche Props die Komponente erwartet/versteht.


WICHTIG: Die **{} in der Parameter-Liste** - eigentlich logisch, trotzdem vergessen Anfänger sie oft und brauchen dann recht lange, bis sie verstehen, was schief läuft ...

## State

State bezeichnet Daten innerhalb einer Komponente - und auch nur innerhalb dieser Komponente kann der state geändert werden. 

Komponenten sollten auch niemals Daten manipulieren, die außerhalb der Komponente definiert wurden!
```js
    let x=7;
    function Comp() {
      x=5; // DON'T DO THIS ! ! !
      return <div>{x}</div>;
    }
```

In React gibt es daher einen strengen Datenfluss in eine Richtung (top-down, vom Parent zum Child - NICHT UMGEKEHRT!). Andere Frameworks erlauben auch Datenfluss in beide Richtungen (z. b. Angular).

State ist dabei eher ein konzeptioneller Begriff und umfasst die Gesamtheit dieser Daten. "A piece of state" oder "state variable" sind gebräuchliche Begriffe für einzelne Statewerte. Dabei kann "a piece of state" durchaus ein komplexes Objekt sein und ist keinesfalls auf primitive Datentypen beschränkt.

Jede Änderung eines piece of state löst ein Rerendering für die gesamte Komponente aus. Während React die Änderung von primitiven Datentypen erkennt, trifft das auf komplexe Datentypen (Arrays, Objekte, ...) nicht zu. Solche komplexen pieces of state muss man daher immer komplett neu schreiben - damit React die Änderung erkennt.

State erfüllt somit zwei wesentliche Aufgaben:
1. Es löst die Änderung des Aussehens der Komponente aus (weil eine Änderung von State die Komponente erneut rendert)
2. Es speichert Werte zwischen den einzelnen Rerendern

### Erzeugen von State

Um eine state variable zu erzeugen verwendet man **useState**. Bei useState handelt es sich um eine spezielle eingebaute Funktion von React, einen sogenannten Hook. Hooknamen beginnen immer mit use (und so erkennt man sie auch).  Hooks dürfen nur auf dem Top-Level der Komponente verwendet werden und müssen bei jedem Render in der gleichen Reihenfolge (und vollständig) durchlaufen werden. Man kann also nach einem "early return" oder in einer Bedingung keinen Hook verwenden - weil nicht sichergestellt ist, dass man bei jedem Renderdurchlauf zu dieser Stelle kommt.

useState hat einen Parameter (den "Startwert" für diesen piece of state - kann auch weggelassen werden, dann hat dieses piece of state initial "keinen" Wert, d. h. es ist *undefined*) und liefert ein Array mit zwei Elementen zurück. Als erstes Element den aktuellen Wert von dem piece of state, als zweites die sogenannte Set-Funktion. Mit dieser kann man den Wert des piece of state ändern. 

``const [count,setCount] = useState(1);``

Es ist üblich die set-Funktion genauso zu nennen wie das piece of state - mit vorangestelltem set (und in Camelcase-Schreibweise, darum wird der 1. Buchstabe vom Namen des piece of state in der set-Funktion in Großbuchstaben geschrieben).

Wenn man für den Startwert einen Funktionsaufruf übergibt wird diese Funktion beim Erzeugen der Komponente (**initial render**) einmalig aufgerufen und das Ergebnis dieses Aufrufs ist der Startwert für diesen piece of state.

**WICHTIG**: Man darf den Wert einer State-Variable **nicht manuell ändern**, sondern muss dass immer über die set-Function machen. Der Grund dafür ist, dass React nur über die set-Function mitbekommt, wenn sich der Wert des States ändert, d. h. wenn man den Wert einer State-Variable direkt ändert, wird dadurch kein Rerender der Komponente ausgelöst.

Im Normalfall geht es auch gar nicht, die State-Variable direkt zu ändern, weil diese im Normalfall mit const deklariert wird (solange es sich um einen "primitiven" Datentyp handelt, bei Arrays oder Objekten geht es "leider doch").

Um in React eine Component View zu aktualisieren, muss man den State der Component verändern. Das löst automatisch einen rerender der Component aus. Und ein Rerender ist im Wesentlichen das löschen und neuerliche Erzeugen der Component View. Dabei bleibt aber der State erhalten!

### Ändern vom State

Wenn man eine State-Variable in Abhängigkeit vom aktuellen Wert ändern will (z. b. um 1 erhöhen) muss man eine Callback-Funktion verwenden. Diese hat einen Parameter (es wird von React automatisch der aktuelle Wert des States übergeben) und der Rückgabewert der Funktion wird zum neuen Wert vom State.

```js
const [count,setCount] = useState(1);
...
setCount(p => p + 1); // kurz fuer setCount(function (prev) { return prev + 1 });
```

Wenn man die State-Variable unabhängig vom aktuellen Wert der State-Variable ändert ist es nicht notwendig eine Callback-Funktion zu verwenden, d. h.

```js
const [time,setTime]=useState((new Date).toLocalTimeString());
...
setTime((new Date).toLocalTimeString()); // ist OK weil der derzeitige State "egal" ist
```

Jede Komponente hat ihren eigenen State bzw. genauer jede Instanz einer Komponente hat ihren eigenen State, d. h. wenn auf einer Seite mehrere Instanzen einer Counter Komponente sind hat jede dieser Instanzen ihren eigenen State - und weiß nichts vom State anderer Instanzen.

Man kann sich das User Interface als eine Funktion über den State (aller enthaltenen Komponenten) vorstellen. Bei einer React Applikation geht es daher im wesentlichen darum, wie der State im Laufe der Zeit geändert wird - und die Applikation kümmert sich darum, dass der jeweils gerade gültige Zustand in der UI korrekt dargestellt wird.

Der Entwickler beschreibt diese Änderung im Lauf der Zeit mittels State, Event Handler und JSX.

"Spielregeln für State":
- Man sollte eine State Variable für alle Daten, die eine Komponente über die Zeit beachten soll, verwenden.
- Wann immer man will, dass etwas dynamisch in einer Komponente ist, verwendet man eine State Variable - und verändert den Wert dieser, wenn es sich verändern soll.
- Wenn sich das Aussehen (oder die dargestellten Daten) in einer Komponente ändern sollen, muss man den State der Komponente ändern. Das passiert zumeist in Event Handlern.
- Wenn man eine Komponente schreibt ist es hilfreich sich ihre Darstellung als eine Reflektion des States im Lauf der Zeit vorzustellen.
- Für Daten, die kein Rerendering auslösen sollen, darf keine State Variable verwendet werden! Statt dessen soll eine normale Variable verwendet werden.
- Für Daten, die sich aus einem oder mehreren State Variablen ableiten lassen, sollte ebenfalls eine normale Variable verwendet werden.

Die Verwendung einer State Variable hat immer drei Schritte:
1. Definition mit useState
2. Verwendung innerhalb von JSX
3. Verändern des Werts mit der set-Funktion

Wenn man eine State Variable hat, die eine dieser drei Dinge nicht braucht ist es wahrscheinlich keine State Variable...

## Formulare

Form Elemente (wie beispielsweise input) haben ihren State im DOM. In React will man aber den State in der Komponente haben. Daher verwendet man "Controlled Elements".

Diese erzeugt man wie folgt:
- man braucht eine state Variable, die den state (=Wert des Form Elements) speichert
- man weißt dem value Property des Form Elements die state Variable zu
- in dem Form Element definiert man einen event Handler, der die set-Function der State-Variable mit dem zu setzenden Wert aufruft. Für eine state Variable desc, die über ein input Element erfasst werden soll wäre das ``<input value={desc} onChange={(e) => setDesc(e.target.value)}; />``

Im Normalfall ist e.target.value immer vom Typ string. Wenn man weiß, dass es eine Zahl ist (weil es beispielsweise aus einem select kommt, wo man die Optionen im Skript selbst erzeugt hat, kann man das ganze mittels ``Number(e.target.value)`` in eine Zahl umwandeln - im obigen Beispiel wäre das ``setDesc(Number(e.target.value))`` 

**bis "73. Controlled Elements" übernommen**
