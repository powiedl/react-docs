# Tailwind Grid

Ein Grid besteht aus dem Grid-Container und den Grid-Items. Ein Grid ist immer zweidimensional (auch wenn es vielleicht nur eine Spalte oder eine Zeile ist). 

## Begriffsdefinitionen

Ein Grid besteht aus den **Zellen**. Diese sind im zwei Dimensionalen Raster angeordnet. Die Zellen sind der "Platz" wo dann die Grid Items platziert werden. Im Standardfall belegt ein Item genau eine Zelle.

Die Zeilen werden als **row track**, die Spalten als **column track** bezeichnet.

Die tracks werden von den lines umschlossen, jeder einzelne Track hat dabei eine Beginnline und eine Endline. Die End- und die Beginnline von benachbarten tracks fällt dabei zusammen, darum gibt es immer genau eine Line mehr wie es tracks gibt. Die Lines werden (wie auch die Tracks von links nach rechts bzw. von oben nach unten nummeriert und die Nummerierung startet mit 1). In der gegenläufigen Richtung (also z. b. von rechts nach links wird mit -1 zu zählen begonnen und dann immer um eins erniedrigt). Damit kann man auch "die letzte" oder "die vorletzte" line ansprechen. Außderm kann man lines auch Namen geben.

Wenn man bei der Definition die Zeilen und Spalten festlegt ist dieser Teil des Grids ein **explizites Grid**. Außerdem gibt es bei einem Grid immer eine "Wachstumsrichtung" (kommt eine neue Spalte oder eine neue Zeile dazu, wenn für ein neues Item kein Platz mehr ist). Dieser Teil (der nicht von vornherein definierte ist) wird als **implizites Grid** bezeichnet. Nachdem das Grid erzeugt ist, gibt es aber keinen Unterschied zwischen den beiden Teilen und aus dem Browser kann man auch nicht erkennen, welcher Teil was ist.

Mit Grid wurde auch eine neue Einheit eingeführt **1fr** (fraction). Dabei handelt es sich "um einen Teil des verfügbaren Platzes".

## Eigenschaften für explizites Grid festlegen

### Anzahl der Spalten und Reihen festlegen

Dazu verwendet man die Klasse **grid-cols-** um die Anzahl der Spalten festzulegen. TailwindCSS bietet 1 bis 12 standardmäßig an (z. b. `grid-cols-3` für 3 Spalten), darüber hinaus muss man die `[ ]` verwenden. Die Anzahl der Reihen legt man analog mit **grid-rows-** fest. Standardmäßig bietet TailwindCSS hier ebenfalls 1 bis 12 an (z. b. `grid-rows-7` für 7 Zeilen). 

In diesem Fall werden die Spalten alle gleich breit bzw. die Reihen alle gleich hoch. Will man unterschiedliche Größen für die einzelnen Spalten bzw. Reihen haben, muss man mit `[ ]` arbeiten. Siehe [Größe der Spalten und Reihen festlegen](#Größe der Spalten und Reihen festlegen).

## Eigenschaften für implizites Grid festlegen

Mit den Klassen **grid-flow-row** und **grid-flow-col** legt man fest, ob zusätzliche Zellen (wenn kein freier Platz mehr für neue Items im Grid existiert) zu einer zusätzlichen Reihe (das ist der Standard) oder zu einer neuen Spalte führen sollen. Für die Festlegung der Spaltenbreite bzw. Reihenhöhe des impliziten Grids verwendet man die Klassen **auto-cols-** und **auto-rows-**. Danach gibt man die Größe an. Dazu siehe [Größe der Spalten und Reihen festlegen](#Größe der Spalten und Reihen festlegen).

## Größe der Spalten und Reihen festlegen

Wie bereits festgestellt, muss man dazu auf `[ ]` "ausweichen". Darin gibt man die Größe der jeweiligen Spalten und Reihen an. Die einzelnen Angaben trennt man mit _ (weil sie in nativem CSS mit einem Leerzeichen zu trennen sind, Leerzeichen aber in `[ ]` durch _ ersetzt werden.

Im einfachsten Fall legt man die Größe der einzelnen Spalten bzw. Reihen mit entsprechenden Längenangaben fest (z. b. `50px`, `15%`, `2fr`). Man hat aber auch noch folgende zusätzliche Möglichkeiten:

- **min-content**: So klein wie möglich. Für Spalten bedeutet das im Normalfall, dass die Spalte so breit wird wie das längste Wort. Für Reihen bedeutet es, dass der Inhalt auf so wenig Zeilen wie möglich aufgeteilt wird.
- **max-content**: So groß wie notwendig. Für Spalten bedeutet das im Normalfall, dass die Spalte so breit wird wie der gesamte Inhalt - sofern für die Spalte prinzipiell so viel Platz möglich ist.

Außerdem kann man die Funktion **minmax** verwenden. Diese erwartet zwei Parameter (wobei der erste kleiner wie der zweite sein muss) und kümmert sich dann darum dass die Dimension, wo die Funktion verwendet wird immer im Bereich zwischen den beiden Parametern ist.

Wenn man jetzt ein "Muster" wiederholen will (z. b. immer eine kleine Spalte/Reihe gefolgt von einer großen) kann man die Funktion **repeat** verwenden. Diese hat zwei Parameter. Zuerst die Anzahl der Wiederholungen und dann was wiederholt werden soll, z. b. `repeat(2,50px_max-content)`. Das erzeugt diesen String: `50px_max-content_50px_max-content`.

Für den impliziten Teil gibt es noch folgende "Sonderfälle" (wenn alle impliziten Reihen / Spalten gleich groß sein sollen):
- **auto-...-min** - es wird min-content verwendet
- **auto-...-max** - es wird max-content verwendet
- **auto-...-auto** - es wird sehr ähnlich (oft gleich) wie minmax(min-content,max-content) enden. Ein Sonderfall ist, dass es eine Größe von auto der Reihe / Spalte erlaubt "beliebig" zu wachsen (so wie Größen der Einheit **fr**)

**Beispiele**:
- `grid-cols-[repeat(2,50px_max-content)]` führt zu diesem CSS: `grid-template-cols: repeat(2,50px max-content)`
- `grid-rows-[min-content_max-content]` führt zu diesem CSS: `grid-tempate-rows: min-content_max-content`
- `auto-cols-[50px_100px_150px]` führt zu diesem CSS: `grid-auto-columns: 50px 100px 150px`
- `auto-rows-min` führt zu diesem CSS: 'grid-auto-rows: min-content`

### Explizites Grid - Zellengröße festlegen

Das geht über **grid-rows-** bzw. **grid-cols-**. In diesem Fall gibt man nicht die 

### Implizites Grid - Zellengröße festlegen

## Items im Grid platzieren

Die Items werden "der Reihe nach" (so wie sie im HTML definiert sind) im Grid platziert. Man kann sowohl die Position als auch die Größe der Items definieren. Wenn dadurch Lücken entstehen werden die von nachfolgenden Items nicht automatisch gefüllt. Man kann diese aber durch entsprechende Platzierungsanweiungen in die Lücken geben.

### Items entlang der Spalten platzieren

Dafür gibt es die Klassen **col-start** und **col-end** und man gibt jeweils die Row Line an, an der das Item beginnt bzw. endet. Außerdem gibt es noch **col-span** - damit definiert man wie viele Zellen Breite das Item haben soll (natürlich sollte man nur zwei der drei Klassen verwenden). Wenn man alle drei verwendet gelten die letzten beiden. Bei col-span gibt es noch den Spezialfall **col-span-full** (damit erstreckt sich das Item über eine ganze Zeile).

### Items entlang der Zeilen platzieren

Analog dazu gibt es die **row-start** und **row-end** Klassen. Damit kann man ein Element auch außerhalb der Reihenfolge im HTML platzieren. Und auch hier gibt es **row-span-full** womit das Item eine ganze Spalte belegt.

## Zellen im Grid positionieren

Wenn das Grid in der Dimension größer als die Summe der Größe aller Items in der Dimension ist (es also im Grid ungenutzten Platz in dieser Dimension gibt) kann man festlegen wie die einzelnen Zellen verteilt werden. Das kann nur der Fall sein, wenn keine Zelle in der Dimension eine Größe mit der Einheit **fr** hat (weil die Zellen mit einer Größe in **fr** teilen sich den ungenutzten Platz untereinander auf). Dabei muss man die Ausrichtung in Zeilen und Spalten unterscheiden.

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

Diese Klassen setzen das CSS Attribut *justify-content*.

### Zellen in Spalten im Grid positionieren (vertikal)

Dazu verwendet man **content-**. Daran anschließend kommt die eigentliche Ausrichtung. Es sind prinzipiell die gleichen Werte wie bei justify möglich (nur dass es sich hier eben auf Spalten und nicht auch Zeilen bezieht). Also **content-start**, **content-center**, **content-end**, **content-between**, **content-around**, **content-stretch**, **content-evenly** und **content-normal**.

Diese Klassen setzen das CSS Attribut *algin-content*.

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

Diese Klassen setzen das CSS Attribut *justify-items*.

##### Vertikale Positionierung eines Items in der Zelle

Dazu verwendet man **items-**. Daran anschließend kommt die eigentliche Ausrichtung. Es sind prinzipiell die gleichen Werte wie bei justify-items möglich (nur dass es sich hier eben auf die vertikale anstatt die horizontale Ausrichtung bezieht). Also **items-start**, **items-center**, **items-end**, **items-strech** und **items-normal**.

Diese Klassen setzen das CSS Attribut *align-items*.

#### Individuelle Festlegung für die Positionierung eines einzelnen Items in der Zelle

#### einzelnes Item in der Zelle positionieren (horizontal)

Dazu verwendet man **justify-self-**. Es sind folgende Werte möglich:
- **justify-self-auto**: Es gilt die allgemeine Einstellung vom Container.
- **justify-self-start**: Dieses Item wird am Anfang der Zelle positioniert.
- **justify-self-center**: Dieses Item wird zentriert in der Mitte der Zelle positioniert.
- **justify-self-end**: Dieses Item wird am Ende der Zelle positioniert.
- **justify-self-strech**: Dieses Item nimmt die gesamte Breite der Zelle ein.

Diese Klassen setzen das CSS-Attribut *justify-self*.

#### einzelnes Item in der Zelle positionieren (vertikal)

Dazu verwendet man **self-**. Daran anschließend kommt wieder die Ausrichtung. Es sind prinzipiell die gleichen Werte wie bei justify-self möglich (nur dass es sich hier eben auf die vertikale und nicht die horizontale Ausrichtung bezieht). Also **self-auto**, **self-start**, **self-center**, **self-end**,  **self-strech**.

Diese Klassen setzen das CSS-Attribut *align-self*.

### Abkürzung, wenn man horizontal und vertikal gleich haben will

In diesem Fall kann man einfach **justify-** durch **place-** ersetzen. Achtung: Die Klassen justify- (für die grundlegende Ausrichtung der Zellen innerhalb der Zeile bzw. Spalte) werden durch **place-content-** ersetzt.

## Abstand zwischen Zellen im Grid

Dazu verwendet man **gap-**. Für den horizontalen Abstand verwendet man **gap-x-** (das setzt das CSS Attribut gap-column), für den vertikalen Abstand *gap-y-* (das setzt das CSS Attribut *gap-row*).

## Offizielle Doku von TailwindCSS

[Tailwind CSS Doku](https://tailwindcss.com/docs/display#grid)

