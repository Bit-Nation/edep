# edep
> A easy (hopefully) way to work with dependency inject in javascript 

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
import {insert} from './user/repo.js';



```
