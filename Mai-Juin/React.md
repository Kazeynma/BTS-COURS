
?) Firebase (pour les app mobile, nous aide à faire beaucoup moins de code au départ)

# Introduction à React 
une bibliothèque open-source qui permet la construction d'interfaces graphiques avec HTML, CSS et Javascript.

Programme de la semaine :
-  Comprendre les avantages apportés par React
-  Découvrir le **JSX**
-  Créer des **composants**
-  Comprendre les imports et les exports
-  Utiliser des **props**
-  Utiliser le State
-  Utiliser les events en React


Reaact = framework en javascript // on le considère plus comme une bibliothèque

Javascript permet de manipuler le DOM ( = c'est la représentation 'objets' des éléments HTML qui constitue une page web ), autrement dit, c'est une interface qui permet d'intéragir avec la stucture des pages web. 
*Manipuler le DOM directement peut être très coûteux*
Documentation MDN DOM : https://developer.mozilla.org/fr/docs/Web/API/Document_Object_Model

=> React utilise un DOM virtuel pour afficher ses composants (Virtual DOM, shadow DOM) // *Ce qui fait que React est très performant*

**JSX = Javascript XML** 

## Comment c'est possible de mettre de l'html dans le js ?
Dans cet exemple : 
``` jsx
	function app() {
		return (
			<div class="App"></div>
		)
	}
```

*Il faut faire attention car en html, class est utilisé en tant que classe CSS alors qu'en js class est réserve pour faire des classes => class est un mot réservé* 

Pour ne pas avoir ce problème, React va avoir ses propres mots réservés. *class => className*
React = mélange de HTML et JS



## Comment notre navigateur compile React 
Les navigateurs ne se sont pas adaptés pour compiler du React, c'est React qui c'est adapté =
**Transpilation** (certain diront compiler), et un outil pour faire cette transpilation est **babel**.
Site internet Babel : https://babeljs.io/
Pour voir comment les syntaxes JSX sont compilées : https://babeljs.io/repl

*Avec l'aide de codeBox.io* : 
Dans un index.js d'un projet React on a 2 bibliothèques : 
- react 
- react-dom (pour manipuler le dom)

avec n'importe quel site internet, si on a un transpiler, react et react-dom on peut injecter du React


## Imports Exports
*Les imports et les export permettent de structurer les fichiers js en module*

Par défaut, js exécute ce que l'on appelle "global scope"/ Le contenu du code provenant d'un fichier est automatiquement disponible dans un autre fichier

### module
On peut considérer qu'un fichier js est un module dès lors qu'il contient un "export"

``` js
function myFuncA() {
	
}

function myFuncB() {

}

function myFuncC() {

}

export {myFuncA, myFuncB, myFuncC}; // syntaxe de l'export nommé
```
*Ce fichier est un module car un a un "export"*

A ne pas oublier à faire , dans le package.json :
``` json
"type" : "module
```
*Pour pouvoir utiliser la syntaxe import/export* // module pour ESmodule

1 export default par fichier
```
export default myFuncA;
```
*Quand on va importer, on n'est pas obligé d'avoir le même nom / cf ./COURS-TP/REACT/import-export* 


## Initialisation d'un projet REACT
``` bash
npm create vite@latest
// ou
npm create vite@latest my-vue-app -- --template react-ts
```
*pnmp permet de régler le soucis sur le poids du node_module*
### Pourquoi ne plus utiliser create-react-app ?
C'est très lourd et c'est assez dur pour remise à niveau etc...

### ECMAScript
Association qui est à l'origine du standard JS
=> ne signifie pas que tout les navigateurs sont à jour sur les nouveaux standard ECMA (faire attention)

## Premier pas  sur l'application 

pour faire un composant :
- Faire commencer le fichier par une majuscule
- .jsx
- Faire commencer la fonction composant aussi par une majuscule

Exemple : 
``` jsx
<>
</>
```
comme les balises div, une des fonctionnalités de React pour éviter la pollution des div au sein du DOM

La totalité du template d'un composant doit être dans un seul return 
=> template = jsx du composant

### Props
Les props sont des paramètres optionnels que l'ont peut passer à un composant React. Elles constituent un objet qu contient notamment des propriétés que l'on peut choisir.

C'est le composant parent qui fait passer la props à l'enfant en utilisant des attribut JSX.

On est pas obligé de l'appeler comme ça mais c'est une convention.

``` jsx
export default function Alert({message, type}){}
```
*Permet de ne récupérer que des props spécifiques*

On peut également rajouter *children* qui est commune à tous les composants React. Elle permet de spécifier un endroit du template dans lequel on va pouvoir afficher le template de composant(s) enfant(s)
On a aussi *key* qui est commun à tous les composants React. 
**Ce sont donc des mots réservés**

```jsx
export default function Alert({message, type, children}) {
	{children} // permet d'afficher les enfants 
}
```

### State
L'Etat d'un composant désigne une variable sp&éciale qui contient des informations sur le contenu actuel du composant. Par exemple, un composant peut être en état d'erreur ou de changement.
Un changement de cet état va entraîner ce que l'on appelle communement un :  `re-render`

* Utilisation du hook useState()
```
	const [count, setCount] = useState(initialState);
```
*Syntaxe destructuration*

#### un hook
Qu'est qu'un hook ? 
*  permet de gérer l'état ou le cycle de vie de nos composants
*  donné par React et commence par "use"

#### Les événements
ils commencent tous par "on" et fournissent tous des cb qui permettent d'exécuter des fonctions.
Par exemple : *onClick*
```
onClick={()}
```

Pour le handler on a une convention pour les nommer :
- handleClick
- clickHandler