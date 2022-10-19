# Microservice Architectures in Java with Eureka

- [Microservice Architectures in Java with Eureka](#microservice-architectures-in-java-with-eureka)
  - [Intro](#intro)
  - [What are Microservices?](#what-are-microservices)
    - [In short](#in-short)
    - [Monolithic versus Microservices](#monolithic-versus-microservices)
  - [What are the benefits of using a microservices architecture?](#what-are-the-benefits-of-using-a-microservices-architecture)
  - [How do you implement microservices in a Java stack?](#how-do-you-implement-microservices-in-a-java-stack)
  - [References](#references)

## Intro

This research document will mainly focus about microservice architectures, the main problem of service discovery, and the solution Netflix Eureka provides for a Java stack.

The problem will first be laid out and explained, which will be followed by sub-questions, finally leading up to a proof of concept with the soluton integrated into it.

_This research uses various methods and strategies from the DOT Framework, mainly the "library" and "workshop" methods._ <small>[(Meesters, 2018)](#meesters-2018)</small>

## What are Microservices?

### In short

Microservices architecture is an approach in which a single application is composed of many loosely coupled and independently deployable smaller services. <small>[(IBM Cloud Education, 2021)](#ibmcloudedu-2021)</small>

These services typically have their own technology stack and communicate with other microservices via REST APIs.

### Monolithic versus Microservices

Traditionally, applications used to be developed monolithically. This often resulted as a giant stack with tightly coupled processes running as a single service. This means that if one process experiences a spike in popularity and demand, the entire monolith needs to be scaled accordingly. As the code base grows, this become a more and more complex of a job. This complexity limits the experimentation and implementation of new ideas. A monolithic architecture also adds risk for application availability. Many processes are dependant and tightly coupled, which means an increased impact should one fail. <small>[(AWS, n.d.)](#aws-ms-nd)</small>

With a microservice architecture, a single application is composed of many loosely coupled and independently deployable smaller services. These services communicate via a well-defined interface using lightweight APIs, such as REST. Each service typically has a single function. Because they are independently run, each service can be updated, deployed, and scaled to meet the demand for specific application functionality. <small>[(IBM Cloud Education, 2021)](#ibmcloudedu-2021) [(AWS, n.d.)](#aws-ms-nd)</small>

## What are the benefits of using a microservices architecture?

Adding to the [previous header](#monolithic-versus-microservices), the main benefits to using a microservices architecture are:

- Microservices remove _single points of failure_ (SPOFs) by ensuring that an issue with one service, should not crash or affect other parts of the application.
- Individual microservices can be scaled independently to provide extra availability and capacity.
- Development teams can extend the functionaity of an application by adding new microservices without unnecessarily affecting other parts of said application.

<small>[(Microsoft Learn, 2022)](#msoftlearn-ms-2022)</small>

## How do you implement microservices in a Java stack?

For this part, a previous proof of concept will be referenced. It is a relatively simple API microservice using a service discovery and API gateway to navigate the microservice landscape.

_see [here](4-poc-dockerized-java-customer-services.md)_

There are various framework options for creating a microservices architecture in Java:

- Spring Microservices with Spring Boot <small>[(Spring, n.d.)](#springio-ms-nd)</small>
- Jersey JAX-RS REST framework <small>[(Eclipse Foundation, n.d.)](#eclipsejersey-ms-nd)</small>
- Swagger RESTful APIs <small>[(Wagner, n.d.)](#swaggerapi-ms-nd)</small>

Spring is the easiest to implement, is the Spring Boot implementation, due to its extensive documentation and easy set up. As such, Spring will be used for implementing the proof of concept.

## References

> <a name="meesters-2018"></a> Meesters, M., 2018. The DOT Framework - ICT research methods. [online] Ictresearchmethods.nl. Available at: <https://ictresearchmethods.nl/The_DOT_Framework> [Accessed 19 October 2022].

> <a name="ibmcloudedu-2021"></a> IBM Cloud Education, 2021. What are Microservices? | IBM. [online] Ibm.com. Available at: <https://www.ibm.com/cloud/learn/microservices> [Accessed 19 October 2022].

> <a name="aws-ms-nd"></a> aws.amazon.com. n.d. What are Microservices? | AWS. [online] Available at: <https://aws.amazon.com/microservices/> [Accessed 19 October 2022].

> <a name="msoftlearn-ms-2022"></a> learn.microsoft.com. 2022. What are Microservices? - Azure DevOps | Microsoft Learn. [online] Available at: <https://learn.microsoft.com/en-us/devops/deliver/what-are-microservices> [Accessed 19 October 2022].

> <a name="springio-ms-nd"></a> Spring.io. n.d. Microservices. [online] Available at: <https://spring.io/microservices> [Accessed 19 October 2022].

> <a name="eclipsejersey-ms-nd"></a> Eclipse Foundation, n.d. Eclipse Jersey. [online] Eclipse-ee4j.github.io. Available at: <https://eclipse-ee4j.github.io/jersey/> [Accessed 19 October 2022].

> <a name="swaggerapi-ms-nd"></a> Wagner, J., n.d. Building an Application: Strategies for Microservices. [online] Swagger.io. Available at: <https://swagger.io/resources/articles/building-an-application-with-microservices/> [Accessed 19 October 2022].