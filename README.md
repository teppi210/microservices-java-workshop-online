
# ✨ Building Microservice for Apache Cassandra™ ✨

[![Gitpod ready-to-code](https://img.shields.io/badge/Gitpod-ready--to--code-blue?logo=gitpod)](https://gitpod.io/#https://github.com/DataStax-Academy/microservices-java-workshop-online) 
[![License Apache2](https://img.shields.io/hexpm/l/plug.svg)](http://www.apache.org/licenses/LICENSE-2.0)
[![Discord](https://img.shields.io/discord/685554030159593522)](https://discord.com/widget?id=685554030159593522&theme=dark)

*"In this repository, you'll find everything you need related to the **Cassandra Developer Workshop Build Java Microservices for Apache Cassandra**. [The first live stream will be June 17th](https://www.youtube.com/watch?v=KAcZg6l9QTw). Past this date the `README.MD` will be updated with the recording. Feel free to bookmark this page for future reference, Enjoy"!* - The Developer Advocates Team.

![SplashScreen](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/splash.png?raw=true)

`Cassandra Developer Workshorp` are an interactive experiences. Advocates share some knowledge about  Apache Cassandra™ database and you can interact with them through chats *([youtube](https://www.youtube.com/channel/UCAIQY251avaMv7bBv5PCo-A) and [discord](https://discord.com/widget?id=685554030159593522&theme=dark))*, quizzes (menti.com), and  exercises.

Today we are creating the Todo Application with storage in to Apache Cassandra™.

![Home](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/home.png?raw=true)


# Table of Content
For simplicity all exercises instructions are listed in a single `README.MD` document. As it is quite long we provide you a table of content is provided and after each chapter you can go back to it.

| Sections  | Material Description
|---|---|
| **Slide deck** | [Slidedeck for the workshop](4-materials/presentation.pdf) |
| **1. Bootstrapping** | [Setup your environment](#1-bootstrapping) |
| **2. Run the Todo Application** | [Run the Todo Application](#2-run-the-todo-application) |
| **3. Create your Astra instance** | [Create your Astra instance](#3-create-your-astra-instance) |
| **4. Connectivity to Astra** | [Connectivity to Cassandra](#4-connectivity-to-astra) |
| **5. CRUD Repository** | [Implement CRUD Repository](#5-crud-repository) |
| **6. CRUD Repository Object Mapper** | [Test Object Mapper](#6-crud-repository-with-object-mapper) |
| **7. CRUD Repository Spring Data** | [Test with Spring DATA](#7-crud-repository-with-spring-data) |
| **8. Going Reactive** | [Going Reactive](#8-going-reactive) |

## 1. Bootstrapping

There are 2 ways to do the exercises, **locally** on your computer and with a **cloud-based IDE named Gitpod.** We recommend you to use your laptop in order to save code modifications and come back later. In both cases you should start by cloning the repository and download everything (including slides).

- ### Option A - Work with a 100% Cloud-based Environment ☁️

**✅ Open gitpod** : [Gitpod](https://www.gitpod.io/) is an IDE 100% online based on Eclipse Theia. To initialize your environment simply click on the button below.

[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/DataStax-Academy/microservices-java-workshop-online)

A new tab opens in your browser at  `https://<your_uid>.<your_region>.gitpod.io/#/workspace/microservices-java-workshop-online`. Those URL are dynamic and we cannot provide clickable links in advance. You should copy-paste `<your_uid>.<your_region>` as we will insert them in each URL  during the exercises.

**👁️ Expected output**

![SplashScreen](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/gitpod-home.png?raw=true)

**That's it.** Gitpod provides all tools we will need for today including `Maven` and exporting port `8080`. At initialization of the workspace we schedule a `mvn clean install` to download dependencies. You can still download the repository and bookmark it as all materials including slides are part of it.

- ### Option B - Work with Local Environment 💻

This part is dedicated to people will to run the exercises on their laptop. You can skip it and directly go to [2. Run the Todo Application](#2-run-the-todo-application) if you want to work with gitpod.

**✅ (local env) Clone the repository :** : With `git` or through the web UI clone the repo
```bash
# Clone the current repository
git clone https://github.com/DataStax-Academy/microservices-java-workshop-online.git

# Access the proper folder
cd microservices-java-workshop-online
```

**✅ (local env)  Install Java (JDK8+)** Pick the proper infos based on your operating system
- ![Windows](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/windows32.png?raw=true) Please use the following tutorial [Installation of the JDK on Microsoft Windows Platforms](https://docs.oracle.com/en/java/javase/11/install/installation-jdk-microsoft-windows-platforms.html#GUID-A7E27B90-A28D-4237-9383-A58B416071CA)
- ![linux](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/linux32.png?raw=true) Please use the following tutorial [Installation of the JDK on Linux Platform Platforms](https://docs.oracle.com/en/java/javase/11/install/installation-jdk-linux-platforms.html#GUID-737A84E4-2EFF-4D38-8E60-3E29D1B884B8)
- ![osx](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/mac32.png?raw=true) Please use the following tutorial [Installation of the JDK on MACOS Platforms](https://docs.oracle.com/en/java/javase/11/install/installation-jdk-macos.html#GUID-2FE451B0-9572-4E38-A1A5-568B77B146DE) or with [homebrew](https://docs.brew.sh/Installation):
```bash
brew cask install java
```

**✅ (local env) Install Maven**
- ![Windows](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/windows32.png?raw=true) Please use the following tutorial [How to install Maven on Windows](https://mkyong.com/maven/how-to-install-maven-in-windows)
- ![linux](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/linux32.png?raw=true). For CentOS you can use: `sudo yum install maven`
- ![osx](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/mac32.png?raw=true) For MacOS you can use `brew install maven`

Validate installation
```bash
mvn -v
```

**👁️ Expected output**
```bash
Apache Maven 3.6.0 (97c98ec64a1fdfee7767ce5ffb20918da4f719f3; 2018-10-24T20:41:47+02:00)
Maven home: /usr/local/Cellar/maven/3.6.0/libexec
Java version: 12, vendor: Oracle Corporation, runtime: /Library/Java/JavaVirtualMachines/openjdk-12.jdk/Contents/Home
Default locale: en_FR, platform encoding: UTF-8
OS name: "mac os x", version: "10.15.3", arch: "x86_64", family: "mac"
```

**✅ (local env)  Install an IDE**

Pick and install your favourite Java IDE. Here are some propositions without preference order.

| Tools  | Download link
|---|---|
| **Eclipse STS** | 📥[Download Eclipse Spring Tools Suite](https://spring.io/tools#main)
| **Jetbrains IntelliJ** | 📥[Download IntelliJ](https://www.jetbrains.com/idea/download/index.html)
| **Core Eclipse** | 📥[Download Eclipse](https://www.eclipse.org/downloads/)
| **Visual Studio Code** | 📥[Downlowd Visual Code](https://code.visualstudio.com/Download)


[🏠back to table of content](#table-of-content)

## 2. Run the Todo Application

**TodoMVC** is a fabulous community contribution that helps developers compare frameworks on the basis of actual project code, not just claims and anecdotes. Michael Mahemoff. TodoMVC is an immensely valuable attempt at a difficult problem - providing a structured way of comparing JS libraries and frameworks.

![TodoMVC](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/todomvc.png?raw=true)

**✅ Step 2a. Test todoMVC application** : Access the [http://todomvc.com/](http://todomvc.com/) website and test one application with the framework of your choice.

**Todo-Backend** is a shared example to showcase backend tech stacks. The Todo-Backend project defines a simple web API spec - for managing a todo list. Contributors implement that spec using various tech stacks. Those implementations are cataloged below. A spec runner verifies that each contribution implements the exact same API, by running an automated test suite which defines the API.

![TodoBackend](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/todobackend.png?raw=true)

There are multiple free implementations available already. Some implementations provide endpoints to be tested in `heroku`. [Heroku provide free hosting for a Java application but this is on-demand](https://devcenter.heroku.com/articles/deploying-spring-boot-apps-to-heroku). With `Heroku` The application will be sleeping until you access the endpoint. So it will take 30s for the first person to have the application running. Among the available free endpoints we can list:
- `Endpoint#1` : [https://todo-back-springboot220-java12.herokuapp.com/todos](https://todo-back-springboot220-java12.herokuapp.com/todos)
- `Endpoint#2` : [https://todo-quarkus.herokuapp.com/todos](https://todo-quarkus.herokuapp.com/todos)
- `Endpoint#3` : [https://todo-backend-micronaut.herokuapp.com/todos](https://todo-backend-micronaut.herokuapp.com/todos)

**✅ Step 2b. Test TodoBackEnd Spec Runner** : Locate the [spec runner](https://www.todobackend.com/specs/index.html) and use one of the `endpoints` listed below to evaluate if API matchs the requirements. To do so copy-paste one URL and click `Run Tests`.

![TodoBackendTest](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/todobackend-runtest.png?raw=true)

**👁️ Expected output**

![TodoBackendOuput](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/todobackend-output-host.png?raw=true)

**Note:** *During the live stream you will be hundreds testing the same endpoints so - maybe - we could hit some issues = race conditions.*

**✅ Step 2c. Test TodoBackEnd Web Client** : todoBackend.com provides a [client](https://www.todobackend.com/client/index.html) to work with the API. As before pick one of the `endpoints` listed before and try the client.

![TodoBackendClient](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/todobackend-runclient.png?raw=true)

**👁️ Expected output**

![TodoBackendClient](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/todobackend-output-client.png?raw=true)

Our mission withing the next hour is to implement the *backend API* and store  data into Apache Cassandra™. We have you covered by providing the skeleton of the application.

**✅ Step 2d. Start Backend API** : By using a maven command or run application in your IDE

```bash
# Build the project without tests (you did not implemented them yet TDD baby !)
mvn clean install -Dmaven.test.skip=true

# Navigate to the proper folder
cd todobackend-cassandra/

# Start the backend API
mvn spring-boot:run
```

**👁️ Expected output**
```bash
[...]
INFO] ------------------------------------------------------------------------
[INFO] Reactor Summary for Spring microservices with Apache Cassandra 1.0-SNAPSHOT:
[INFO] 
[INFO] Spring microservices with Apache Cassandra ......... SUCCESS [  4.115 s]
[INFO] + microservice-1-common ............................ SUCCESS [  8.893 s]
[INFO] + microservice-2-spring-boot ....................... SUCCESS [  3.504 s]
[INFO] + microservice-3-spring-data ....................... SUCCESS [  1.369 s]
[INFO] + microservice-4-spring-webflux .................... SUCCESS [  0.311 s]
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  18.701 s
[INFO] Finished at: 2020-06-15T13:08:57Z
[INFO] ------------------------------------------------------------------------
```

```bash
 ________                __      __ __           .__                   
 \______ \   _______  __/  \    /  \  | __  _____|  |__   ____ ______  
  |    |  \_/ __ \  \/ /\   \/\/   /  |/ / /  ___/  |  \ /  _ \\____ \ 
  |    `   \  ___/\   /  \        /|    <  \___ \|   Y  (  <_> )  |_> >
 /_______  /\___  >\_/    \__/\  / |__|_ \/____  >___|  /\____/|   __/ 
         \/     \/             \/       \/     \/     \/       |__|    

 Backend API implementation of todobackend.com
 We are using SpringBoot and Apache Cassandra
 The application is started at http://localhost:8080  

14:54:54.773 INFO  com.datastax.sample.TodoBackendApplication         : Starting TodoBackendApplication on clunhost with PID 75757 (/Users/cedricklunven/dev/WORKSPACES/DATASTAX/microservices-java-workshop-online/wkshop-microservice-2-spring-boot/target/classes started by cedricklunven in /Users/cedricklunven/dev/WORKSPACES/DATASTAX/microservices-java-workshop-online/wkshop-microservice-2-spring-boot)
14:54:54.775 INFO  com.datastax.sample.TodoBackendApplication         : No active profile set, falling back to default profiles: default
14:55:03.604 INFO  com.datastax.sample.TodoBackendApplication         : Started TodoBackendApplication in 1.075 seconds (JVM running for 1.492)
```

**✅ Step 2e. Show Api Documentation** : through your browser

- 💻 If you are on your **laptop** : open a browser and navigate to [http://localhost:8080](http://localhost:8080)

- ☁️ If you are on **gitpod** : a popup may show up and redirect you to `https://8080-<your_id>.<>your_region.gitpod.io` as you can see this an alias for port `8080`.

**👁️ Expected output**

![TodoBackendClient](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/backend-doc.png?raw=true)

**✅ Step 2f. Test Backend API** :using the OpenAPI generated documentation. You can open the `GET` bloc labeled `/api/v1/todos` and pick `Try It Out`. Then locate `Execute` to test the API  and get a few results.

**👁️ Expected output**

![TodoBackendClient](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/todobackend-swagger-test.png?raw=true)

**✅ Step 2g. Test our Backend API against the spec runner** : This REST API store data **In memory** but is 100% valid. We can validate by testing the same spec runner as before.

- 💻 If you are on your **laptop** open a browser and navigate to [https://www.todobackend.com/specs/index.html?http://localhost:8080/api/v1/todos](https://www.todobackend.com/specs/index.html?http://localhost:8080/api/v1/todos)

-  ☁️ If you are on **gitpod** : a popup may show up and redirect you to `https://8080-<your_id>.<>your_region.gitpod.io/api/v1/todos`.

**👁️ Expected output**

![TodoBackendClient](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/realbackend-test.png?raw=true)

**✅ Step 2h. Test our Web Client UI against our Backend API** : This is neat, the client and spec runner both work even with URL like `localhost` because this is some `javascript` code executed at client side.

Back the client UI change the URL to match you backend URL :
- 💻 If your work locally : [https://www.todobackend.com/client/index.html?http://localhost:8080/api/v1/todos](https://www.todobackend.com/client/index.html?http://localhost:8080/api/v1/todos)
 

- ☁️ If you are using gitpod `https://www.todobackend.com/client/index.html?https://8080-<your_id>.<your_region>-eu01.gitpod.io/api/v1/todos`

**👁️ Expected output**

![TodoBackendClient](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/backend-ok.png?raw=true)

*Ok I changed a little bit the values but now this is working....* 

![TodoBackendClient](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/welldone.png?raw=true)

[🏠 Back to Table of Content](#table-of-content)

## 3. Create your Astra instance

`ASTRA` service is available at url [https://astra.datastax.com](https://astra.datastax.com/)

**✅ Step 3a.Register (if needed) and Sign In to Astra** : You can use your `Github`, `Google` accounts or register with an `email`

- [Registration Page](https://astra.datastax.com/register)

![TodoBackendClient](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/astra-create-register.png?raw=true)

- [Authentication Page](https://astra.datastax.com/)

![TodoBackendClient](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/astra-create-login.png?raw=true)


**✅ Step 3b. Fill the Create New Database Form** : As you don't have have any instances the login will route through the instance creation form. You will find below which values to enter for each field.

- *Initialization Form*
![TodoBackendClient](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/astra-create-2.png?raw=true)


- **Set the Compute Size**: For the work we are doing please use `Free tier`. You instance will be there forever, free of charge. If you already have a free tier db that you created in a previous workshop (`killrvideo`) you can reuse it.

- **Select region**: This is the region where your database will reside physically (choose one close to you or your users). For people in EMEA please use `europe-west-1` idea here is to reduce latency.

- **Fill in the database name** - Proposed value `dev-workshop-db`. You can use any alphanumeric value it is not part of the connection fields. Now it will be part of a file downloaded later and you should avoid capital letters.

With the 3 fields below you can pick any name, simply REMIND them, they will be required both to connect `and do the exercises.

- **Fill in the keyspace name** - Proposed value `todoapp` (no spaces, alpha numeric)

- **Fill in the user name** - `todouser`. Note the user name is case-sensitive. Please use the case we suggest here.

- **Fill in the user password** - `todopassword`. Fill in both the password and the confirmation fields. Note that the password is also case-sensitive. Please use the case we suggest here.

- **Launch the database**. Review all the fields to make sure they are as shown, and click the Launch Database button.

**👁️ Expected output**

![TodoBackendClient](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/astra-create-3.png?raw=true)

**✅ Step 3c. View your Database and connect** : View your database. It may take 2-3 minutes for your database to spin up. You will receive an email at that point. But, go ahead and continue with the rest of the exercise now.

**👁️ Expected output**

*Initializing*
![TodoBackendClient](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/astra-create-4.png?raw=true)

*Database is ready*
![TodoBackendClient](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/astra-create-5.png?raw=true)

**✅ Step 3d. Open DataStax Studio** : Locate  `Launch Developer Studio` on the bottom left part of the screen and click on `Launch now`. Please enter the same credentials you used for instance creation.

![TodoBackendClient](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/launch-studio.png?raw=true)

- **Fill in the Database User name** - `todouser`. Note the user name is case-sensitive. Please use the case we suggest here.

- **Fill in the password** - `todopassword`. Fill in both the password and the confirmation fields. Note that the password is also case-sensitive. Please use the case we suggest here.

**👁️ Expected output**

![TodoBackendClient](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/astra-create-6.png?raw=true)

**✅ Step 3e. Import a notebook** : DataStax studio should now be opened.

![TodoBackendClient](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/launch-studio-home.png?raw=true)

- Download locally the file `datastax-studio-notebook.tar` located in `z-materials/notebooks/datastax-studio-notebook.tar` [here](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/notebooks/datastax-studio-notebook.tar?raw=true)

- Import the file in studio with a drag and drop in the Datastax studio window

*Importing*
![TodoBackendClient](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/launch-studio-import.png?raw=true)

*File is now open*
![TodoBackendClient](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/launch-studio-open.png?raw=true)

![TodoBackendClient](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/welldone.png?raw=true)


[🏠 Back to Table of Content](#table-of-content)


## 4. Connectivity to Astra

With `Cassandra-as-a-service` ready let's connect from our application

**✅ Download the secure connect bundle** : On the home page of your DB first refresh (the download link will be valid 5 min we want to be sure we don't reach the timeout). Locate link `Download secure connect bundle` and click. You should download a file named `secure-connect-<your_db_name>.zip`. Please remind the location of the file.

![TodoBackendClient](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/astra-create-7.png?raw=true)

**✅ Upload the zip in `gitpod` ** :



**✅ Fix unit test `ConnectivityToAstraExplicitTest.java` ** :


- Run the test
```bash
mvn test -Dtest=com.datastax.samples.astra.ConnectivityToAstraExplicitTest#should_connect_to_Astra_static
```




**✅ Fix unit test `ConnectivityToAstraWithConfTest.java` ** :



- Run the test
```bash
mvn test -Dtest=com.datastax.samples.astra.ConnectivityToAstraWithConfTest#should_connect_to_Astra_withConfig
```

**✅ Fix unit test `CreateSchemaInAstraTest` ** :


```sql
CREATE TABLE todoapp.todo_tasks (
    uid uuid PRIMARY KEY,
    completed boolean,
    offset int,
    title text
);
```

- Run the test
```bash
mvn test -Dtest=com.datastax.samples.astra.CreateSchemaInAstraTest#should_create_expected_table
```


**✅ Check that the table `todoapp.todo_tasks` now exist ** :

**✅ Create bean `CqlSession` in the application ** :


[🏠back to table of content](#table-of-content)

## 5. CRUD Repository

**✅ Fix Unit Test `CrudWithSimpleStatementTest` ** :

**✅ Change injection dependency in `TodoListRestController` ** :


[🏠back to table of content](#table-of-content)

## 6. CRUD Repository with Object Mapper

**✅ Change dependency injection in `TodoListRestController` ** :

 
[🏠back to table of content](#table-of-content)

## 7. CRUD Repository with Spring Data

**✅ Cassandra Configuration ** :

**✅ Change dependency injection in `TodoListRestController` ** :


[🏠back to table of content](#table-of-content)

## 8. Going Reactive

**✅ Location project 2

**✅ Change dependency injection in `TodoListRestController` ** :


[🏠back to table of content](#table-of-content)

THE END.





