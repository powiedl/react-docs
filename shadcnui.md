# shadcn/ui

shadcn/ui ist eine CSS Bibliothek, die auf Tailwind basiert. Sie bietet Komponenten, die von Haus aus schon recht schön gestyled sind. Damit kann ein Nachteil, der bei der Verwendung von Tailwind (ein Element hat sehr viele Klassen, damit es "richtig" gestyled ist) oft auftritt, reduziert werden. Außerdem verfolgt shadcn/ui zwei weitere (interessante) Ansätze. Zum einen erhält man den gesamten Sourcecode der verwendeten Komponenten direkt im "normalen" Bereich seiner Applikation (/src) und zum anderen kann man die Komponenten einzeln installieren, d. h. man installiert nur die Komponenten, die man auch tatsächlich verwendet.

## Tipps und Tricks

### Button mit einer SVG-Grafik (beispielsweise durch ein react-icon)

Will man bei einem Button die Größe der SVG-Grafik anpassen, kann man die size nicht direkt am Icon setzen, weil shadcn/ui die Size bereits am Button vorgibt. Man muss daher ebenfalls den Button stylen. Das erreicht man so: `className='[&_svg]:size-8'` (Standard ist size-4).
