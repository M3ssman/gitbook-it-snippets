## Database Document MongoDB 3.4+

### General

Start with custom path to database and REST web-gui

```
./mongod --dbpath "/data/<user>/mongodb/databases/" --rest
```

### Administration

```
mongoimport --drop -d students -c grades grades.json
mongoimport --drop -d video -c video video
mongoimport --db video --file video/contacts.json
mongorestore --stopOnError --db video video/movieDetails.bson
```

## Queries

### Read Data

```
# movies from year 2013 where field "rated" is not null
db.movieDetails.find( { "year" : 2013 ,  "rated" : { $not : { $eq : null }} } )
```

### Aggregation

```
db.zips.aggregate([
    {$group:
     {
	 _id:"$state", 
	  population:{$sum: "$pop"}
     }
    }
])
db.zips.aggregate([
    {$group:
     {
	 _id:"$state", 
	  average_pop:{$avg: "$pop"}
     }
    }
])
### example addToSet
db.products.aggregate([
    {$group:
     {
	 _id: { "maker" : "$manufactorer"}, 
	  categories : {$addToSet: "$catagory"}
     }
    }
])
db.zips.aggregate([
    {$group:
     {
	 _id: "$city", 
	  postal_codes : {$addToSet: "$_id"}
     }
    }
])
```



