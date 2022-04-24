```
Create a Employee Collection add 5 documents:
Example:
{empno:111,ename:”Deepali Vaidya”,sal:40000.00,dept:{deptno12,dname:,”Hr”,dloc:”Mumbai},
Desg:”Analyst”,mgr:{name:”Satish”,num:111},project:[{name:”Project- 1”,Hrs:4},{name:”project- 2”,Hrs:4}]}
```

    1. All Employee’s with the desg as ‘CLERK’ are now called as (AO) Administrative Officers. Update the Employee collection for this.
>db.Emp.updateMany({Desg:'Cleark'},{$set :  {Desg:'AO'} });




    2. Change the number of hours for project-1 to 5 for all employees with designation analyst.

 >db.Emp.updateMany({ 'project.0.name':"Project-1" , Desg:'Analyst' } , {$set : { 'project.0.Hrs':5} } );



    3. Add 2 projects project-3 and project-4 for employee whose name starts with ”Deep” with 2 hrs

>db.Emp.updateMany({ename:/^Deep.*/},{$push:{project:{$each:[{name:'project-3' , Hrs:2},{name:'project-4' , Hrs:2}]}}});




    4. Add bonus rs 2000 for all employees with salary > 50000

>db.Emp.updateMany({sal: {$gt : 50000 }},{ $inc : { sal :  2000 } });





    5. Add bonus rs 1500 if salary <50000 and salary > 30000

>db.Emp.find({sal: {$gt : 30000 } ,sal: {$lt : 50000 } }).pretty().limit(1);









    6. increment bounus by 1000 for all employees if salary <=30000

>db.Emp.updateMany({sal:{$lte : 50000 } },{ $inc : { sal :  1000 } });




    7. Change manager name to Tushar for all employees whose manager is currently “satish”
And manager number to 3333

> db.Emp.updateMany({'mgr.name':"Satish" },{ $set : { 'mgr.name' : "Tushar" } });



    8. Increase salary of all employees from “purchase department” by 15000

> db.Emp.updateMany({'dept.dname':"Sales" },{ $inc : { sal : 15000 } });



    9. Decrease number of hrs by 2 for all employees who are working on project-2

> db.Emp.updateMany({ 'project.1.name':"Project-2" },{ $inc : { 'project.1.Hrs' : -2 } });





    10. Delete project-2 from all employee document if they are working on the project for 4 hrs.


>db.Emp.update( { 'project.Hrs' : 4 , 'project.name' : "project- 2"  },
   { $pull :{ 'project' : { name:'project- 2' , Hrs:4 } } } )



    11. Change the salary of employees to 10000 only if their salary is < 10000

> db.Emp.updateMany({ sal : {$lt : 10000} } , {$set : { sal : 10000 } } );







    12. Increase bonus of all employees by 500 if the bonus is <2000 or their salary is < 20000 or if employee belong to sales department

> db.Emp.updateMany({  $or: [ { sal : {$lt : 20000}  }, { 'dept.dname' : "Sales" } , {bonus : {$lt : 2000}} ] } , {$inc : { bonus : 500 } } );





    13. Add 2 new project at position 2 for all employees with designation analyst or salary is equal to either 30000 or 33000 or 35000


> db.Emp.update(  { $or: [  { Desg:"Analyst" } , { sal : {  $in :[30000,33000,35000] } }  ] },
...    { $push :{ 'project' : { $each:[{ name : "Project-50", Hrs : 50 }, { name : "Project-60", Hrs : 60 }] , $position : 1 } } } );




    14. Delete last project of all employees with department name is “HR” and if the location is Mumbai

> db.Emp.update({  $and: [ { 'dept.dloc' : "Mumbai" }, { 'dept.dname' : "Hr" } ] },  { $pop : {'project' : 1} } );








    15. 	Change designation of all employees to senior programmer if they are working on name:”Project-1” for 4 hrs

> db.Emp.update( { $and: [ { 'project.name':"Project-1" }, {'project.Hrs' : 4 } ] },  { $pop : {'project' : 1} } );








    16. Add list of hobbies in all employees document whose manager is Rajan or Revati

> db.Emp.updateMany(  { 'mgr.name':{$in:['Rajan','Revati']} },  { $push : { Hobbies : {  $each: ['swimming','Cycling','Soccer'] }  } } );
{ "acknowledged" : true, "matchedCount" : 0, "modifiedCount" : 0 }





    17. Add list of skillset in all employee documents who are working on project-4 for 3 hrs or on project-3 for 4 hrs

>db.Emp.update({ $or: [  { $and:[{ 'project.name':"Project-3" },{'project.Hrs':4}] } , { $and:[{ 'project.name':"Project-4" },{'project.Hrs':3}] } ] } , { $push : { Skillset : {  $each: ['java','C++','Reactjs'] }  } } );





    18. Add a new hobby as blogging at 3 position in hobbies array for all employess whose name starts with R or p and ends with j or s

>db.Emp.update(  { ename:/^[Rp].*[js]$/ },  { $push : { Hobbies : {  $each: ['Cricket']  , $position : 2 } } } );



    19. Increase salary by 10000 for all employees who are working on project-2 or project-3 or project-1 .Decrease bonus by 1000 rs And increase salary by 1000rs for all employees whose department location is Mumbai

>db.Emp.update(  { $or: [ { 'project.name':"Project-3" }  ,  { 'project.name':"Project-2" } , { 'project.name':"Project-1" } ] },  { $inc : {sal : 10000} } );


> db.Emp.updateMany(  {'dept.dloc':'Mumbai'} ,  { $inc : {bonus : -1000},$inc : {sal : 1000} } );







    20. Remove all employees working on project-1

>db.Emp.deleteMany({ 'project.name':"Project-1" });


    21. Replace document of employee with name “Deepak to some new document

>db.Emp.replaceOne(
{ ename:"Roses" } ,
{

        empno : 125,
        ename : "Clara",
        sal : 39000,
        dept : {
                deptno : 13,
                dname : "Admin",
                dloc : "Satara"
        },
        Desg : "AO",
        mgr : {
                name : "Sham",
                num : 11
        },
        project : [
                {
                        name : "Project-10",
                        Hrs : 9
                },
                {
                        name : "Project-11",
                        Hrs : 10
                }
        ],
        Hobbies : [
                "swimming",
                "Cycling",
                "Modelying",
                "Soccer"
        ]
}
);











    22. Change skill python to python 3.8 for all employees if python is there in the skillset

>db.Emp.updateMany(
    {Skillset : 'java'}, 
    { $set: {'Skillset.$':'Java 8'}});





    23. Add 2 skills MongoDb and Perl at the end of skillset array for all employees who are working at Pune location


> db.Emp.update({ 'dept.dloc':"Pune" } , {$push :{ Skillset :  { $each: ['mongodb','perl'] } } } );





    24. Delete first hobby from hobby array for all employees who are working on project-1 or project-2

>db.Emp.update({ $or: [ { 'project.name':"Project- 1" },{ 'project.name':"Project- 2" }]}, {$pop :{ Hobbies :  -1 } } );







    25. Delete last hobby from hobbies array for all employees who are working on project which is at 2 nd position in projects array for 4 hrs

>db.Emp.update({'project.1.Hrs' : 4}, {$pop :{ Hobbies :  1 } } );


    26. Add 2 new projects at the end of array for all employees whose skillset contains Perl or python
>db.Emp.updateMany( {
	Skillset :{
		$in:['perl','mongodb']
		}
	}, {
	$push :{
		project : {
			$each: [
				{name:"Project-22" , Hrs:44 } ,
					{name:"Project-21" , Hrs:42 } ]
						}
							}
								} );





    27. Change hrs to 6 for project-1 for all employees if they working on the project-1 for < 6 hrs. otherwise keep the existing value.


	
>db.Emp.update( {
	'project.Hrs' : {$lt : 6} , 'project.name' : "Project- 1"  },
 { $set :{ 'project.$.Hrs' : 6 	}	} );















