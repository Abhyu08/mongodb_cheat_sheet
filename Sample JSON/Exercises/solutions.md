1. Write a MongoDB query to display all the documents in the collection restaurants
> db.restraurant.find().pretty();


2. Write a MongoDB query to display the fields restaurant_id, name, borough and cuisine for all the documents in the collection restaurant.

> db.restraurant.find({},{_id:1, restaurant_id :1,name:1 , borough:1,cuisine:1}).pretty();


3. Write a MongoDB query to display the fields restaurant_id, name, borough and cuisine, but exclude the field _id for all the documents in the collection restaurant.

> db.restraurant.find({},{_id:0, restaurant_id :1, name:1 , borough:1,cuisine:1}).pretty();



4. Write a MongoDB query to display the fields restaurant_id, name, borough and zip code, but exclude the field _id for all the documents in the collection restaurant.

> db.restraurant.find({},{restaurant_id:1,name:1,borough:1,'address.zipcode':1,_id:0}).pretty();



5. Write a MongoDB query to display all the restaurant which is in the borough Bronx

> db.restraurant.find({borough:'Bronx'},{}).pretty();


6. Write a MongoDB query to display the first 5 restaurant which is in the borough Bronx.

> db.restraurant.find({borough:'Bronx'},{}).pretty().limit(5);



7. Write a MongoDB query to display the next 5 restaurants after skipping first 5 which are in the borough Bronx.
> db.restraurant.find({borough:'Bronx'},{}).pretty().limit(5).skip(5);


8. Write a MongoDB query to find the restaurants who achieved a score more than 90.
> db.restraurant.find({'grades.score':{$gt:90}},{}).pretty();


9. Write a MongoDB query to find the restaurants that achieved a score, more than 80 but less than 100.

> db.restraurant.find({$and :[ {'grades.score':{$gt:80}} ,{ 'grades.score':{$lt:100} } ] },{}).pretty();



10. Write a MongoDB query to find the restaurants which locate in latitude value less than - 95.754168.

> db.restraurant.find({'address.coord.0':{$lt:95.754168}},{name:1 ,'address.coord':1}).pretty();


11. Write a MongoDB query to find the restaurants that do not prepare any cuisine of 'American' and their grade score more than 70 and latitude less than -65.754168.

db.restraurant.find({'grades.score':{$gt:70} , cuisine:{$ne:"American"} , 'address.coord.0':{$lt:65} , 'grades.0.score':{$gt:70}},{}).pretty();



12. Write a MongoDB query to find the restaurants which do not prepare any cuisine of 'American' and achieved a score more than 70 and located in the longitude less than - 65.754168.
> db.restraurant.find({'grades.score':{$gt:70} , cuisine:{$ne:"American"} , 'address.coord.1':{$lt:65} , 'grades.0.score':{$gt:70}},{}).pretty()



13. Write a MongoDB query to find the restaurants which do not prepare any cuisine of 'American ' and achieved a grade point 'A' not belongs to the borough Brooklyn. The document must be displayed according to the cuisine in descending order.

> db.restraurant.find( {borough:{$ne:'Brooklyn'} , 'grades.0.grade':'A' },{}).pretty().sort({cuisine:-1})



14. Write a MongoDB query to find the restaurant Id, name, borough and cuisine for those restaurants which contain 'Wil' as first three letters for its name.
> db.restraurant.find({name:/^Wil.*$/},{_id:1, restaurant_id :1,name:1 , borough:1,cuisine:1}).limit(1);



15. Write a MongoDB query to find the restaurant Id, name, borough and cuisine for those restaurants which contain 'ces' as last three letters for its name.

> db.restraurant.find({name:/^.*ces$/},{_id:1, restaurant_id :1,name:1 , borough:1,cuisine:1}).limit(1);


16. Write a MongoDB query to find the restaurant Id, name, borough and cuisine for those restaurants which contain 'Reg' as three letters somewhere in its name.


> db.restraurant.find({name:/^.*reg.*$/},{_id:1, restaurant_id :1,name:1 , borough:1,cuisine:1}).limit(1);




17. Write a MongoDB query to find the restaurants which belong to the borough Bronx and prepared either American or Chinese dish.

> db.restraurant.find( { borough:{$ne:'Bronx'} , cuisine:{$in:['American','Chinese']} },{_id:1, restaurant_id :1,name:1 , borough:1,cuisine:1}).pretty().limit(2);


18. Write a MongoDB query to find the restaurant Id, name, borough and cuisine for those restaurants which belong to the borough Staten Island or Queens or Bronxor Brooklyn.
> db.restraurant.find( { borough:{$in:['Staten Island' , 'Queens ' , 'Bronxor Brooklyn']} },{_id:1, restaurant_id :1,name:1 , borough:1,cuisine:1}).pretty()



19. Write a MongoDB query to find the restaurant Id, name, borough and cuisine for those restaurants which are not belonging to the borough Staten Island or Queens or Bronxor Brooklyn.

> db.restraurant.find( { borough:{$nin:['Staten Island' , 'Queens ' , 'Bronxor Brooklyn']} },{_id:1, restaurant_id :1,name:1 , borough:1,cuisine:1}).pretty()




20. Write a MongoDB query to find the restaurant Id, name, borough and cuisine for those restaurants which achieved a score which is not more than 10.
> db.restraurant.find({ 'grades.0.score':{$lte:10} }, {_id:1, restaurant_id :1,name:1 , borough:1,cuisine:1} ).pretty().limit(1);


21. Write a MongoDB query to find the restaurant Id, name, borough and cuisine for those restaurants which prepared dish except 'American' and 'Chinees' or restaurant's name begins with letter 'Wil'.
> db.restraurant.find( { name:/^Wil.*$/ , cuisine:{$nin:['American','Chinese']} },{_id:1, restaurant_id :1,name:1 , borough:1,cuisine:1}).pretty().limit(2);


22. Write a MongoDB query to find the restaurant Id, name, and grades for those restaurants which achieved a grade of "A" and scored 11 on an ISODate "2014-08-11T00:00:00Z" among many of survey dates

> db.restraurant.find({ 'grades.0.score':11 , 'grades.0.grade':'A' , 'grades.0.date' : ISODate("2014-08-12T00:00:00Z") }, {_id:1, restaurant_id :1,name:1 , borough:1,cuisine:1 , grades:1} ).pretty().limit(1);



23. Write a MongoDB query to find the restaurant Id, name and grades for those restaurants where the 2nd element of grades array contains a grade of "A" and score 9 on an ISODate "2014-08-11T00:00:00Z".


> db.restraurant.find({ 'grades.1.score':9 , 'grades.1.grade':'A' , 'grades.1.date' : ISODate("2014-08-11T00:00:00Z") }, {_id:1, restaurant_id :1,name:1 , borough:1,cuisine:1 , grades:1} ).pretty().limit(1);




24. Write a MongoDB query to find the restaurant Id, name, address and geographical location for those restaurants where 2nd element of coord array contains a value which is more than 42 and upto 52

> db.restraurant.find({ $and:[ {'address.coord.1':{$gt:42}} ,{ 'address.coord.1':{$lte:52}} ] }, {_id:1, restaurant_id :1,name:1 , borough:1,cuisine:1 , address:1} ).pretty().limit(2);


25. Write a MongoDB query to arrange the name of the restaurants in ascending order along with all the columns.
> db.restraurant.find().sort({name:1}).pretty();



26. Write a MongoDB query to arrange the name of the restaurants in descending along with all the columns.
> db.restraurant.find().sort({name:-1}).pretty();


27. Write a MongoDB query to arranged the name of the cuisine in ascending order and for that same cuisine borough should be in descending order.
> db.restraurant.find().sort({cuisine:1,borough:-1}).pretty()


28. Write a MongoDB query to know whether all the addresses contains the street or not.
> db.restraurant.find({'address.street':{$exists:false}},{}).pretty()

29. Write a MongoDB query which will select all documents in the restaurants collection where the coord field value is Double.
> db.restraurant.find({'address.coord':{$type:'double'}},{}).pretty()


30. Write a MongoDB query which will select the restaurant Id, name and grades for those restaurants which returns 0 as a remainder after dividing the score by 7.

> db.restraurant.find({'grades.0.score':{$mod:[7,0]}},{restaurant_id:1,name:1,grades:1}).pretty()

31. Write a MongoDB query to find the restaurant name, borough, longitude and attitude and cuisine for those restaurants which contains 'mon' as three letters somewhere in its name.
> db.restraurant.find({name:/^.*mon.*$/},{name:1,borough:1,'address.coord':1}).pretty()



32. Write a MongoDB query to find the restaurant name, borough, longitude and latitude and cuisine for those restaurants which contain 'Mad' as first three letters of its name.
> db.restraurant.find({name:/^Mad.*$/},{name:1,borough:1,'address.coord':1}).pretty()


