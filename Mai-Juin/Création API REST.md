# Initialisation
- ExpressJS 
Est un middleware

Middleware => prends en paramètre (req, res, next) une requête et permet de renvoyer une réponse ou passer le relais à un middleware suivant

```js
qpp.use((req, res, next) => {})
```
*next permet de passer au middleware suivant*
On peut enchainer plusieurs middleware dans une requete

## Definition
**REST** (Representational State Transfer) defini un standard et des contraintes tels que :
- l'utilisation de d'URI pour identifier les ressources
- l'utilisation de méthodes HTTP (GET, POST, PUT, DELETE, etc...) pour effectuer des opérations sur ces ressources
- la representation des ressources au format JSON ou XML

Les API (Application programming interfaces) sont des 'interfaces' aui per;ettent a des applications de communiquer entre elles. On s'en sert notamment afin d'echanger des donnees.

Voici un exemple de JSON aui represente un etudiant ISITECH :
``` JSON
{
	"lastname" : "DJEBLI",
	"firstname" : "Ayoub",
	"age" : 19,
	"addresse" : {
		"rue" : "2 rue de la paix",
		"ville" : "Paris",
		"pays" : "France"
	},
	phoneNumbers : [
		{"type" : "mobile", "number" : "0606060606"}
	]
}
```


Endpoint : point d'entrée de notre requête

## dépendances à télécharger 
- body-parser : permet de récupérer les données que l'on passe (middleware)


## Les codes http :
https://developer.mozilla.org/fr/docs/Web/HTTP/Status

- 2XX : tous s'est bien passé (200 : OK, 201 : Created)
- 3XX : redirection
- 4XX : Erreur due au client (404 : Not Found)
- 5XX : Erreur due au serveur

## CRUD
Pour chaque ressource mettre en place un CRUD : 
- Create
- Read
- Update
- Delete : (soft delete)

Les grands principes REST

### Bonnes pratiques : 
- quand on veut récupérer un post (par exemple) par son id bien faire attention à gérer le cas où le post que l'on récupère n'existe plus

=> bien faire attention à gérer toutes les erreurs possibles