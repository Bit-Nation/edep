# edep
> A (hopefully) easy way to work with dependency injection in JavaScript. **This repository is in experiment mode**. 

## Why?
I couldn't find a nice tool to handle dependency injection for JavaScript. Everything was either abondoned for an OO approach, or poorly documented / doesn't work. 

## The goal
The goal is, to have way to inject "static" dependecy's into functions, without doing it manually, and still being able to call the funciton with custom arguments. 

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
* It's obvious that this proccess can be annoying, 
* Imgine having 3 "static dependencies" (like the database) 
* and a few parameters that you want to dynamically fit in. 
*/
insertWayA(db, user);

/**
* Insert way b is almost as annoying and resource consuming.
*/
insertWayB(db)(user)


```

```
// edep.js

export default {
	
	//Holds all services
	services: []

	//Register a service with a name, it's "functionality" (has to be a function) 
	//and an array of string which represent other needed services which will be registered in the application lifecyle
	//@todo think about if an autoinjection wouldn't be awesome
	reg(name, service, args),

	//Call the service and inject the dynamic dependencies. The service will be called with the static + dynamic dependency. 
	call(name, param1, param2)
}



```

