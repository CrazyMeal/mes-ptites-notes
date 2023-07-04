#java 
Pas spécialement beaucoup de feature *importante* il y a notamment plusieurs choses qui passent en incubator.
Le rythme de LTS passe à 3 ans; nouvelle approche de release / LTS.
[Release note](https://www.oracle.com/java/technologies/javase/17-relnote-issues.html)

# Features

## Sealed class 🚀
Donne plus de contrôle sur les héritages / implémentations. Très pratique notamment si on fait des librairies et que l'on *opiniate* celle-ci.
Plus de détails sur la [JEP 409](https://openjdk.org/jeps/409).

## Record 🚀
Amené en fait avec Java 14

## Context-Specific Deserialization Filters 👍
Amène un moyen de rendre plus sécuritaire la désérialisation de données par l'utilisation de filtre(s).
Il y a un article officiel dédié dans la [documentation de Core Librairies](https://docs.oracle.com/en/java/javase/17/core/serialization-filtering1.html).

On peut appliquer des filtres de manière *wide-JVM* donc pour toute désérialisation qui survient, mais aussi des filtres plus spécifiques, plus focus sur le traitement d'un stream en particulier.
Les filtres peuvent gérer différents aspects:
- allow-lists / reject-lists
- des filtres basés sur les patterns
Même s'il y a des filtres déjà built-in, il est conseillé de spécifier les filtres que l'on veut appliquer (surtout qu'ils sont surtout là pour l'utilisation de RMI).

## Floating-Point Semantics 💤
À voir selon les contextes quand on fait des opération mathématiques. Semble quand même très pointu comme modification mais à garder dans un coin de tête, au cas où comme par exemple dans un contexte de développement de librairie existante (ou pas forcément ?) qui va faire pas mal d'opération mathématiques variées.
Par opération mathématique on évoque ici `java.lang.Math` et `java.lang.StrictMath`.