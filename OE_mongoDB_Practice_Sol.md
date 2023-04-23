# OE_MongoDB_Practice
Laboratory practice for the Mongo DB lecture.

## IF NECESSARY 

install Mongo DB Comunity version form the link:

 ```https://www.mongodb.com/try/download/community?tck=docs_server```

since the new version of mongo requires the databese tools to be installed separately.
they can be found in the link:
```https://www.mongodb.com/try/download/database-tools```

(For Windows) Copy the files inside the forlder "bin" into the 
```C:\Program Files\MongoDB\Server\x.x\bin```

## Prepare de Database

In a CMD window on the repository folder (Mongo DB is NOT runing)

```
mongoimport --db test --collection movieDetails --file imdb-new.json

```

What is the output of the previous command? 

Run Mongo DB

``` bash
mongosh
```
or in the previous version 

``` bash
mongo
```

Access the database "test"

```
use test
```

confirm that the data set was imported properly.

```
db.movieDetails.count();
```

You should get a total of 2295 collections

now try

```
db.movieDetails.findOne();
```

## TASK
Create queries to find out the requiered information:

### How many Comedies are in the movieDetails?

```js
db.movieDetails.find({genres:"Comedy"}).count();
# 749

```

```js
db.movieDetails.find({genres:{$in:["Comedy"]}}).count();
# 749
```

### How many Western films exists among its genres?

```js
db.movieDetails.find({"genres.1":"Western"}).count();
#14
```

### How many movies in the movieDetails collection have exactly 1 award won or 1 award nominations?

```js
db.movieDetails.find({$or: [{"awards.wins":1}, {"awards.nominations":1}]}).pretty();
# 339
```

### How many documents list just these two writers: "Ethan Coen" and "Joel Coen", in that order?

```js
db.movieDetails.find({writers: ["Ethan Coen", "Joel Coen"]}).count();
```

### How many movies match the following criteria?

* The cast includes either of the following actors: "Seth MacFarlane".
* The viewerRating is greater than 7.
* The mpaaRating is "R".

```js
db.movieDetails.find({writers: {$in: ["Seth MacFarlane"]}, viewerRating: {$gt: 7}, mpaaRating: "R"});
# 0 
```
### Show the top 5 rated film with the most voted (by imdb) films. Show only title and ratings and votes.

```js
db.movieDetails.find({},{"title":1,"imdb.rating":1, "imdb.votes":1, _id:0}).sort({"imdb.votes":-1,"imdb.rating":-1}).limit(5);
# 5 
```







