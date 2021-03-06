Simple wrappers to the node oracle library integrated with a promise interface. It contains simple commands such as executing a statement and executing a query after connecting commiting and releasing. Viable with node version > 4.0.0.

##### Dependency:

https://github.com/oracle/node-oracledb

#### Installation

```
npm install node_oracle_wrappers
```

#### Example usage

```javascript

const oracleWrappers = require('node_oracle_wrappers');

let credentials = {
	user: "hello",
	password: "world",
	connectString: "localhost/XE"
};

/*
Simple query execution
*/


let query = `select 'hello world' from dual`;

oracleWrappers.getData(credentials, query)
.then((results)=> {
	let rowsInObjectFormatt = results.rows;
	let metaData = results.metaData;
})
//Will propagate all errors during either phase of connection / etc
.catch((errors)=> {
	console.error("Odear!");
	console.log(errors);
})

/*
Query with bind variables
*/

let query = `select * from base_table where column = :bindOne`;

const bindParams = {
	bindOne: 'some bind condition'
}

oracleWrappers.getData(credentials, query, bindParams)
.then((results)=> {
	let rowsInObjectFormatt = results.rows;
	let metaData = results.metaData;
	console.log(rowsInObjectFormatt);
})
.catch((errors)=> {
	console.error("Odear!");
	console.log(errors);
})

```
#### Methods

```
# Will connect, query and release. Note params are optional.
oracleWrappers.getData(credentials, query, params)

# Will connect, execute, commit and release. Note params are optional.
oracleWrappers.executeStatement(credentials, statement, params)
```