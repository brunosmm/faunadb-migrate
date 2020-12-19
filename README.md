# faunadb-migrate
FaunaDB Migrate is a tool to help [faunadb](https://fauna.com) developers setup theirs app database.
**This is not an official tool supported by Fauna**

## Install
```bash
npm i -g git+https://github.com/brunosmm/faunadb-migrate.git\#master
```

## Before start
Before start you should set `FAUNADB_SECRET` env variable with a faunadb **admin** key.
```bash
export FAUNADB_SECRET=fnyoursecret-here
```

## Commands

### Setup
Setup migrations in faunadb. You should use this command before run the migrations.
```bash
faunadb-migrate setup
# or using a scope env
FAUNADB_SECRET=fnyoursecret-here faunadb-migrate setup
```

### Create migrations
Create new migration file inside of `./migrations` folder.
```bash
faunadb-migrate create create_users
```
This command will generate the following template for you:
```js
module.exports.up = q => {
  return q.CreateCollection({ name: 'Users' })
}

module.exports.down = q => {
  return q.Delete(q.Collection('Users'))
}
```
*The collection name is not dynamic. "Users" is only a sample.*

### Migrate
Run the migration files.
```bash
faunadb-migrate migrate
```
*Currently we are not handling failures well so in case of runnning mutiple migrations and something get wrong you should remove the "garbage" using the console UI or fauna-shell.*

### Rollback
Rollback all the previous changes.
```bash
faunadb-migrate rollback
```

### Help
See all available commands and params.
```bash
faunadb-migrate --help
```

## Improvements
- Tests, tests and tests
- Add `--force` option to ignore errors
- Better error handling

