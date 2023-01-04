#newsletter #graphql

[Site officiel](https://graphql.org/)
[Spécification officielle](https://github.com/graphql/graphql-spec) 🚩pas forcément pertinent de se jeter dedans `The target audience for this specification [...] those who have, or are actively interested in, building their own GraphQL implementations and tools.`

Information | Lien| Notes
--------------|----|---------
Documentation officielle | https://graphql.org/learn/ | Pas mal fournie, termine sur lest best-practices
Multiples liens de la communauté | https://graphql.org/community/ | Ramène vers Discord, Github etc...

La documentation officielle recommende également un "Database" explorer: [GraphiQL](https://github.com/graphql/graphiql)

La documentation officielle référence aussi quelques formations faites par d'autres, des blogs, des vidéos, en voici quelques notables (le tout regroupé [par ici](https://graphql.org/community/users/)):
- 👓 [The Fullstack Tutorial for GraphQL](https://www.howtographql.com/): semble amener un complément à la documentation officielle 
  - se décrit elle même en The free and open-source tutorial to learn all around GraphQL to go from zero to production.
  - Faite par les gens de chez [Prisma](https://www.prisma.io/)
- 👓 [Apollo Odyssey](https://www.apollographql.com/tutorials/): permet si suivi au complet d'être certifié **Graph Developer - Professional**
- 📚 En terme de livre, ils sont presque tous payants, et ceux en gratuit semble _legers_ par rapport à des tutoriaux / formations en ligne gratuit. Peut-être quelques exceptions comme [Production ready GraphQL](https://book.productionreadygraphql.com/) après avoir _épuisé_ les ressources gratuites
- 😎 [awesome-graphql](https://github.com/chentsulin/awesome-graphql) comme tous les repo' _awesome_ énormément de ressources référencées


De manière générale GraphQL est très très orienté Javascript / Typescript. Même s'il n'y a pas de limitation particulière aux autres technos' c'est quand même la majorité des outils, librairies etc... surement du fait que c'est _pensé_ pour le frontend.

À la suite de ce document on va trouver divers liens, vers divers outils, ressources etc... Pour un apprentissage, plutôt se tourner vers [[GraphQL - roadmap]]


---
## Divers outils 🛠, liens 🌎...

### Prisma
[Site officiel](https://www.prisma.io/) _Next-generation **Node.js** and **TypeScript** ORM_
La partie [blog](https://www.prisma.io/blog) est assez fournie, par contre très orientée sur Prisma. Il y a quand même de quoi à en retirer notamment dans la partie _hands-on_ comme avec Redwood etc... en commençant la série [Fullstack App With TypeScript, PostgreSQL, Next.js, Prisma & GraphQL](https://www.prisma.io/blog/fullstack-nextjs-graphql-prisma-oklidw1rhw) #learning même si le combo avec PostgreSQL... 🤔


### Apollo
[Site officiel](https://www.apollographql.com/)

### GraphQL.wtf 
#newsletter 
[Site officiel](https://graphql.wtf/) _Learn something new with GraphQL, every week._

### GraphQL weekly
#newsletter 
[Site officiel](https://www.graphqlweekly.com/) _A weekly newsletter of the best **news**, **articles** and **projects** about GraphQL_

### TypeGraphQL
#framework
[Site officiel](https://typegraphql.com/) _Modern framework for GraphQL API in Node.js_

### NestJS
#framework 
[Documentation pour GraphQL](https://docs.nestjs.com/graphql/quick-start#getting-started-with-graphql--typescript)
Ce n'est pas un framework spécialement dédié à GraphQL, mais quand même répandu dans le monde _entreprise_ donc à prendre en considération.

### Magidoc
#librarie
[Site officiel](https://github.com/magidoc-org/magidoc) _Fast and customizable GraphQL documentation generator_

### Hasura
[Site officiel](https://hasura.io/) 
[GraphQL engine](https://github.com/hasura/graphql-engine) est open-source et semble assez fourni en terme de features. Son pitch est: _Blazing fast, instant realtime GraphQL APIs on your DB with fine grained access control, also trigger webhooks on database events._

### The guild
#learning 
[Site officiel](https://the-guild.dev/) _Modern API Platform and ecosystem that scales_
Fourni pas mal de ressources que ce soit en documentations, librairies, services ou encore liens vers d'autres sites et news interesantes.
La partie _at scale_ semble interessante même si pas spécialement la plus riche en informations (au premier abord).

### Hussein Nasser
#learning 
Pas dédié au sujet GraphQL, il amène par contre des informations et analyses poussées. [Plusieurs vidéos](https://www.youtube.com/c/HusseinNasser-software-engineering/search?query=graphql) sur le sujet GraphQL sont notables:
- [Un crash course d'environ 1h](https://www.youtube.com/watch?v=fVmQCnQ_EPs)
- [When to use GraphQL over REST](https://www.youtube.com/watch?v=J5NkUQ7XRYA)
- [The problem with error management in GraphQL](https://www.youtube.com/watch?v=EjTFlaFSwro) #error-management
- [Une analyse sur le cas Instagram](https://www.youtube.com/watch?v=rjZpGc9xWlM)

### RedwoodJS
#framework 
[Site officiel](https://redwoodjs.com/) _Redwood is the full-stack web framework designed to help you grow from side project to startup._
Pas hyper répandu dans l'industrie, par contre amène un package complet quand on veut faire une app' en utilisant notamment GraphQL. Au niveau des tech' on est sur [React](https://reactjs.org/) / [GraphQL](https://graphql.org/) / [Prisma](https://www.prisma.io/) / [TypeScript](https://www.typescriptlang.org/) / [Jest](https://jestjs.io/) / [Storybook](https://storybook.js.org/)

### Escape
#learning
[Site offciel])(https://escape.tech/) _Dynamic GraphQL API Security Testing_
Pour l'apprentissage ils ont fait une bonne page [Learning GraphQL Roadmap: 8 Steps to Master GraphQL](https://escape.tech/blog/learning-graphql-roadmap-8-steps-to-master-graphql/) a surement se baser pour ma roadmap (car reste très très léger / succinte dans son approche)
À lire surement aussi: [GraphQL Cyclic Queries and Depth Limiting](https://escape.tech/blog/cyclic-queries-and-depth-limit/)

### Aista - Blog post
#controversial
[GraphQL is a hot smoking pile of garbage](https://aista.com/blog/graphql-is-hot-smoking-pile-of-garbage/)

### One week GraphQL
#learning 
[Site officiel](https://oneweekgraphql.com/) _Build a fullstack eCommerce application with GraphQL Yoga, Prisma, Planetscale, Next.js, Tailwind CSS, & Stripe Checkout._
Complètement gratuit, surement à approcher dans la phase après les premiers apprentissage quand on va chercher à produire de quoi de concret.

### Pothos
#librarie #plugin
[Site officiel](https://pothos-graphql.dev/) Tooling pour construire des schémas GraphQL de manière _type-safe_
Sans rien y connaitre on se demande un peu à quoi ça peut servir face à des chose comme Prisma, TypeGraphQL etc...

### WunderGraph
[Site officiel](https://wundergraph.com/)
Ce qui est peut-être plus interessant c'est du côté article comme [Analyzing public GraphQL APIs #1: Twitch.tv](https://wundergraph.com/blog/graphql_in_production_analyzing_public_graphql_apis_1_twitch_tv) #learning #production. D'autres sont bien sûr disponibles sur leur partie [blog](https://wundergraph.com/blog).

### GraphQL rules
[Site officiel](https://graphql-rules.com/)
Un petit site qui regroupe un ensemble de _best-practices_ à tenir lorsque l'on fait du GraphQL. Assez léger et pas hyper maintenu malheuresement 😥

### Spring for GraphQL
[Documentation de référence](https://docs.spring.io/spring-graphql/docs/current/reference/html/)
Par contre ça semble encore assez _jeune_, on est sur une version 1.0, avec peu d'exemples (qui en plus vont être déplacés...) à voir si ça vaut le coup de s'y pencher quand toute l'industrie fait majoritairement du GraphQL en Javascript / Typescript.
Même chose du côté de [microprofile-graphql](https://github.com/eclipse/microprofile-graphql/) qui semble encore très jeune aussi

### Stepzen
[Site officiel](https://stepzen.com/)
[Blog](https://stepzen.com/blog) qui contient quelques articles potentiellement interessants comme par exemple [# GraphQL Architecture Master Class](https://stepzen.com/blog/graphql-masterclass-build-faster-run-better) qui donne un bon point de sortie vers d'autres articles.

### Podcast Mirego
[Elixir et GraphQL](https://anchor.fm/mirego/episodes/Elixir-et-GraphQL-e1842oc/a-a6k74h3)
Ce n'est que le second épisode fait par Mirego donc il essui un peu les platres, mais ça reste un échange interessant.

### Roadmap.sh
Elle était manquante jusqu'à tout récemment, la voici enfin [ici](https://roadmap.sh/graphql).
Par contre, elle est entièrement vide en terme de liens. Ce n'est pour l'instant qu'une représentation graphique. Ça ne vaut donc pas spécialement le coup de s'y attarder quand la documentation officielle trace déjà un chemin _de base_.

### GraphQL Conf'
#talk
[Site officiel](https://graphqlconf.org/)
Comme toutes les conférences de langage, framework etc... les divers talks sont assez peu orientés "beginner-friendly". Il y a [une playlist](https://www.youtube.com/playlist?list=PL5SvzogSTpeFmfihbyL7RaX1DiHTbFELx) qui regroupe l'ensemble des talks qui ont été donnés.
Un talk qui attire l'oeil sans (sembler) être focus sur GraphQL uniquement est [The rise of Backendless](https://www.youtube.com/watch?v=KRtk2__MGAI&list=PL5SvzogSTpeFmfihbyL7RaX1DiHTbFELx&index=5)

### GraphQL Summit
#talk 
[GraphQL Summit 2021](https://www.youtube.com/playlist?list=PLpi1lPB6opQy2nbiaJTv8KsZbwSGP5g71)

### Hygraph
[Site officiel](https://hygraph.com/) _The Federated Content Platform_
Plateforme qui semble interessante quand on traite le sujet de la gestion de contenu (à priori pas seulement e-commerce). Au niveau pricing on est sur du gratuit en mode _Community_ et ressemble à un mode SaaS (<-- à confirmer).

Ils ont une section [Academy](https://hygraph.com/academy) qui regroupent des articles d'apprentissage #learning . Certains sont courts par contre certains sont bien fournis comme [What is a Knowledge Base?](https://hygraph.com/academy/what-is-a-knowledge-base). Pas d'article sur la partie #production par contre 😥

### Hodovoci (article)
[CI/CD for Apollo GraphQL Managed Federation](https://hodovi.cc/blog/ci-cd-for-apollo-graphql-managed-federation/)