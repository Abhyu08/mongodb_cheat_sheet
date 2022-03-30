## mongoimport --db test --collection movie --file D:\movie.json
 ```
 1. to import JSON:
 mongoimport --db admin --collection movie --file D:\movie.json
 ```
 ```
 2. to check collections
 show collections
 ```
 ```
 3. to show all elements
 db.movie.find()
 ```
 ```
 4. to return where rating=3 and only output name
 db.movie.find({rating:3},{name:1,_id:0})
 ```
 ```
 5. to print only name (here default id also be printed..)
 db.movie.find({},{name:1})
 ```
 ```
 6. to find movie rating > 3 and show only name,rating columns..
 db.movie.find({rating:{$gt:3}} , {name:1 ,rating:1,_id:0})
 ```
 ```
 7. sort in db
 db.movie.find( {} , {name:1 , price:1 , rating:1 ,_id:0}).sort({rating:-1}).pretty().limit(1);
 ```
 ```
 8. skip and limit in DB
 db.movie.find( {} , {name:1 , price:1 , rating:1 ,_id:0}).sort({rating:-1}).pretty().limit(1).skip(1);	
 ```
 ```
 9. Relational operators  [ gt,lt,gte,lte ]
 db.movie.find({ $or: [ {rating:{$gte:3}  }, { price:{$gte:200} } ] } , {name:1, rating:1 , _id:0 }).sort({name:1});
 ```
 ```
 10.search based on 1st index of array
 db.movie.find({} , {'actor.0','Amitabh'} );
 ```
 ```
 11.search based on 2nd index of array
 db.movie.find({} , {'actor.1','Amitabh'} );
 ```
 ```
 12. 
 db.movie.find( {'actor.1':'Amitabh'} , {name:1,actor:1,_id:0}).pretty();
 ```
 ```
 13. Regex in Mongo DB.(to search pattern like K* | k* )
 db.movie.find({name:/^[Kk].*$/}).pretty(); //Regex
 ```
 ```
 14. to seach where rating is null ($in --> similar of (in) in SQL )
 db.movie.find({rating:{$in:[null] , $exists:true}}).pretty();
 ```
 ```
 15. to search where rating -> null
 db.movie.find({rating:null}).pretty();
 ```
 ```
 16. to print where rating is not null
 db.movie.find({rating:{$exists:true}}).pretty(); //where rating not null
 ```
 ```
 17. to search where size of list is 3
 db.movie.find({actor:{$size:3}}).pretty(); //size
 ```
 ```
 18. to print where rating type defined as string
 db.movie.find({rating :{$type:'string'}}).pretty(); //print by type
 ```
 ```
 19. where rating is odd
 db.movie.find({rating :{$mod: [2:1]}}).pretty();//odd rating
 ```
 ```
 20. where rating is even
 db.movie.find({rating :{$mod:[2:0]}}).pretty(); //even
 ```
