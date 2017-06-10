## This is example app of `graphql-compose`

[![Greenkeeper badge](https://badges.greenkeeper.io/nodkz/graphql-compose-examples.svg)](https://greenkeeper.io/)

Live example on Heroku: [https://graphql-compose.herokuapp.com/](https://graphql-compose.herokuapp.com/)

```
npm install
npm run seed && npm run start:watch
open http://localhost:3000
```


## User: simple schema with one type
This [example](https://github.com/nodkz/graphql-compose-examples/tree/master/examples/user) has simple User mongoose model that supports bunch of CRUD operations.

```js
const UserSchema = new mongoose.Schema({
  name: String, // standard types
  age: {
    type: Number,
    index: true,
  },
  languages: {
    type: [LanguagesSchema], // you may include other schemas (here included as array of embedded documents)
    default: [],
  },
  contacts: { // another mongoose way for providing embedded documents
    email: String,
    phones: [String], // array of strings
  },
  gender: { // enum field with values
    type: String,
    enum: ['male', 'female', 'ladyboy'],
  },
});
```

<img width="982" alt="screen shot 2016-07-03 at 15 23 03" src="https://cloud.githubusercontent.com/assets/1946920/16544733/9ef9b146-4132-11e6-8a90-8702d2474cfd.png">

<img width="1330" alt="screen shot 2016-07-15 at 12 41 17" src="https://cloud.githubusercontent.com/assets/1946920/16865833/7ec028c8-4a89-11e6-980e-e17745e5085c.png">


## User for Relay: simple schema with one type

This [schema](https://github.com/nodkz/graphql-compose-examples/tree/master/examples/userForRelay) shows all available CRUD operations which are compatible with Relay. It uses `graphql-compose-mongose` and `graphql-compose-relay`:
- `composeWithRelay(RootQueryTC)` adds `node` field to the RootQuery. Via `RootQuery.node(id)` you may find objects by globally unique ID among all types.
- `composeWithRelay(UserTC)` - modify `UserTC` generated by `graphql-compose-mongoose`  
  - adds `id` field with Relay's globally unique ID
  - this type will be added to `NodeInterface` for resolving via `RootQuery.node`
  - for mutations will be added `clientMutationId` to input and output objects types
  - also all arguments in mutations will be moved into `input` arg
  
<img width="1362" alt="screen shot 2017-03-13 at 10 20 34" src="https://cloud.githubusercontent.com/assets/1946920/23841356/d3bd6f42-07d6-11e7-94f5-cc3618eaf45a.png">


## Northwind: complex schema with 8 models 🌶🌶🌶

This is a sample data of some trading company, which consists from 8 models. All models has cross-relations to each other. This schema used in the Relay example app: [Server schema code](https://github.com/nodkz/graphql-compose-examples/tree/master/examples/northwind), [Client app code](https://github.com/nodkz/relay-northwind-app), [Live demo of client](https://nodkz.github.io/relay-northwind/).

![relay-northwind-app](https://cloud.githubusercontent.com/assets/1946920/18013918/488e6830-6be2-11e6-84b6-884c8ab971ac.gif)


## Elasticsearch REST API wrapper

This [schema](https://github.com/nodkz/graphql-compose-examples/tree/master/examples/elasticsearch) uses [graphql-compose-elasticsearch](https://github.com/nodkz/graphql-compose-elasticsearch) module and  provides full API available in the official elasticsearch module. 

<img width="1316" alt="screen shot 2017-03-07 at 22 26 17" src="https://cloud.githubusercontent.com/assets/1946920/23841396/2c123b3c-07d7-11e7-8c83-ff01c98090fb.png">
