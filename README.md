Assignment 2 
Plan MongoDB-based Schema Design for a Learning Management System (LMS) application. 

This LMS will involve entities like 
* Users, 
* Courses, 
* Enrollments, 
* Modules, 
* Lessons,
* Assignments

Demonstrate Model structure and relationship for the following including 
* CRUD operations,
* find by query using aggregation pipeline

**Relationships**
Users ↔ Courses: One-to-Many (Instructors create multiple courses)
Users ↔ Enrollments: One-to-Many (Users enroll in multiple courses)
Courses ↔ Enrollments: One-to-Many (Courses have multiple enrollments)
Courses ↔ Modules: One-to-Many (Courses have multiple modules)
Modules ↔ Lessons: One-to-Many (Modules have multiple lessons)
Courses ↔ Assignments: One-to-Many (Courses have multiple assignments)


**Get**

db.enrollments.find({userID: 2}) 

db.enrollments.find({userID: 2}).count();

db.enrollments.aggregate([{$match: {"courseID": {$eq: "c2"}}},{$group: {_id: {userId: "$userID"}, TotalEnrollments : {$sum:1}}}]);


**Insert**

db.enrollments.insertOne({"enrollmentID": "E7", userID: 2, courseID: "c1"});

db.enrollments.insertMany([{"enrollmentID": "E8", userID: 1, courseID: "c1"},{"enrollmentID": "E9", userID: 1, courseID: "c2"}]);



**Update**

db.enrollments.updateOne({enrollmentId: "E1"},{$set: {courseID: "c2"}});

db.enrollments.updateMany({userID: {$eq: “2”}},{$set: {courseID: "c1"}});



**Delete**

db.enrollments.deleteOne({"enrollmentID": "E7"})

db.enrollments.deleteMany({"userID": 1})


**Aggregation**

db.enrollments.aggregate([{$match: {"courseID": {$eq: "c2"}}}]);

db.enrollments.aggregate([{$match: {"courseID": {$eq: "c2"}}},{$project: {"_id": 0,"enrollmentId": 1, "userID": 1, "courseID": 1}}]);

db.enrollments.aggregate([{$match: {"courseID": {$eq: "c2"}}},{$project: {"_id": 0,"enrollmentId": 1, "userID": 1, "courseID": 1}},{$sort: {"userID": -1}}]);

db.enrollments.aggregate([{$match: {"courseID": {$eq: "c2"}}},{$project: {"_id": 0,"enrollmentId": 1, "userID": 1, "courseID": 1}},{$sort: {"userID": -1}},{$count: "total"}]);

**Lookup**
db.enrollments.aggregate([{$match: {"courseID": {$eq: "c2"}}},{$lookup: {from: "courses", localField: "courseID", foreignField: "courseID", as: "courseDetails"}}]);





