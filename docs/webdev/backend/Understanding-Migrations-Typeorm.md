## Migrations

Once you run this SQL query your database schema is ready to work with your new codebase. TypeORM provides a place where you can write such sql queries and run them when needed. This place is called "migrations".

To put simply a **migration** is just a single file with sql queries to update a database schema and apply new changes to an existing database.



## How to run migrations ‼️Local‼️

During Testing in Local you can use synchronization. Synchronization will automatically run queries to the the database to match any model changes you have made. _This is only a safe practice in testing your local database. This is not safe for staging or production_

<img width="601" alt="Screen Shot 2022-11-11 at 10 54 49 PM" src="https://user-images.githubusercontent.com/111775505/201457915-2852e318-9bb8-4615-84ae-04f82be911f4.png">

Run command: 

Use the following to auto generate the migration file
- `npm run typeorm migration:generate -- InitialState -d src/main/config/DataSource.ts `

Use the following to run the migration file
- `npm run typeorm migration:run -- -d src/main/config/DataSource.ts `

_Replace the string term InitialState with something that will identify the change. i.e. OrderUpdate or AddOrganizerContactInfo_

## How to run migrations ‼️Stag‼️

**We do not want to push anything in staging database that would not want to run in the production database. All testing should be done on your local database.** 

The code below will run any migrations listed in the AimlyDatasource:

_NODE_ENV would be set to Test_

`if (initializationResult.migrations && NODE_ENV === Env.Test) await initializationResult.runMigrations({ transaction: 'all' })`

## How to run migrations ‼️Prod‼️

The code below will run any migrations listed in the AimlyDatasource:

_NODE_ENV would be set to Prod_

`if (initializationResult.migrations && NODE_ENV === Env.PRODUCTION) await initializationResult.runMigrations({ transaction: 'all' })`

Datasource:

_It is import to note that all migrations will be run in the migrations array._

<img width="641" alt="Screen Shot 2022-11-11 at 10 29 46 PM" src="https://user-images.githubusercontent.com/111775505/201457078-994cea76-fa8b-4454-88b3-cd0bba7a1fd0.png">

Optional Methods:

- runMigrations - Runs all pending migrations.

- undoLastMigration - Reverts last executed migration.


## References:

- [Typeorm Breakdown](https://orkhan.gitbook.io/typeorm/)
- [Typeorm Official Docs](https://typeorm.io/migrations)
- [Typeorm Methods](https://typeorm.delightful.studio/classes/_connection_connection_.connection.html#migrations)
