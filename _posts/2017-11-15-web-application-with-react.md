---
layout: post
title:  "Web Application with React.js, Express.js and MongoDB"
date:   2017-11-15
categories: mediator feature
image: /assets/article_images/2017-11-11-instagram-like-app-with-react-native/web-app-background.jpg
---

I recently came across a design and implementation question, the problem is as below:


> Design and implement a web application that collects local weather data from a simulated IoT device via
a REST API. The web application should save the data in a database and display it in an interactive
visualization. Assume the IoT device reports the device ID, timestamp, temperature, and humidity.
Assume new data is available every 60 seconds.

# Let's analyze these problem:

Design and implement a web application that collects local weather data from a simulated IoT device via a REST API.

* The web application should save the data in a database and display it in an interactive visualization.
* Assume the IoT device reports the device ID, timestamp, temperature, and humidity.
* Assume new data is available every 60 seconds.

These are the major requirements that will affect the choice of framework that I am going to use.

# Analysis Result

Based on the requirement, I have to decide which framework should I used to develop the web application.

## Front end
* **Options**: React, AngularJS
* **My choice**: React
* **Reason**: React has better performance than Angular due to React's implementation of virutal DOM. The web application I am designing require constantly updating user interface from the database. With React, this increase the efficiency of rendering the web app, as it only rerun the part that we make changes.

## Back end
* **Options**: express.js, meteor.js
* **My choice**: express.js
* **Reason**: Meteor provides full stack development framework for developer which means backend development framework is also available. However, some of the libraries are stopped develop and maintain by the community, which will cause inconvenient in the future. Since I have decided to use react as my front end framework, why bother working with meteor which provide full stack framework. Plus express.js is much more light weighted than meteor.js.

## Databases
* **Options**: mongodb, MySQL
* **My Choice**: mongodb
* **Reason**: We know that the database going to grow very large as time goes as every 60 seconds new data will be obtained and stored in database. And we will need to constantly read and write from the database in order to do so and to update the UI. Mongodb is what we looking for. It has the capability to store large volumes of data. And since in 75F, Cloud services is very important to process the data. Mongodb can load high volume of data and givve us lots of flexibility and availability in a cloud based environment. It has built in sharding solutions that make it easy to partition and spread out data across multiple servers. It is also easy to scale the database to connect ot other hardware or in cloud without the need of additional software.

# Result
Before we run the API server that gets the data from mongoDB server, we try run the web application by using the following command

```Shell
$ npm install
$ npm start
```  

We will get this at [http://localhost:3000](http://localhost:3000)

![](https://github.com/clementpeihengtan/clement-tph/blob/gh-pages/assets/article_images/2017-11-15-web-application-with-react/Before-server.png?raw=true)

After running the server by running the command below

```Shell
$ node server.js
```

We will be able to see the result being populated in the website and the graph is being created

![](https://github.com/clementpeihengtan/clement-tph/blob/gh-pages/assets/article_images/2017-11-15-web-application-with-react/After-server.png?raw=true)

We can get a look at the data from mongodb at [http://localhost:3001/api/data](http://localhost:3001/api/data) which look like this

![](https://github.com/clementpeihengtan/clement-tph/blob/gh-pages/assets/article_images/2017-11-15-web-application-with-react/api.png?raw=true)

For more details about the code. Look at my [repo](https://github.com/clementpeihengtan/Weather_App) on Github.
