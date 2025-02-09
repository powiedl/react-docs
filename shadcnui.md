# shadcn/ui

shadcn/ui ist eine CSS Bibliothek, die auf Tailwind basiert. Sie bietet Komponenten, die von Haus aus schon recht schön gestyled sind. Damit kann ein Nachteil, der bei der Verwendung von Tailwind (ein Element hat sehr viele Klassen, damit es "richtig" gestyled ist) oft auftritt, reduziert werden. Außerdem verfolgt shadcn/ui zwei weitere (interessante) Ansätze. Zum einen erhält man den gesamten Sourcecode der verwendeten Komponenten direkt im "normalen" Bereich seiner Applikation (/src) und zum anderen kann man die Komponenten einzeln installieren, d. h. man installiert nur die Komponenten, die man auch tatsächlich verwendet.

## Tipps und Tricks

### Button mit einer SVG-Grafik (beispielsweise durch ein react-icon)

Will man bei einem Button die Größe der SVG-Grafik anpassen, kann man die size nicht direkt am Icon setzen, weil shadcn/ui die Size bereits am Button vorgibt. Man muss daher ebenfalls den Button stylen. Das erreicht man so: `className='[&_svg]:size-8'` (Standard ist size-4).

### Varianten für eigene Komponenten erstellen

Mit shadcn/ui kann man relativ leicht auch für eigene Komponenten varianten erstellen. Dazu bringt shadcn/ui eine Utilityfunktion cva mit. Diese hat zwei Parameter:
1. Defaultklassen:string : Diese Klassen gelten für alle Varianten (und können auch nur ein leerer String sein, dann haben die Varianten nichts miteinander gemein)
2. Varianten:{variants:object;defaultVariants?:object}: Dieses Objekt hat ein Attribut variants, wo die einzelnen Varianten definiert sind und optional ein Attribut defaultVariants (dort kann man pro festgelegter Variante einen Default festlegen)

Am einfachsten ist es verständlich, wenn man sich ein Beispiel ansieht:

```
const avatarVariants = cva("",{
  variants:{
    size: {
      default:"h-9 w-9",
      xs:"h-4 w-4",
      sm:"h-6 w-6",
      lg:"h-10 w-10",
      xl:"h-[160px] w-[160px]"
    },
  },
  defaultVariants: {
    size:"default"
  }
});
```

Damit definiert man eine Variante `size`. Diese kann die Werte `default`, `xs`, `sm`, `lg` und `xl` annehmen. Wenn man bei der Verwendung dann keine `size` angibt, werden die Einstellungen, die bei `default` hinterlegt sind, genommen.

Dann kann man für seine Komponente ein Interface für die Props definieren (welches VariantProps) erweitert:

```
interface UserAvatarProps extends VariantProps<typeof avatarVariants> {
  imageUrl: string;
  name: string;
  className?: string;
}
```

Und zum Schluss definiert man die Komponente, deren Props vom Typ des erstellten Interfaces sind (und dann hat man in der Komponente Zugriff auf die Attribute der variants):

```
export const UserAvatar = ({ imageUrl,name,size,className } : UserAvatarPros) => {
 return (
    <Avatar className={cn(avatarVariants({ size, className }))}>
      <AvatarImage src={imageUrl} alt={name} />
    </Avatar>
  );
}
```

