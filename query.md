//Provide a query showing just the names (and nothing else) of the Italian
//restaurants.
db.restaurants.find({cuisine:"Italian"})

//Provide a query showing how many Bakeries have a name that start with "M".
db.restaurants.find({name: /^M/})

//Provide a query showing the zip codes (and `_id`s) of all restaurants with
the word "Ice" in their cuisine.
db.restaurants.find({cuisine: /Ice/}, {"address.zipcode": true})

//Provide a query showing the street and street number of Chinese restaurants
ordered by zip code.
db.restaurants.find({cuisine: "Chinese"}, {"address.building" :1, "address.street" :1}).sort({"address.zipcode": 1})

//Show only the American restaurants in Manhattan.
 db.restaurants.find({$and: [{cuisine: "American"},{borough: "Manhattan"}]})

//Provide a query showing the restaurants that have been graded exactly 4
times.
db.restaurants.find({$where: 'this.grades.length>=4'})

//Provide a query showing only `_id`, name and 2 grades from each restaurant on
Broadway.
db.restaurants.find({"address.street": "Broadway"},{name: 1, grades: {$slice: 2}})

//Provide a query showing the 5 pizza restaurants in the Bronx with the highest
score on an evaluation.
db.restaurants.find({$and : [{borough: "Bronx", cuisine: "Pizza"}]}).sort({"grades.score": -1}).limit(5)

//Provide a query to find all of the restaurants in Brooklynn and list only the
11st-20th results when ordered alphabetically by name.

db.restaurants.find({borough: "Brooklyn"}).limit(10).skip(10)

//Provide a query that returns all pizza and Italian restaurants in reverse
alphabetic order.
 db.restaurants.find({$or:[{cuisine: "Pizza", cuisine: "Italian"}]}).sort({name: -1})
