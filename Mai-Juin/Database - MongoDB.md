# Introduction 
Toutes les données stockées dans mongodb n'ont pas de contrainte de structure => plasticité des schéma. 

MongoDB est fait pour êtres très performant avec beaucoup de données
## Vocabulaire

### Schema
### Index
permet d’accélérer le processus de recherche de donnes dans une base de données.
Pratique quand on a beaucoup de données.

### format JSON
=> JavaScript Object Notation (format d'échange de données)
=> format universel très répandu 
L'unité de stockage en MDB est le document.
=> notion de collection et de document

### Collection 
Groupe de documents MDB 
+ sans schema précis
+ documents au seins d'une même collection peuvent avoir des champs différents => tous les docs d’une collection sont généralement similaire avec des usages similaires

### Documents
Ensemble de données clé-valeur
Le schéma des documents est dit "dynamique"


## MongoDB & RDBMS

```
| RDBMS       | MongoDB            |
| ----------- | ------------------ |
| Table       | Collection         |
| Row         | JSON Document      | 
| Index       | Index              |
| Join        | Embedding & Linking|
| Partition   | Shard              |
```
## Types de données

Nativement format JSON accepte: 
- booléen
- numérique
- chaîne de caractères
- tableau 
- objet
- null

Mongo va ajouter : 
- type Date : stocke sous la forme d'un entier signe de 8octets (forcément positif) qui représente le nombre de seconde écoulées depuis l'époque (epoch) unix : le 1er janvier 1970 à minuit.
- type ObjectId : un type interne   utilisé par MongoDB pour garantir l'unicité des identifiants générés par la base de données
- les types entiers NumberLong (8 ocets) et NumberInt (4 octets): par défaut, MDB considère que les nombres sont des nombres à virgules flottantes
- le type NumberDecimal (16 octets) : nombre à virgule flottante de grande précision 

BSON (format JSON a la sauce de mongoDB) : https://www.mongodb.com/docs/manual/reference/bson-types/

## Command lines + link docs
Utiliser mongodb en ligne de commande : 
```bash
mongod --port 27017 --dpath /data/db --logpath /tmp/mongodb 
--logappend
```

Se connecter en ligne de cmd 
```bash
mongo --host lien.moncluster.fr --port 27017
```

En général, après une installation fraîche de mongodb vous avez 3 bases disponibles : 
`admin`, `config`, `local`

Elles servent à gérer les rôles, es autorisations, la gestion de MongoDB, du paramétrage d'instance

Pour savoir sur quelle base de données on se trouve actuellement il suffit de taper la commade `db`, pour lister les collections presentes dans votre bases vous pouvez enter : `show collections`

Pour switcher de base on utilise la commande . `use maDb`

On peut utiliser use afin de se connecter a une base inexistante, c'est lorsque vous insererez votre premier document dans une collection de cette base qu'elle sera cree : 
```
use maBaseDeDonnee
db.maCollection.insert({"une_cle" : "une valeur"})
```

```
db.maCollection.find()

{
	"_id" : ObjectId("..."),
	"une_cle" : "une valeur"
}
```

L'insertion de document se fait comme ceci : 
`db.collection.insert(<document ou un tableau>)`

### application
- Pour filter la requête (sommaire) : https://www.mongodb.com/docs/manual/reference/operator/query/ 
- Pour retourner que certain champs (les champs indiqués et l'id): 
```
db.collection.find({}, {champ : 1})
```
=> Si on veut exclure un champ : {champ : 0}

- Pour trier des données : 
```
db.collection.find().sort({champ : 1})
```
=> trier dans l'ordre : 1 | trier dans l'ordre décroissant : -1

* Pour compter le nombre de documents avec des champs égaux () : 
```
db.collection.aggregate(
	[
		{
			$match : {
				champATester : Valeur
			}

		}, 
		{
			$count: "nomDuCompteur"
		}
	]
)
```
=> ref : https://www.mongodb.com/docs/manual/reference/operator/aggregation/count/

Array queries : https://www.mongodb.com/docs/manual/tutorial/query-arrays/
- Pour vérifier si un champ contient un certain nombre de valeur (**$size**): 
```
db.collection.find({array : {$size : 1}}) 
```

- Pour vérifier si un tableau contient un ou plusieurs éléments (**$in**):
```
db.collection.find({array : {$in : ["champ1", "champ2"]}})
```

- On peut même vérifier la valeur à l'index n
```
db.collection.find("array.n" : true)
```

## EXO
### (cf exoBook)
Les données
```
{ name: "John Doe", age: 35, job: "Manager", salary: 80000 }

{ name: "Jane Doe", age: 32, job: "Developer", salary: 75000 }

{ name: "Jim Smith", age: 40, job: "Manager", salary: 85000 }
```

- Pour récupérer toutes les données d'une collection : 
```shell
db.collection.find()
```

* Si on veut récupérer les données de ceux dont l'âge est supérieur à 33 
```
db.collection.find({age : {$gt : 33}})
```

* Si on trier les documents dans la collection "employees" par salaire décroissant
```
db.collection.find().sort({salary : -1})
```


* Si on veut  sélectionner uniquement le nom et le job de chaque document.
```
db.collection.find({}, {name : 1, job : 1})
```

* Si on veut compter le nombre d'employés par poste.
```
db.collection.aggregate(
	[
		{
			$match : {
				job : "Manager"
			}

		}, 
		{
			$count: "number_manager"
		}
	]
)
```
=> ref : https://www.mongodb.com/docs/manual/reference/operator/aggregation/count/

* Si on veut faire en sorte que tout les développeurs aient un salaire de 80000
```
db.collection.updateMany({job : "Developer"}, {$set : {salary : 80000}})
```

### cf exo
```
db.salles.insertMany([ 
   { 
       "_id": 1, 
       "nom": "AJMI Jazz Club", 
       "adresse": { 
           "numero": 4, 
           "voie": "Rue des Escaliers Sainte-Anne", 
           "codePostal": "84000", 
           "ville": "Avignon", 
           "localisation": { 
               "type": "Point", 
               "coordinates": [43.951616, 4.808657] 
           } 
       }, 
       "styles": ["jazz", "soul", "funk", "blues"], 
       "avis": [{ 
               "date": new Date('2019-11-01'), 
               "note": NumberInt(8) 
           }, 
           { 
               "date": new Date('2019-11-30'), 
               "note": NumberInt(9) 
           } 
       ], 
       "capacite": NumberInt(300), 
       "smac": true 
   }, { 
       "_id": 2, 
       "nom": "Paloma", 
       "adresse": { 
           "numero": 250, 
           "voie": "Chemin de l'Aérodrome", 
           "codePostal": "30000", 
           "ville": "Nîmes", 
           "localisation": { 
               "type": "Point", 
               "coordinates": [43.856430, 4.405415] 
           } 
       }, 
       "avis": [{ 
               "date": new Date('2019-07-06'), 
               "note": NumberInt(10) 
           } 
       ], 
       "capacite": NumberInt(4000), 
       "smac": true 
   }, 
    { 
       "_id": 3, 
       "nom": "Sonograf", 
       "adresse": { 
           "voie": "D901", 
           "codePostal": "84250", 
           "ville": "Le Thor", 
           "localisation": { 
               "type": "Point", 
               "coordinates": [43.923005, 5.020077] 
           } 
       }, 
       "capacite": NumberInt(200), 
       "styles": ["blues", "rock"] 
   } 
])
```

- Si on veut afficher l'identifiant et le noms des salles qui sont des SMAC
```
db.salles.find({"smac" : true}, {nom : 1})
```

* Si on veut afficher le nom des salles qui possèdent une capacité d’accueil strictement supérieure à 1000 places.
```
db.salles.find({capacite : {$gt : 1000}}, {_id : 1})
```

* SI on veut afficher l’identifiant des salles pour lesquelles le champ adresse ne comporte pas de numéro.
```
db.salles.find({"adresse.numero" : null})
```

* Si on veut afficher l’identifiant puis le nom des salles qui ont exactement un avis.
```
db.salles.find({avis : {$size : 1}}, {_id : 0})
```

* Si on veut afficher tous les styles musicaux des salles qui programment notamment du blues.
```
db.salles.find({styles : { $in : ["blues"]}}, {styles : 1})
```

* Si on veut afficher tous les styles musicaux des salles qui ont le style « blues » en première position dans leur tableau styles.
```
db.salles.find({"styles.0" : "blues"}, {styles : 1})
```

* Si on veut afficher la ville des salles dont le code postal commence par 84 et qui ont une capacité strictement inférieure à 500 places (pensez à utiliser une expression régulière).
```
db.salles.find(
{
	$and : [
	{"adresse.codePostal" : /84\d\d\d/}, 
	{capacite : {$lt : 500}}
	]
}
, {"adresse.ville" : 1}
)
```

* Si on veut afficher l’identifiant pour les salles dont l’identifiant est pair ou le champ avis est absent.
```
db.salles.find(
	{
		$and : [
			{$or : [{_id : {$mod : [2, 0]}}]},
			{$or : [{avis : {$size : 0}]}} 
		]
	}, 
	{_id : 1}
)
```