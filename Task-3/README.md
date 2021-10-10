Building a Microservices based E-Commerce App


I’ll create a simplified store based on microservice architecture. This is going to be a headless backend application without a frontend. However, testing is possible with any REST APIclient, e.g., by using CURL or POSTMAN. In order to prepare for deployment, we need to make several important choices.

Domain-Driven Design
Since eCommerce apps are extremely complex and they keep evolving, it makes sense for us to follow a domain driven design here. With a domain driven design, we have specific teams and stakeholders responsible for each services.The first and foremost task is to find the core, supporting, and generic subdomains of the application. In DDD terms, it is called Strategic Design.

Kindly see the Developign-eCommerce-app-with-a-domain-driven-design image.

our code is now divided into a bunch of well defined microservices. our image above shows the top 10 microsevices that you would absolutely need in order to build a high performing, scalable ecommerce.

Database per Microservice
When you are interested in a short-term gain (like boosting initial development velocity), a single database is a better choice. But for long-term benefits, what microservices is all about, I’ll use the database-per-microservice approach, where both the Product and Customer microservices will have separate databases. In this case study, we need an OLTP database supporting the ACID transnational guarantee; any SQL database or a handful of NoSQL ones may apply here. However, I will choose MongoDB, the most popular among NoSQLs and the most widely utilized document database. Since version 4.0, MongoDB also offers a cross-table ACID transactional guarantee with its WiredTiger storage engine. As described in detail here, managing transactions in microservices offers completely new sets of challenges. For our demo, we will accept the eventual consistency and won’t implement the distributed transaction.


Tech Stack
I’ll use Node.JS for API design and Python for server side programs. But we can use any language if necessary as this is one of the interesting benefits of MicroService Design. If you understand what performance you can get from a particular language or a server framework, you are no longer bound by limitations to only use a few of them. In the age of cloud computing, because of the microservice design, we can use any server side framework depending on workload and criteria. 


Cloud-Native Infrastructure 
In the microservice architecture, we have to deal with common issues like service discovery, load balancers, scaling, and fault tolerance. we are going to use infrastructure, like Docker and Kubernetes, to address this.


Synchronous Communication
I will start with synchronous communication using REST because it is simple to implement and a popular way of communication.


Here we are covering only the Customer and Product microservices. Microservice architecture follows the single responsibility principle and each service handles only one specific task.
In this demo, the Customer microservice will deal with every customer-related action: Create, Update, Delete, and Feed customers.It will do much more in a real e-commerce shop (like activate/deactivate customers, onboarding, etc.). Our Customer microservice will only do the basic things for the sake of simplicity.
Similarly, the Product microservice will manage everything regarding an order: Create, Read, Update and Delete orders. As I’ve already mentioned, they will have a separate data store (database/table/collection).
The frontend (web, desktop, and mobile) or the REST clients will connect with these microservices via REST API, i.e., REST API will serve as the contact between the frontend and the backend.The Order microservice in our example needs to communicate with the Customer one. When a customer orders via the Order frontend, an Order is created in the Order database. Then it uses the “customerOrders” API to link the Order with the Customer. The Customer microservice will then maintain the link between the Customer and Order.

Implementation
This use case will employ API-driven development, meaning we will first define the microservices API. It will then enable individual teams to work on the implementation without waiting for others. We’re going to apply the Swagger 2.0 REST API specification.

System requirements:
NodeJs
Python
MongoDB (Local or Atlas cluster);
Docker;
Kubernetes (kubectl CLI);
An AWS Account;
AWS CLI Version 2;
Cache Service
