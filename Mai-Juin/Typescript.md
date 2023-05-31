**Lien documentation officiel TypeScript : https://www.typescriptlang.org/docs/handbook/intro.html**
*Le plus gros problème de JS c'est qu'il n'y a rien qui va détecter les problèmes liés au types.*

```
npm install -g typescript
```
installation de manière globale de typescript

Pour vérifier que l'on a bien typescript :
``` 
tsc
```
tsc = typescript compiler (on a besoin de convertir le ts en js pour que les navigateurs puissent l'exécuter)

Typescript nous permet d'assigner des types à nos variables.
``` ts
let age : number = 20;
let greeting : string = "Hello World"
```

-  *Comment préciser le type d'un array ?*
``` ts
let arrayNumber : number[] = [1, 2, 3]
```

-  *Comment préciser la valeur de retour d'une fonction ?*
``` ts
function getName(name : string) : string {
	return name
}
```


Une variable peut avoir plusieurs types :
``` ts
let iCanChangeType : number | boolean = 4;
iCanChangeType = false;
```
Il faut faire attention aux fonctions que l'on utilise, les comportements seront différents en fonction du type de notre variable. On peut également trouver des fonctions qui ne fonctionne qu'avec un certain type.
________________________________________________
TS nous permet d'ajouter des informations supplémentaire sur le type des variables. 
On peut même créer ses propres types.

## Type custom
Typescript propose le type **enum** 
``` typescript
enum StudentStatus {
	Asleep, 
	Focused,
	Missing
}
```

Il propose également des **interfaces**.
On peut comparer une interface à un contrat, implémenter une interface c'est s'engager à posséder toutes les propriétés présentées dans l'interface.
``` typescript
interface Student {
	firstname : string, 
	lastname :  string, 
	age : number, 
	status : StudentStatus, 
	followInClass(cours : string) : void //on peut aussi passer des fonctions en propriétés
}

const Angelo : Student = new Student({
	"Angelo", 
	"MACAIRE", 
	22, 
	StudentStatus.Focused, 
	followInClass: function(cours: string){ console.log("je suis en " + cours)}
})
```

### Les fonctions ts
``` ts
function createStudent(firstname : string, lastname : string, age : number, status? : StudentStatus) : Student {
	const newStudent : Student = {
	age: age, 
	firstname: firstname, 
	lastname: lastname,
	status : status
	};
	return newStudent
}
```
***Si on la fonction ne retroune rien  : void***
+ le ? permet de rendre optionnel le typage

## Les classes
C'est la base de la programmation orienté object, mode d'emploi qui va indiquer comment les entité de notre programme vont intéragir entre eux 
Et les objets qui sont la classe qui prends vie grâce à l'instanciation avec "new" (on fait une instance). 

``` ts
class Vehicule {
	brand : string;
	color : string;
	speed: number; 
	deplacer(): void {
		console.log(`je me déplace avec ma voiture de la marque ${this.brand}`)
	} 
	constructor() {
	console.log("nouveau véhicule créer")
	}
}

const car : Vehicule = new Vehicule()
voiture.brand = "Peugeot"
voiture.color = "white"
voiture.speed = 10
```

On peut également utiliser le constructor d'une autre manière.
``` ts
class Vehicule {
	brand: string; 
	color: string;
	speed: number; 
	
	deplacer() : void {
		console.log(`je me déplace avec ma voiture de la marque ${this.brand}`)
	}
	
	constructor(brand: string, color: string, speed: number) {
		this.brand = brand; 
		this.color = color; 
		this.speed = speed;
	}
}

const car : Vehicule = new Vehicule("Peugeot", "white", 10);
```