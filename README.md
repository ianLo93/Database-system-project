# Database-system-project
JIANHUI LU, WEIRAN YUAN

RIN: 661752675, 661677444

## APP User Interface

![HOME](https://image.ibb.co/eNZgH6/homepage.png)
![Search](https://image.ibb.co/btcOVR/searchui.png)
![Detail](https://image.ibb.co/n3hxc6/schooldetail.png)

## Used Datasets

The two datasets we use are terrorist attacks data and college information data as we demonstrated in the memo. There are 135 schemas in the terrorist attacks data, which includes incident information, incident location, attack information, weapon information, target/victim information, perpetrator information and consequences. We narrow down the scope of the dataset from global to US domestic since our application do not use any of the other data and the US terrorism data is large enough. The college data comes from a score rating system. It includes most of the colleges in US includes those not verified by the accrediting institutions. There are 27 schemas in the colleges datasets including college overall information, location information and the accrediting agencies information. We provided source for the two datasets and the Githud repository and google drive link where we preserve these datasets.

Source of terrorism data: http://www.start.umd.edu/gtd/

Source of colleges data: https://catalog.data.gov/dataset/college-scorecard

Githud repository: https://github.com/ianLo93/Database-system-project

Google drive (Store USTerrorismData.csv): https://drive.google.com/file/d/1QpVNxwgVBsfWxXk85EO2lw1HRghi4oMl/view?ts=5a3334c4

## Application
Our group chose to make a web application using JSP and use PostgreSQL and MongoDB as the database of the three tiers application. We store terrorism data in the MongoDB since most of the schemas do not really have functional dependencies with each other, we can split them into several tables but these tables don’t make sense as relational models, like even if we specified an attack type, we still can’t sure what kind of weapons the terrorists used. Hence, using a non-relational model should be more appropriate for the dataset. We split the college dataset into three tables, respectively college overall information, geographical information and the accredition institutes table. 

We designed an interface of our web application with a navigation bar on the top and some contact and relevant information at the bottom. Two class of buttons on the homepage, one is to search for the information of the schools, it asks user to provide some basic information such as school name, city and zip code, it will provide an overall information to the users to have a basic understanding of the school, we will also provide historical terrorists attack information in that area, if the city the school placed have ever experienced some attacks, our app will provide that information and the detail is accessible if the user click the link. The other button is for users who wants to explore more about terrorist attacks in United States, it also needs users to provide some information so that queries can start to work on the database and several results will come out. 

### Data import
We use Java and JSP to build the web application, we first created three table schemas in Postgres database to store the college data, then we use a java program to clean data and insert them into the tables. The program works pretty well, we got a good result of three tables. The ER diagram is provided in the githud file.

Run 'PostgresDB.java' to import college data. 

Make sure that "CollegeData2.1.csv" is in the same directory as in Eclipse workspace. Actually we have included our data file in the source code zip file.
 
MongoDB is in BSON format, it needs a schema as the key and a value as the value. We directly import our datafile into the database named "databaseproject" in mongoDB using the following command line. Before that, you should have been set up a database called "databaseproject" and make sure that tha USTerrorismData.csv is in the same file as in the directory that can call "mongo" command in your computer.

mongoimport -d databaseproject -c terrorism --type csv --file USTerrorismData.csv --headerline

### Environment Setup
Now we have all the data in the database, we can implement some java code on JSP file to perform the use cases of our application. Our web application passes request values to the next page and responds with a new HTML page to the user, JavaBean has been used to receive and store the request from the previous page and the JSP file performs some function on these request to derive some results. 

After we connect the Postgres database and MongoDB (Use 'ConnectMongodb.java' and 'ConnectPostgre.java', no need to run, we've implemented in the code), we will be able to access the data from the database and respond data to the users. If the user try to lookup some school information, he can explore our Postgres database to get data from the combination of our three tables, our program will construct a query base on what the user request and send it to the database, then the result will display to the users. If any historical terrorist attacks is detected, we will also send the information about these terrorist attacks and help users to have a good preview of the school. If this arose the interest of the user, he can try to explore our terrorism data in the MongoDB dataset, which contains more information about historical terrorist attacks, he can explore any year and anywhere in US.

The application is run on a virtual server called 'Tomcat' which the users need to install. We make our program on Eclipse. You need to installed a java jar ‘postgresql-42.1.4.jar’ under the ‘WEB-INF/lib’ to have connection with the Postgres database, and you also need mongodb-driver-36.0.jar and mongodb-java-driver-36.0.jar to connect with the mongoDB database. Two classes need to implement to get the connection to these database, one is ‘ConnectMongodb.java’ and the other is ‘ConnectPostgres.java’, we have included them in our zip file. When all these things are ready, you can right click ‘Homepage.jsp’ under WebContent folder in Eclipse IDE and Run As -> Run on Server or just go to http://localhost:8080/DBprojectCode/Homepage.jsp (If you can't open, try the newest code on Github) you can get access to our web application. 

Have fun!

## Other interfaces
![terrorism](https://image.ibb.co/b0HFC6/explore_Terro.png)
