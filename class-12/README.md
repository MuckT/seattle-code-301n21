# Mongo, Mongoose and Data Modeling

## Overview

Today is all about persistence. We will introduce Mongodb and Mongoose. We will create data models and hard code some data to store in our database so that our front end can retrieve that data. We will introduce `CRUD` and focus on the `R`:`READ`.

## Daily Plan

- Review code challenges
- [Warm-up exercise](./warm-up.md)
- Mongo, Mongoose, Data Modeling
- Code Demo
- Lab Preview

## Learning Objectives

As a result of completing lecture 13 of Code 301, students will:

- Describe and Define
  - CRUD
  - MONGO
  - Mongoose
  - ORM
  - GET
- Be able to create a data model or schema
- Be able to set up a Mongo database using Mongoose
- Be able to retrieve all of the entries from a Mongo database using Mongoose

## Notes

1. What does the R stand for in CRUD?

1. What is an ORM?

1. How are Mongo and Mongoose related?

1. Why do we need to use Mongoose at all?

1. Where does Mongo live?

1. Mongoose:
    - step 1: Bring in Mongoose

    ```javaScript
    const mongoose = require('mongoose');
    // making a database called cats
    mongoose.connect('mongodb://localhost:27017/cats', {useNewUrlParser: true, useUnifiedTopology: true});

    const db = mongoose.connection;
    db.on('error', console.error.bind(console, 'connection error:'));
    db.once('open', function() {
      console.log('Mongoose is connected')
    });
    ```

    - step 2: Make a schema

    ```javaScript
    const catSchema = new mongoose.Schema({
      name: {type: String}
    });

    const kittySchema = new mongoose.Schema({
      name: {type: String, required: true},
      cats: [catSchema]
    });
    ```

    - step 3: Make a model from the schema

    ```javaScript
    const CatParent = mongoose.model('kittyCats', kittySchema);
    ```

    - step 4: Create and save a record

    ```javaScript
    const bob = new CatParent({ name: 'bob', cats: [{name:'fluffy'}, {name:'joe'}]});
    bob.save();
    ```

    - step 5: Gets all the records from the database

    ```javaScript
      CatParent.find((err, person) => {
        if(err) return console.error(err);
        console.log({person})
      });
    ```

    - Gets the record where the name is 'bob'

    ```javaScript
      CatParent.find({name:'bob'}, (err, person) => {
        if(err) return console.error(err);
        console.log({person})
      });
    ```

1. What resources can I use to help me with my lab and to learn more?
[mongoose](https://mongoosejs.com/docs/)
