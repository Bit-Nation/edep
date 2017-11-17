# edep
> A easy (hopefully) way to work with dependency injection in javascript. THIS is in an experiment mode. 

## Why?
I couldn't find a nice tool to handle dependency injection for javascript. Everything i fould is abonded, for an OO approach or very bad documented / don't work. 

## The goal
The goal is, to have way to inject "static" dependecy's into functions without doing manual and still being able to call the funciton with custom arguments. 

E.g: 

```js

//src/services/mongo.js

export const db = mongo('...mongo_url...');

...
...

```

```
//src/user/repo.js

export function insertWayA(db){
	
	return (user) => {

		db.insert(user);

	}

}

export function insertWayB(db, user){
	
	db.insert(user);

}

```

```
//src/app.js

import {db} from './services/mongo.js';
import {insertWayA, insertWayB} from './user/repo.js';


/////////////////////////////////////////////
// The anoying way (if your project grows) //
/////////////////////////////////////////////

const user = {
	email: 'hi@example.com',
	password: 'i_am_secret'
}

/**
* It's obvuisly that this proccess can be anoying, 
* imageing you would have 3 "static dependencys" (like the database) 
* and a few parameters that you want to dynamilcly pass in. 
*/
insertWayA(db, user);

/**
* Insert way b is almos as anoying and resouce takeing.
*/
insertWayB(db)(user)


```

```
// edep.js

export default {
	
	//Holds all services
	services: []

	//Register a service with a name, it's "functionality" (has to be a function) 
	//and an array of string which represent other needed services which will be register in the application lifecyle
	//@todo think about if an autoinjection wouldn't be awesome
	reg(name, service, args),

	//Call the service and inject the dynamic dependecy's. The service will be called with the static + dynamic dependency. 
	call(name, param1, param2)
}



```

