# FRONT
## Style
### Prettier & ESlint
```
npm install -D prettier
npm install -D eslint-config-prettier eslint-plugin-prettier
```

#### .prettierrc.json
Permet de configuer notre formattage 
Lien de la docs : https://prettier.io/docs/en/index.html

#### Settings
On installe l'extension Prettier dans VSC.
Ensuite dans settings > rechercher format on save > rechercher default formatter : prettier 

## Utils
### React Router DOM
*lib de routing pour React, permet d'afficher un contenu pour un chemin donné*

#### CreateBrowserRoute
Tableau qui va contenir des objets qui auront au minimum 2 éléments :
- un path 
- un element (celui à charger)

```tsx
import {createBrowserRoute, RouterProvider} from "react-router-dom"

consst router = createBrowserRoute([
	{
		path="/",
		element=<App/>
	}, 
	{
		path="/test",
		element=<div>hello test</div>
	}
])

export function Routes() {
	return <RouterProvider router={router}/>
}
```
*Problématique : Si on veut que certaines parties soit fixes, on peut donner le paramètres children qui prends aussi un tableau similaire à son parent*

![[Pasted image 20230605113423.png]]


```tsx
import {Outlet} from "react-router-dom"
import {Header} from "./Header"

export default function App() {
	return (
	<>
		<Header/> // contenu statique
		<Outlet/> // contenu dynamique | les childrens de App 
	
	</>
	)
}
```

On a d'autres paramètres comme : 
- errorElement : l'élément que l'on va recharger en cas d'erreur de notre page
- loader (avec le hook useLoaderData pour récupérer les données) : permet de charger les données
- action

React-router-dom a également ses propres composants :
- Form : permet de simuler au navigateur un routing côté client avec une mutation de donnée
-

#### Params
On les reconnait dans une url car ils sont précédés de ":". Ce sont des segments dynamiques qui vont se synchroniser avec les changements.


# BACK
## Swagger UI
https://github.com/scottie1984/swagger-ui-express
https://www.npmjs.com/package/swagger-jsdoc
Permet de visualiser sur une page internet toutes nos routes.

# General
## git cz
https://www.conventionalcommits.org/en/v1.0.0/
https://www.npmjs.com/package/commitizen
Permet de créer des commit conventionnels

On peut écrire un script dans le package.json qui permet de lancer cz

```json
{
	"script" : {
		"commit" : "cz"
	}
}
```