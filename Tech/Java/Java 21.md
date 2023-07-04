#java 
Prévue pour le 19 septembre 2023

## Pattern-matching switch 🚀
Va permettre de ne plus avoir besoin de cast une variable dont on vient de vérifier le type.
Par exemple:
```java
static String formatterPatternSwitch(Object obj) {
    return switch (obj) {
        case Integer i -> String.format("int %d", i);
        case Long l    -> String.format("long %d", l);
        case Double d  -> String.format("double %f", d);
        case String s  -> String.format("String %s", s);
        default        -> obj.toString();
    };
}
```

## Record Patterns 👍
Viens un peu comme une extension du pattern-matching, dans le coin des *records* pour entre autre permettre des *data-queries* plus composables.

De manière simple on va avoir
```java
static void printSum(Object obj) {
    if (obj instanceof Point(int x, int y)) {
        System.out.println(x+y);
    }
}
```
Dans cet exemple, la partie `Point(int x, int y)` est ce que l'on appelle le *record pattern*.

Pour l'aspect composition, on peut voir cet exemple dans lequel on peut voir la composition de `Point`, `ColoredPoint` pour enfin avoir un `Rectangle`.
```java
static void printColorOfUpperLeftPoint(Rectangle r) {
    if (r instanceof Rectangle(ColoredPoint(Point p, Color c),
                               ColoredPoint lr)) {
        System.out.println(c);
    }
}
```

Là où le lien se fait avec le pattern-matching sur switch, c'est sur le fait que le switch doit être exhaustif dans les *case* qu'il gère.

## Sequence collections
Permet d'avoir des types qui décrivent plus précisément des collections dont l'ordre importe, comme dans une séquence.
On se retrouve avec `SequenceSet`, `SequenceCollection`, `SequencedMap`. On peut voir comment ça s'inscrit dans les collections en terme de hiérarchie:
![[o6fsrrha.bmp]]

## Virtual threads
Va permettre de faire des threads *legers* de manières simples. Beaucoup font le rapprochement avec les coroutines de Kotlin.
Le détail est disponible dans la [JEP-444](https://openjdk.org/jeps/444)

En points mis en avant:
- possibilité de faire des variables locales au thread (surtout là pour les librairies / codes existants)
- pouvoir les utiliser en *thread-per-request style*

Pour un focus plus prononcé, aller sur [[Virtual threads]]
