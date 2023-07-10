#youtube

# 📃 Playlists
- [Édition 2023](https://www.youtube.com/playlist?list=PLz7aCyCbFOu-5OE0ajDUVjlqBFq1y9XiQ)

***

# 👀 ToWatch

| Titre | Tags | Priorité | Lien | Watched |
| ----- | ---- | -------- | ---- | :-------: |
| Apache Kafka : Tips & Tricks que j'aurais aimé connaître plus tôt.. | #kafka | Haute | [Lien](https://www.youtube.com/watch?v=ojlnNl-pzb8) | ✅ |
| Programmation Concurrente et Asynchrone : Loom en Java 20 et 21 | #loom #virtual-threads #java  | Haute | [Lien](https://www.youtube.com/watch?v=OPV8GIdnQto) | ✅ |
| Secret Story pour faire sa veille et apprendre efficacement | #veille | Moyenne | [Lien](https://www.youtube.com/watch?v=4OJgkQZwMmg) | ❌ |
| The next generation of Angular Application | #angular #frontend | Moyenne | [Lien](https://www.youtube.com/watch?v=50Gjdi72xd4) | ❌ |
| Example Mapping: expliquer facilement les attentes du métier à vos équipes | #soft-skills | Moyenne | [Lien](https://www.youtube.com/watch?v=57g1ocHZqt0) | ❌ |
| Comment économiser 80% de temps de CI avec PNPM | #frontend #ci | Moyenne | [Lien](https://www.youtube.com/watch?v=zKMt2i5L8ME) | ❌ |
| A Pragmatic Data Stack | #data | Moyenne | [Lien](https://www.youtube.com/watch?v=O_nNRIquYTg) | ❌ |
| CodeCarbon : Comment mesurer l’impact CO2 de vos projets? | #écologie | Basse | [Lien](https://www.youtube.com/watch?v=GxwEa7wydWI) | ❌ |
| SwiftUI vs Jetpack Compose par un Ingénieur Android | #mobile #jetpack-compose #android | Basse | [Lien](https://www.youtube.com/watch?v=EZeycvVbIVQ) | ❌ |

***

# ✅ Watched

## [Apache Kafka : Tips & Tricks que j'aurais aimé connaître plus tôt..](https://www.youtube.com/watch?v=ojlnNl-pzb8)

- Ne pas autoriser la création automatique de topic (à contrebalancer avec la potentielle utilisation de proxy dispo' dans [[Tech/Conferences/Devoxx 2023/WatchList|WatchList]])
- Attention sur le hash de clé, ce n'est pas forcément le même algorithme de hash d'un langage à un autre. Pour faire safe: forcer le même algorithme pour tout le monde.
- Ne pas se baser fortement sur la compaction de topic, par exemple ne pas l'utiliser comme logique déterministe pour supprimer de vieux doublons.
- Sur le nombre de partition, vis à vis de la notion de *divisibilité* les chiffres qui reviennent souvent: `6 / 12 / 24 / 48 / 60 / 120 / 180 / 240 / 360` 
- Importance du schéma, contrat entre Producer et Consumer: utiliser un schema-registry
- Mieux vaut mettre à jour les consumers avant les producers
- Avoir le réflexe d'utiliser les JMX pour débugger une situation.
- La compression a lieu sur les batch: pas de batch == pas de compression
- Pour les tests de performances, mieux vaut se baser sur le traffic de production, et le comportement de la production. Par exemple, en production on ne produit pas les messages dans une logique *round-robbin*.