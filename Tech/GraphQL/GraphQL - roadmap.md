#graphql #roadmap #learning 
# Objectif de la roadmap
Idéalement avec cette roadmap on veut minimalement être opérationnel professionnellement. Même si on ne pourra pas se vendre comme "expert" ou senior, l'idée est d'être assez _alléchant_ pour se démarquer et qu'un client nous choisisse.

On s'attend donc à avoir
- une certaine autonomie sur la techno'
- des facilités à rentrer dans un projet client en place

# Documentation officielle

La [documentation officielle](https://graphql.org/learn/) est un très bon point d'entrée pour l'apprentissage de GraphQL.
Elle permet d'introduire les fondametaux tout en mettant un pied dans les best-practices.
> [!warning]
> Cette documentation reste très théorique, nous ne sommes pas ici sur un tutoriel ni même prise en main, mais plus sur un _cours_ sur GraphQL.

Avant de se jeter sur du hands-on, il peut être pertinent de regarder du côté [Apollo Odyssey](https://www.apollographql.com/tutorials/) 

> [!tip]
> Après chaque série de cours / tutoriel, il est possible de passer un examen afin d'être "certifié". Même si ce n'est pas une énorme certification comme celles des cloud providers, ceci permet de valider les acquis.

Si jamais on préfère aller plus sur un format vidéo, celle de Hussein Nasser peut être une bonne porte d'entrée. Elle reste aussi pertinente pour avoir un petit _pros / cons_.
<div class=iframe-container>
<iframe width="560" height="315" src="https://www.youtube.com/embed/fVmQCnQ_EPs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

# Hands-On
## Beginner-friendly 👶
Pour basculer tranquillement vers du hands-on, on peut se rendre vers [How to GraphQL](https://www.howtographql.com/) qui après avoir refait un petit tours théorique nous amène vers de vrais _hands-on_ 
On peut passer par:
1. typescript-apollo
2. React + Apollo 
3. node-typescript-helix 

## Practising 🐱‍🏍

Après avoir fait les premier pas, on peut explorer avec [NestJS](https://nestjs.com/) qui est un backend en Javascript / Typescript avec tout une documentation faisant usage de GraphQL.
Ici on parle uniquement de backend, donc il va falloir utiliser des outils comme [GraphiQL](https://github.com/graphql/graphiql) afin de pouvoir exploiter le backend que l'on produit. Postman devrait quand même aussi faire l'affaire, on a juste un environnement un peu moins "complet".

De la pratique avec une stack complète avec [One Week GraphQL](https://oneweekgraphql.com/). Avantage d'être un _cours_ de bout en bout, à la fois un inconvénient car pas forcément focus uniquement sur GraphQL.

Si jamais on préfère être complètement en exploratoire, il est possible de se tourner vers un framework comme [RedwoodJS](https://redwoodjs.com/). C'est un framework donc ce sera à nous de déterminer le use-case que l'on veut couvrir pour faire notre apprentissage.

Pour se focus principalement sur le frontend et la partie client on peut se tourner vers le repository [graphql-apis](https://github.com/IvanGoncharov/graphql-apis) qui regroupe un ensemble d'API GraphQL publique. 

# Approfondir

[The guild](https://the-guild.dev/) qui regroupe beaucoup d'outils, d'articles, de guides etc...

[Academy de Hygraph](https://hygraph.com/academy) qui permet de s'interesser plutôt du côté du domaine e-commerce, headless CMS etc...

Sur l'aspect testing, on va l'avoir vu (normalement) au travers des apprentissages précédents, il y a aussi diverses ressources comme:
- [Best practices for testing GraphQL APIs](https://fauna.com/blog/best-practices-testing-graphql-apis)
- [Testing, by The Guild](https://the-guild.dev/graphql/modules/docs/essentials/testing)
Ou encore le produit [Escape](https://escape.tech/) dont le focus principal est la partie sécurité / tester la sécurité de son API GraphQL. Par contre ne semble pas gratuit en dehors de leur middleware GraphQL Armor.

Enfin sur des sujets plus divers, on pourra se tourner vers des talks issus de la [GraphQL conf](https://www.youtube.com/playlist?list=PL5SvzogSTpeFmfihbyL7RaX1DiHTbFELx)

# Production grade 🚀

Pour la génération de documentation, un premier outil à regarder serait [Magidoc](https://magidoc.js.org) #librarie 

Il peut être aussi interessant de se tourner vers des use-case studies disponibles à diverses places comme:
- Le [site officiel de GraphQL](https://www.graphql.com/case-studies/)
- [GraphQL Schema Design at scale](https://www.youtube.com/watch?v=pJamhW2xPYw) par Marc-André Giroux 
- L'article [Scaling GrphQL adoption at Netflix](https://www.infoq.com/news/2022/10/scaling-graphql-netflix/) issu de la QCon de San Francisco. D'ailleurs en restant du côté Netflix il y a aussi ces deux articles:
	- [How Netflix Scales its API with GraphQL Federation (Part 1)](https://netflixtechblog.com/how-netflix-scales-its-api-with-graphql-federation-part-1-ae3557c187e2)
	- [How Netflix Scales its API with GraphQL Federation (Part 2](https://netflixtechblog.com/how-netflix-scales-its-api-with-graphql-federation-part-2-bbe71aaec44a)

Le livre [Production ready GraphQL](https://book.productionreadygraphql.com/) semble être une valeur assez sûre car produit par [Marc-André Giroux](https://twitter.com/__xuorig__) qui semble avoir une certaine notoriété dans le milieu GraphQL. Le livre et package payant mais pas extrêmement cher (49$)



# Se maintenir 🧐
- [GraphQL.wtf](https://graphql.wtf/) _Learn something new with GraphQL, every week._ #newsletter
- [GraphQL weekly](https://www.graphqlweekly.com/) _A weekly newsletter of the best **news**, **articles** and **projects** about GraphQL_ #newsletter 