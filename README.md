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

### JSX 

JSX ist eine Erweiterung von Javascript, die es erlaubt Javascript, CSS und HTML in einer React Komponente einzubetten. Auf den ersten Blick sieht es HTML sehr ähnlich (aber es ist Javascript).

Mit Hilfe des "Tools" Babel wird JSX in entsprechende Javascript Funktionsaufrufe konvertiert. Diese Funktionsaufrufe bestehen aus vielen (geschachtelten) React.createElement() Funktionsaufrufen, die ihrerseits das DOM manipulieren. Dieses manipulierte DOM kann dann vom Browser verstanden und dargestellt werden.

Der "Aufruf" von Babel passiert dabei transparent für den Entwickler - er muss sich also nicht selbst darum kümmern.

JSX ist eine deklarative Sprache, d. h. es wird beschrieben, wie etwas aussehen soll, nicht wie man das erreicht. Im Gegensatz dazu ist der imperative Ansatz - hier wird beschrieben, wie etwas gemacht werden soll (das Aussehen entsteht dann durch die Befolgung der "Arbeitsanweisungen").

JSX Tags müssen **immer auch geschlossen** werden (im Gegensatz zu HTML, wo es möglich ist, bestimmte self closing Tags ohne schließenden Tag zu verwenden). Wenn zwischen dem opening und closing Tag nichts sein soll/muss, kann man das Tag auch "sofort" schließen - aber es muss geschlossen werden, z. b. ```<br />```.

HTML Tags in JSX müssen **immer in Kleinbuchstaben** geschrieben werden! (z. b. ```<h1>``` - nicht ```<H1>```)

Es gibt in HTML Attributnamen, die in Javascript eine (andere) Bedeutung haben. In diesen Fällen heißen die korrespondierenden Attribute in JSX "anders". Die beiden häufigsten abweichenden Attributnamen sind class (wird zu className) und for (wird zu htmlFor).

### Stylen von Komponenten

Styles in JSX: Man kann Elemente in JSX stylen (ähnlich wie inline Style in HTML). Das macht man, indem man den gewünschten Style als Javascript-Objekt angibt. Um in JSX in den "Javascript-Modus" zu kommen, braucht man {, um ihn wieder zu beenden }. Da ein Javascript-Objekt in {} geschrieben wird, ist für die Angabe von Styles eine "doppelte" geschwungene Klammerung notwendig, bzw. richtiger formuliert "sie ergibt sich":

```<h1 style={{ color: 'red' }}>Heading</h1> // da man sich im style in Javascript befindet, kann man ' oder " für die String-Begrenzung verwenden```

In React ist es "fein", inline Styles zu verwenden - weil die "Separation Of Concerns" Komponentenbasiert - und nicht wie bei konventionellem HTML5 technologiebasiert ist.

Viele Style-Attribute (z. b .**font-size** sind keine gültigen Identifier für Javascript, daher wurden diese auf **camel case** Schreibweise umgeändert: das **-** wird entfernt und der erste Buchstabe nach dem - wird groß geschrieben, also **fontSize**).

**Wenn man inline Style in JSX verwendet, ist es wichtig, diesen nur bei Elementen zu verwenden, die sich so dann auch im DOM Tree wiederfinden, d. h. in HTML Elementen.**

### Props

props sind eine Möglichkeit um Daten zwischen Komponenten auszutauschen. Sie werden vom Parent zum Child kommuniziert - nie umgekehrt.

Man kann sich props als Argumente für die Komponente vorstellen - das passt auch gut zum Bild, dass die Kommunikation mit props nur von "oben nach unten" geht. Und da man auch "alles" (z. b. Funktionen, andere React Komponenten, ...) als Parameter für Javascript-Funktionen verwenden kann, kann man das auch mit props. Props sind Daten "von außerhalb" der Komponente und dürfen in der Komponente nicht verändert werden!

### State

State bezeichnet Daten innerhalb einer Komponente - und auch nur innerhalb dieser Komponente kann state geändert werden. 

Komponenten sollten auch niemals Daten manipulieren, die außerhalb der Komponente definiert wurden!
```
    let x=7;
    function Comp() {
      x=5; // DON'T DO THIS ! ! !
      return <div>{x}</div>;
    }
```

In React gibt es daher einen strengen Datenfluss in eine Richtung (top-down, vom Parent zum Child - NICHT UMGEKEHRT!). Andere Frameworks erlauben auch Datenfluss in beide Richtungen (z. b. Angular).

