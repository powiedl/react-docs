# Tailwind Grid

Ein Grid besteht aus dem Grid-Container und den Grid-Items. Ein Grid ist immer zweidimensional (auch wenn es vielleicht nur eine Spalte oder eine Zeile ist). 

## Begriffsdefinitionen

Ein Grid besteht aus den **Zellen**. Diese sind im zwei Dimensionalen Raster angeordnet. Die Zellen sind der "Platz" wo dann die Grid Items platziert werden. Im Standardfall belegt ein Item genau eine Zelle.

Die Zeilen werden als **row track**, die Spalten als **column track** bezeichnet.

Die tracks werden von den lines umschlossen, jeder einzelne Track hat dabei eine Beginnline und eine Endline. Die End- und die Beginnline von benachbarten tracks fällt dabei zusammen, darum gibt es immer genau eine Line mehr wie es tracks gibt. Die Lines werden (wie auch die Tracks von links nach rechts bzw. von oben nach unten nummeriert und die Nummerierung startet mit 1). In der gegenläufigen Richtung (also z. b. von rechts nach links wird mit -1 zu zählen begonnen und dann immer um eins erniedrigt). Damit kann man auch "die letzte" oder "die vorletzte" line ansprechen. Außderm kann man lines auch Namen geben.

Wenn man bei der Definition die Zeilen und Spalten festlegt ist dieser Teil des Grids ein **explizites Grid**. Außerdem gibt es bei einem Grid immer eine "Wachstumsrichtung" (kommt eine neue Spalte oder eine neue Zeile dazu, wenn für ein neues Item kein Platz mehr ist). Dieser Teil (der nicht von vornherein definierte ist) wird als **implizites Grid** bezeichnet. Nachdem das Grid erzeugt ist, gibt es aber keinen Unterschied zwischen den beiden Teilen und aus dem Browser kann man auch nicht erkennen, welcher Teil was ist.

Mit Grid wurde auch eine neue Einheit eingeführt **1fr** (fraction). Dabei handelt es sich "um einen Teil des verfügbaren Platzes".

## Items im Grid platzieren

Die Items werden "der Reihe nach" (so wie sie im HTML definiert sind) im Grid platziert. Man kann sowohl die Position als auch die Größe der Items definieren. Wenn dadurch Lücken entstehen werden die von nachfolgenden Items nicht automatisch gefüllt. Man kann diese aber durch entsprechende Platzierungsanweiungen in die Lücken geben.

### Items entlang der Spalten platzieren

Dafür gibt es die Klassen **col-start** und **col-end** und man gibt jeweils die Row Line an, an der das Item beginnt bzw. endet. Außerdem gibt es noch **col-span** - damit definiert man wie viele Zellen Breite das Item haben soll (natürlich sollte man nur zwei der drei Klassen verwenden). Wenn man alle drei verwendet gelten die letzten beiden. Bei col-span gibt es noch den Spezialfall **col-span-full** (damit erstreckt sich das Item über eine ganze Zeile).

### Items entlang der Zeilen platzieren

Analog dazu gibt es die **row-start** und **row-end** Klassen. Damit kann man ein Element auch außerhalb der Reihenfolge im HTML platzieren. Und auch hier gibt es **row-span-full** womit das Item eine ganze Spalte belegt.

## Zellen im Grid positionieren

Wenn das Grid in der Dimension größer als die Summe der Größe aller Items in der Dimension ist (es also im Grid ungenutzten Platz in dieser Dimension gibt) kann man festlegen wie die einzelnen Zellen verteilt werden. Dabei muss man die Ausrichtung in Zeilen und Spalten unterscheiden. Das kann man am Grid Container für alle Zellen oder für die einzelnen Zellen selbt festlegen.

### Zellen in Zeilen im Grid positionieren (horizontal)

Dazu verwendet man **justify-**. Daran anschließend kommt die eigentliche Ausrichtung. Folgende Werte sind möglich:

- **justify-start**: Die Items werden am Anfang der Zeile positioniert.
- **justify-center**: Die Items werden in der Mitte der Zeile positioniert.
- **justify-end**: Die Items werden am Ende der Zeile positioniert.
- **justify-between**: Der Platz wird gleichmäßig verteilt, so dass die Items möglichst weit auseinander liegen, d. h. das erste Item beginnt ganz am Anfang der Zeile und das letzte endet ganz am Ende der Zeile.
- **justify-around**: Der Platz wird so verteilt, dass links und rechts neben jedem Item gleich viel Platz bleibt. Wenn sich zwei Items nebeneinander befinden ist der Platz zwischen ihnen doppelt so groß (weil jedes Item einmal den Platz "mitbringt").
- **justify-evenly**: Der Platz wird gleichmäßig verteilt, aber am Anfang und Ende der Zeile wird auch jeweils einmal dieser Platz frei gelassen.
- **justify-strech**: Die Items werden so groß wie möglich gemacht, d. h. sie nutzen den verfügbaren Platz bestmöglich aus.
- **justify-normal**: Zum "Resettieren" von einer Einstellung. Danach ist es wieder so, als wäre kein justify-content gesetzt.

Diese Klassen setzen das CSS Attribut **justify-content**.

### Zellen in Spalten im Grid positionieren (vertikal)

Dazu verwendet man **content-**. Daran anschließend kommt die eigentliche Ausrichtung. Es sind prinzipiell die gleichen Werte wie bei justify möglich (nur dass es sich hier eben auf Spalten und nicht auch Zeilen bezieht). Also **content-start**, **content-center**, **content-end**, **content-between**, **content-around**, **content-stretch**, **content-evenly** und **content-normal**.

Diese Klassen setzen das CSS Attribut **algin-content**.

### Items in der Zelle positionieren

Das kann man entweder allgemein für alle items festlegen (dann legt man es am Grid Container fest) oder für ein einzelnes Item.

#### Allgemeine Festlegung für die Positionierung eines Items in der Zelle

##### Horizontale Positionierung eines Items in der Zelle

Dazu verwendet man **justify-items-**. Daran anschließend kommt die eigentliche Ausrichtung. Folgende Werte sind möglich:

- **justify-items-start**: Dieses Item wird am Anfang der Zelle positioniert.
- **justify-items-center**: Dieses Item wird zentriert in der Mitte der Zelle positioniert.
- **justify-items-end**: Dieses Item wird am Ende der Zelle positioniert.
- **justify-items-strech**: Dieses Item nimmt die gesamte Breite der Zelle ein.
- **justify-items-normal**: Eine eventuell gesetzte Klasse wird wieder "gelöscht".

Diese Klassen setzen das CSS Attribut **justify-items**.

##### Vertikale Positionierung eines Items in der Zelle

Dazu verwendet man **items-**. Daran anschließend kommt die eigentliche Ausrichtung. Es sind prinzipiell die gleichen Werte wie bei justify-items möglich (nur dass es sich hier eben auf die vertikale anstatt die horizontale Ausrichtung bezieht). Also **items-start**, **items-center**, **items-end**, **items-strech** und **items-normal**.

Diese Klassen setzen das CSS Attribut **align-items**.

#### Individuelle Festlegung für die Positionierung eines einzelnen Items in der Zelle

#### einzelnes Item in der Zelle positionieren (horizontal)

Dazu verwendet man **justify-self-**. Es sind folgende Werte möglich:
- **justify-self-auto**: Es gilt die allgemeine Einstellung vom Container.
- **justify-self-start**: Dieses Item wird am Anfang der Zelle positioniert.
- **justify-self-center**: Dieses Item wird zentriert in der Mitte der Zelle positioniert.
- **justify-self-end**: Dieses Item wird am Ende der Zelle positioniert.
- **justify-self-strech**: Dieses Item nimmt die gesamte Breite der Zelle ein.

Diese Klassen setzen das CSS-Attribut **justify-self**.

#### einzelnes Item in der Zelle positionieren (vertikal)

Dazu verwendet man **self-**. Daran anschließend kommt wieder die Ausrichtung. Es sind prinzipiell die gleichen Werte wie bei justify-self möglich (nur dass es sich hier eben auf die vertikale und nicht die horizontale Ausrichtung bezieht). Also **self-auto**, **self-start**, **self-center**, **self-end**,  **self-strech**.

Diese Klassen setzen das CSS-Attribut **align-self**.

## Abkürzung, wenn man horizontal und vertikal gleich haben will

In diesem Fall kann man einfach **justify-** durch **place-** ersetzen. Achtung: Die Klassen justify- (für die grundlegende Ausrichtung der Zellen innerhalb der Zeile bzw. Spalte) werden durch **place-content-** ersetzt.

# Offizielle Doku von TailwindCSS

[Tailwind CSS Doku](https://tailwindcss.com/docs/display#grid)

