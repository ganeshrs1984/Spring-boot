Spring Boot RestService API
-----------------------------

Developed a Profile Restservice 

GET Method -  fetch profile details by phone number and render JSON reponse
POST Method - Insert Profile details 

Technology Used
----------------

 Spring Boot
 JUnit - Test case
 H2 Inbuit memory DB
 Gradle
 Java 8


Code Walkthrough
-----------------

1 Controller/Service.<br>
2 CommonUtil is a static class which helps to validate the input.<br>
3 @Valid/Command Object and @RestControllerAdvice- validates the input POST object and incase of any Exception, ProileAdvice class.  with @Advice annotation will take care of sending the Exception Response.<br>
4 DAO - Select and Insert process in H2 SQL.<br>
5 IBatis - ORM Tool.<br>
6 messages.properties INTERNATIONALIZATION feature - Display message from property file<br>


GET Method   - Get Profile details by phone number
----------

eg: <br>
URL - http://localhost:8080/profile-services/profile/6121111111  
URL - http://localhost:8080/profile-services/profile/6121111112  
URL - http://localhost:8080/profile-services/profile/6121111113

POST
----

URL - http://localhost:8080/profile-services/insert

Phone number is the primary Key - Will not allow duplicate inserts

Existing Phone Numbers in the database- 6121111111,6121111112,6121111113 

API takes care of below validation 
------------------------------------

phone should be numeric <br>
name should not be empty <br>
exp should be > 0 <br>
email : email format <br>
tech should not be empty <br>


1) Input JSON :  Duplicate 
------------

{"phone":"6121111111","name":"Raga","exp":10,"email":"test1@gmail.com","tech":"Java Groovy"}


Sample Output
--------------

{
"errorId": "Already Exist",
"errorMessage": "6121111111- Account Already Exist"
}

2) Input JSON :  Incorrect PhoneNumber 
------------

{"phone":"612111111A","name":"Raga","exp":10,"email":"test1@gmail.com","tech":"Java Groovy"}


Sample Output
--------------
 
{
"errorId": "INVALID_PHONE",
"errorMessage": "Given PhoneNumber is invalid"
}

2) Input JSON :   Valid Input
------------

{"phone":"6121111127","name":"Sam","exp":14,"email":"test1@gmail.com","tech":"Java Groovy"}


Sample Output
--------------
 
{
"name": "Sam",
"phone": "6121111127",
"exp": 14,
"email": "test1@gmail.com",
"tech": "Java Groovy"
}
