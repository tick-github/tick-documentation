# Portfolio
 by Erik Van de Laar (code-syl)

## Table of Contents
- [Portfolio](#portfolio)
  - [Table of Contents](#table-of-contents)
- [Intro](#intro)
- [Learning outcomes](#learning-outcomes)
- [Proof](#proof)
- [Self-assessment](#self-assessment)
  - [Web Application](#web-application)
  - [Software Quality](#software-quality)
  - [Agile Methodology](#agile-methodology)
  - [CI/CD](#cicd)
  - [Cultural Differences and Ethics](#cultural-differences-and-ethics)
  - [Requirements and Design](#requirements-and-design)

# Intro

This portfolio will guide you through several snippets of my work during the third software semester of FHICT (2022-2023). This repository will act as a summary of my work in this semester, along with explanations of how I proved a certain set of learning 
outcomes.

Down below I will provide you with the learning outcomes as they are at the time of writing (September 12th, 2022), with the explanation of said outcome. This will be followed with a table containing all of my work proving the outcomes.

# Learning outcomes

For a complete list of the learning outcomes and their explanation as of September 12th, 2022, see [here](/dict/learning-outcomes.md).

# Proof

Below is a table containing all of my proof, with a link to further explanation.

| Explanation | Type | Learning Outcome | Link |
|:------------|:-----|:-----------------|:----:|
| A CI implementation an Angular frontend, complete with DockerHub deployment. | Implementation | [CI/CD](dict/learning-outcomes.md#cicd) | [🔗](docs/proof/1-ci-angular.md) |
| A user-story set and a C4-model showing the desired architecture of my stack. | Design | [Requirements and Design](dict/learning-outcomes.md#requirements-and-design) | [🔗](docs/proof/2-c4-model.md) | 
| A Java Springboot project with a Customer service, Netflix Eureka support and Spring API Gateway implementation. | Proof of Concept | [Web Application](dict/learning-outcomes.md#web-application) (Architecture) | [🔗](docs/proof/3-poc-java-customer-service.md) |
| A dockerized Java Spring Cloud implementation, a continuation of [this](docs/proof/3-poc-java-customer-service.md) POC. | Proof of Concept | [Web Application](dict/learning-outcomes.md#web-application) (Architecture) | [🔗](docs/proof/4-poc-dockerized-java-customer-services.md) |
| How do I implement a microservices architecture in Java? | Research | DOT research requirement Fontys | [🔗](docs/proof/4a-dot-research-microservices.md) |
| Agile methodology in a group project | Research and Analysis | [Agile Methodology](dict/learning-outcomes.md#agile-methodology) | [🔗](docs/proof/5-agile-group-project.md) |
| Unit Testing in a backend ASP.NET API | Implementation | [Software Quality](dict/learning-outcomes.md#software-quality) | [🔗](docs/proof/6-unit-test-in-aspnet-api.md) |
| Unit Testing in an Angular SPA | Implementation | [Software Quality](dict/learning-outcomes.md#software-quality) | [🔗](/docs/proof/7-unit-test-in-angular.md) |
| How can I avoid storing sensitive user data? | Research | DOT research requirement Fontys | [🔗](/docs/proof/8-oauth.md) |
| Analysis: Ethics in Software Development | Analysis | [Cultural Differences and Ethics](dict/learning-outcomes.md#cultural-differences-and-ethics) | [🔗](docs/proof/9-ethics.md) |
| The user flow when logging in and changing settings. | Implementation | [Web Application](dict/learning-outcomes.md#web-application) | [🔗](docs/proof/10-user-flow.md) |
| Logging user interaction and API events. | Implementation | [Software Quality](dict/learning-outcomes.md##../docs/proof/11-logger.md) | [🔗](docs/proof/11-logger.md) |
| The API contract and documentation. | Design | [Requirements and Design](dict/learning-outcomes.md#requirements-and-design) | [🔗](docs/proof/12-apidocs.md) |

# Self-assessment

Below, I will provide the reader with a self-assessment. In this assessment I will assess my own qualities, and explain how I think I quality for the given learning outcome (as they are laid out [here](dict/learning-outcomes.md)). 

The proficiency rating I will give myself are as they are described on [CANVAS](https://fhict.instructure.com/courses/12518/outcomes) on December 20th 2022. The rating goes from '*Undefined*', to '*Orienting*', to '*Beginning*', '*Proficient*' and finally to '*Advanced*', on a scale of 0 to 5.

## Web Application

<table>
  <tr>
    <th><strong>Learning Outcome</strong></th>
    <td>"You desgin and build user-friendly, full-stack web applications."</td>
  </tr>
  <tr>
    <th><strong>Proficiency Rating</strong></th>
    <td>Advanced (5)</td>
  </tr>
  <tr>
    <th><strong>Explanation</strong></th>
    <td>
        <p>
          In this semester I have managed to set up a full Angular-Java-MongoDB stack web application, complete with a Spring Cloud Gateway and Netflix Eureka Service Discovery support.
        </p>
        <p>
          The frontend Angular web-app is built with components and single-responsibility in mind. All calls to the API are done via their own specific service. Logging in is done via a <code>Google API</code> service. All interaction with the Session Storage is wrapped in its own service to be able to control the flow. The GoogleAPI service could do with some improvements, namely by moving its Gmail functionality to a separate Gmail service.
        </p>
        <p>
          All calls so internal and external APIs make use of Angular's Interceptor functionality that modify the request and add in the necessary authentication tokens and/or headers, depending on which resource is being requested.
        </p>
        <p>
          All services are injected via Angular's dependency injection.
        </p>
        <p>
          The UI is made with a handheld device in mind, and as such is made responsive with the use of flexbox and media queries.
        </p>
        <p>
          The Settings API in the backend reads and writes to a MongoDB document store via its own MongoRepository. The data is stored persistently on the computer, and can be accessed in the Docker environment through the use of Docker Volumes.
        </p>
    </td>
  </tr>
</table>

## Software Quality

<table>
  <tr>
    <th><strong>Learning Outcome</strong></th>
    <td>"You use software tooling and methodology that continuously monitors and improve the software quality during software development."</td>
  </tr>
  <tr>
    <th><strong>Proficiency Rating</strong></th>
    <td>Advanced (5)</td>
  </tr>
  <tr>
    <th><strong>Explanation</strong></th>
    <td>
        <p>
          Relevant pieces of code are tested via unit tests and integration tests. All tests are carried out in an isolated manner with mocked classes/services wherever an outside components needs to be accessed.
        </p>
        <p>
          Wherever possible, services and repositories are injected via dependency injection, rather than having multiple instances of a single item.
        </p>
        <p>
          The Settings API logs all activity happening on the API, with anonymous identifiers linked to the authenticated user trying to access a resource. Currently, it logs this directly to the console. An improvement could be to log it to a file, or even better, to log it to a central logging microservice, which in turn saves it to a file and possibly uses it for visualizing data.
        </p>
        <p>
          The frontend Github repository has SonarCloud integrated in its CI. SonarCloud will monitor code coverage and any obvious bugs or code smells that appear in the code. Whenever a bug sneaks into the code, SonarCloud will block the CI pipeline until the bug is fixed. This is not a magical bandaid, but it will help with code quality.
        </p>
        <p>
          During development, all used IDEs have SonarLint installed as an extension. SonarLint will scan all edited files for any obvious errors, bugs and the like and will block pushing to GitHub when it finds something.
        </p>
    </td>
  </tr>
</table>

## Agile Methodology

<table>
  <tr>
    <th><strong>Learning Outcome</strong></th>
    <td>"You choose and implement the most suitable agile software development method for your software project."</td>
  </tr>
  <tr>
    <th><strong>Proficiency Rating</strong></th>
    <td>Proficient (4)</td>
  </tr>
  <tr>
    <th><strong>Explanation</strong></th>
    <td>
        <p>
          As explained in <a href="docs/proof/5-agile-group-project.md">this article</a>, the group project uses Agile extensively. 
        </p>
        <p>
          In my individual project, I could have implemented Agile a bit better. I could, for example have switched to Jira for the issue tracking, and I could have adhered better to the 'sprint system'. I have been very flexible in implementing the user stories, so you could see that as a plus.
        </p>
    </td>
  </tr>
</table>

## CI/CD

<table>
  <tr>
    <th><strong>Learning Outcome</strong></th>
    <td>"You design and implement a (semi)automated software release process that matches the needs of the project context."</td>
  </tr>
  <tr>
    <th><strong>Proficiency Rating</strong></th>
    <td>Provanced (4.5?) (Proficient (4) / Advanced (5))</td>
  </tr>
  <tr>
    <th><strong>Explanation</strong></th>
    <td>
        <p>
          Within every repository, a GitHub Actions workflow is set up to check if the application builds, and if the tests succeed.
        </p>
        <p>
          Within the frontend project, an additional quality gate is implemented via SonarCloud, which blocks the pipeline if it finds any bug, or if the code coverage is below 50%.
        </p>
        <p>
          Currently, I automatically push a new Docker image to DockerHub when the frontend project merges something into main (usually from the dev branch). From there on out, the user can pull the image for a flawless setup of that version. I could have also implemented this for the other repositories/projects, but this fell out of scope at the time. This could be something to work on in the future.
        </p>
        <p>
          I could have worked on deployment to an actual online webservice like DigitalOcean. Currently, the package is deployed by executing a Docker Compose file through the CLI on one's computer. There is no need to install any SDKs or programs other than Docker and Docker Compose to run the full project (and have virtualization enabled on Windows hosts, for WSL).
        </p>
    </td>
  </tr>
</table>

## Cultural Differences and Ethics

<table>
  <tr>
    <th><strong>Learning Outcome</strong></th>
    <td>"You recognize and take into account cultural differences between project stakeholders and ethical aspects in software development."</td>
  </tr>
  <tr>
    <th><strong>Proficiency Rating</strong></th>
    <td>Proficient (4)</td>
  </tr>
  <tr>
    <th><strong>Explanation</strong></th>
    <td>
        <p>
          See <a href="docs/9-ethics.md">this article</a>.
        </p>
    </td>
  </tr>
</table>

## Requirements and Design

<table>
  <tr>
    <th><strong>Learning Outcome</strong></th>
    <td>"You analyze (non-functional) requirements, elaborate (architectural) designs and validate them using multiple types of test techniques."</td>
  </tr>
  <tr>
    <th><strong>Proficiency Rating</strong></th>
    <td>Proficient (4)</td>
  </tr>
  <tr>
    <th><strong>Explanation</strong></th>
    <td>
        <p>
          I have started the individual project by formulation a project idea. I then started to design the user stories, and an accompanying C4-model of the project. The same was done for the group project.
        </p>
        <p>
          The Settings API was made with an API contract in mind. The API contract is presented in <code>yml</code> format. See <a>here</a>.
        </p>
        <p>
          During the group projects, after having reviewed the sprint with the stakeholders, we kept refining the user stories and acceptation criteria based on the feedback they gave us. The C4-Model remained roughly the same throughout the project.
        </p>
        <p>
          In my individual projects, and admittedly the GP as well, I could have formulated my user stories better. I should have split them up more and made them testable by formulating very concise acceptation criteria with clear data to base the tests upon. This will be improved upon with future projects.
        </p>
    </td>
  </tr>
</table>