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
https://developer.mozilla.org/fr/docs/Web/HTT   P/Status

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

## Gestion des erreurs : 
https://expressjs.com/en/guide/error-handling.html

Le middleware pendant la gestion d'erreur prends en paramètres 4 arguments (err, req, res, next).

Créer un middleware et le mettre tout en dernier dans la chaîne pour qu'il puisse gérer les erreurs

xhr = XML HTTP Request 

# Définition REST(FUL)
REST est un ensemble de contrainte architecturales. 
REST signifie *Representational State Transfert*.

Chaque URLS est vue comme une *requête* et chaque données retournées sont vues comme des *réponses*.

## Les principes :
1. Interface uniforme : 
*Cette règle permet le transfert standardisé des informations.*
Notre API doit être  :
- Prédictible
- Bien documentée
- Bien structurée

2. Séparation Client-Serveur
*Le client et le serveur doivent être indépendant.*
La seule information que l'application client possède est l'URI de la ressource désirée. Inversement, le serveur ne peut pas modifier l'application client autrement que par les données envoyée en requête HTTP.


3. Statelessness ()
Chaque requêtes doivent contenir toutes les informations nécessaires. 
Les applications serveurs ne sont pas autorisé à stocker les données liées à la requête du client.

4. Mise en cache
Possibilité de mettre des données en cache du côté client ou serveur. Les réponses du serveur doivent aussi contenir l'informations sur si la ressource envoyé peut être mise en cache.
=> L'API REST doit pouvoir informer de la durée de validité d'une réponse http pour que le client puisse la mettre en cache

5. Système d'architecture en couche
*Invisible pour le client.*
L'application client et l'application serveur ne sont pas directement connectés l'un à l'autre. Il y a différents intermédiaires.

6. Code à la demande (facultatif)
Dans certains cas il arrive que les réponses contiennent du code exécutable. 

## CRUD
https://developer.mozilla.org/fr/docs/Glossary/CRUD
(Create, Read, Update, Delete)
Cet acronyme fait référence à la manière dont sont les opérations sont effectuées dans une base de données.
Les API REST vont communiquer à travers les requêtes HTTP avec le standard CRUD.

- GET
=> Permet de retourner une représentation de l'information et des données contenu dans une ressource. 
Peut importe le nombre de fois que la requête est appelée, elle doit toujours retourner le même résultat

- POST
=> Appliquer POST à la ressource parent permet de créer une nouvelle ressource.

- PUT
=> Permet de modifier la ressource en remplaçant complètement son contenu. 

- PATCH
=> Permet aussi de modifier les ressources, il va cependant le changer et non le remplacer complètement comme PUT.

- DELETE
=> Cible une seule ressource et va complètement la supprimer

### Méthodes HTTP
https://developer.mozilla.org/fr/docs/Web/HTTP/Methods
En effet CRUD sont des méthodes de requêtes qui vont indiquer l'action que l'on souhaite réaliser sur la ressource indiqué. 
Cependant il en existe d'autres : 
- HEAD
=> Demande une réponse identique à une requête GET mais on récupère uniquement l'en-tête

- CONNECT
=> Permet d'établir un tunnel vers le serveur identifié par la ressource cible

- OPTIONS
=> Permet de décrire les options de communications avec la ressource visée

- TRACE
=> Permet de réaliser un message test aller/retour en suivant le chemin de la ressource visée
Pratique pour vérifier si les requêtes sont bien reçues.


## CORS
*Cross-Origin Resource Sharing*
Par défaut les cors ne sont pas autorisés. 
![[Pasted image 20230609114238.png]]

Pour les autoriser : 
```js
app.use((rq, res, next) => {
	res.setHeader('Access-Control-Allow-Origin', '*');
	res.setHeader('Access-Control-Allow-Methods', 'GET, POST, PUT, PATCH, DELETE');
	res.setHeader('Access-Control-Allow-Headers', 'Content-Type, Authorization')
})
```

## Termes liées à REST
### URI :
*Uniform Resource Identifier*
https://developer.mozilla.org/fr/docs/Glossary/URI
C'est une chaîne qui fait référence à une ressource. 
**URI est un moyen d'identifier ses ressources comme une étiquette**

#### Quelle est la différence entre URI/URL/URN ?
![[Pasted image 20230608160946.png]]
**URL | Uniform Resource Locator** : spécifie où une ressource peut-être trouvé sur internet
https://developer.mozilla.org/fr/docs/Glossary/URL

**URN | Uniform Resource Name** : format standardisé qui fait référence à une ressource sans spécifier son emplacement ou si elle existe.
https://developer.mozilla.org/fr/docs/Glossary/URN

Toutes les URL/URN sont des URI mais la réciproque n'est pas vraie.

### Ressource
https://www.ibm.com/docs/en/was-zos/9.0.5?topic=applications-defining-resources-in-restful
Les ressources peuvent contenir des données statiques ou dynamiquement mis à jour. 
Il est important de définir les ressources pour notre API REST.
C'est ressources que les fonctions CRUD vont s'appliquer.

### Représentation
L'état d'une ressource à un instant particulier corresponds la représentation de la ressource.
Cette information peut être délivrée au client dans ces formats :
- JSON
-  HTML
- XLT 
- Python
- PHP
- Texte brut

*Le format JSON est le plus populaire.*




![[Pasted image 20230608172600.png]]
# Aller plus loin
## Système d'authentification 
=> utilisation des dépendances bcrypt et jwt (jsonwebtoken)
https://www.npmjs.com/package/bcrypt
https://www.npmjs.com/package/jsonwebtoken

### Lors de la création d'un utilisateur
On va d'abord hasher le mot de passe de notre utilisateur grâce à la méthode hash de brcypt qui prends en paramètre le texte à crypter et le saltRounds (corresponds au nombre de fois que la chaîne de caractère sera haché)
```
//code before
bcrypt
	.hash(password, 12)
	.then(hashedPw => {
		const newUser = new User({
			email = res.body.email
			password : hashedPw,
			name : req.body.name
		})
		
		return user.save()
	})
```

### Lors de la connexion de l'utilisateur
Pour vérifier que l'utilisateur a rentré le bon mot de passe : utilisation de la fonction compare de bcrypt. Il prends en paramètre 2 chaîne de caractère et va les comparer.
```js
//code before
User.findOne({ email: email })
	.then(user => {
		if (!user) {
			const error = new Error('A user could not be found.');
			error.statusCode = 401;
			throw error;
		
		}
		loadedUser = user;
		return bcrypt.compare(password, user.password);
	.then(isEqual => {
	if (!isEqual) {
		const error = new Error("Wrong password")
		error.statusCode = 401;
		throw error
	}
	const token = jwt.sign({
		email : loadedUser.email, 
		userId : loadedUser._id.toString()
	},
	"somesupersecresecret",
	{expiresIn : '1h'}
	)
	})
})
```
On remarque qu'après avoir comparé nos 2 mots de passe ont utilise ce que retourne la méthode compare. Si le mot de passe est mauvais, on envoie une erreur mais si le mot de passe est bon => création d'un token

#### Qu'est-ce qu'un JSON web token ? 
https://datatracker.ietf.org/doc/html/rfc7519
https://auth0.com/docs/secure/tokens/json-web-tokens

JWT = JSON web token

=> <u> Qu'est-ce qu'un token ? </u>
https://www.fortinet.com/resources/cyberglossary/authentication-token
Un token d'authenification permet l'utilisateur d'accéder aux applications, services,, websites et API sans avoir besoin de se connecter à chaque fois qu'il visite la page.

Il est composé de 3 parties :
- **Header** : l'en-tête qui définie le type de token qui est utilisé ainsi que l’algorithme qui est utilisé pour signer
- **Payload** : Permet de définie l'émitteur du token ainsi que les détails d'expiration. Donne aussi les informations sur l'utilisateur et d'autre métadonnées
- **Signature** : Permet de vérifier l'authenticité du message et que le message n'a pas changé pendant le transfert.

___ 
JWT est un standard qui défini une manière compacte et indépendante de transmettre des informations en format JSON.

=> <u> Pourquoi utiliser JWT ? </u>
Pour :
- Authentification : Quand un utilisateur est connecté, on retourne in **ID token** (un ID token est toujours un JWT)
- Autorisation : Certaines routes ou mêmes toutes ont besoin d'un *Access Token* (qui peut être une forme de JWT) pour permettre à l'application d'accéder aux données
- Echange d'informations : JWT est un bon moyen de transmettre des informations entre deux parties de manière sûre car l'échange est signé. En d'autre terme, on est sûre que celui qui envoie est celui qui prétends être.

#### Utilisation
Si on reprends l'exemple si dessus, on utilise la méthode jwt.sign() pour créer un token.
Définition : **jwt.sign(payload, secretOrPrivateKey, [options, callback])**

##### Utiliser notre jwt pour protéger nos routes
Création d'un middleware qui va vérifier si l'utilisateur est authentifié.
```js
module.exports = (req, res, next) => {
	const authHeader = req.get('Authorization');
	if (!authHeader) {
		const error = new Error('Not authenticated.');
		error.statusCode = 401;
		throw error;
	}
	const token = authHeader.split(' ')[1];
	let decodedToken;
	try {
		decodedToken = jwt.verify(token, 'somesupersecretsecret');
	} catch (err) {
		err.statusCode = 500;
		throw err;
	}
	if (!decodedToken) {
		const error = new Error('Not authenticated.');
		error.statusCode = 401;
		throw error;
	}
	req.userId = decodedToken.userId;
	next();

};
```

Pour les utiliser dans le fichier qui s'occupe des routes : 
```js
router.get("/product", isAuth, productController.getProducts);
```

Quand on va faire appelle à cette requête, on passe d'abord par "isAuth" et si tout est bon on passe au middleware "getProducts"

Pour passer le token :
"Authorization" : "Bearer JWT"

# Pour plus de sécurité
Nous avons vu l'utilisation de jwt et bcrypt mais il est aussi important de protéger nos données sensible en utilisant des variables d'environnement.

## DOTENV .env
Graĉe à la dépendance dotenv on peut utiliser le fichier .env
```
npm install dotenv
```
Des données comme notre connexion à notre base de données ou le salt de bcrypt sont des informations sensibles que l'on ne doit pas dévoiler. 

## Vérifier le format des variables envoyées
Il est aussi important de contrôler les formats des variables envoyés dans notre base de données.


# Dépendances utiles
## Swagger UI express
https://www.npmjs.com/package/swagger-ui-express
Permet de documenter notre api