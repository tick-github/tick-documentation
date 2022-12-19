# Logging user interaction and API events

- [Logging user interaction and API events](#logging-user-interaction-and-api-events)
  - [Intro](#intro)
  - [Why?](#why)
  - [Current implementation](#current-implementation)
  - [Future implementation](#future-implementation)

## Intro

The project currently implements a logger in its settings API. The logger logs the various requests and events that happen to and within the API application. Currently, it uses the `Slf4j` framework.

## Why?

Logging events and request is useful when debugging problems in your application, or when reviewing a certain event in its lifetime. 

For example, when your application receives a sudden spike of activity, or a huge spike of errors, the logger can help locate the problem. A well-implemented logging mechanism can also help with the implementation of automated system to load-balance or even close the application in times of need.

## Current implementation

Currently, the application only logs various events to the console. This is useful during development to debug certain aspects of the application.

The application uses the `@Slf4j` attribute on the controller level to log the following events:

* Received a request do X.
* Created a X for user Y.
* Tried to fulfill request X, but couldn't comply due to reason Y.
* Responded to request X.
* Received an insecure ping request.
* Received a secure ping request from user X.

These events are raised with Slf4j's methods `log.info()`, `log.warn()` and `log.error()`.

Example:

```java
@ApiOperation(value = "Gets a Settings Object for a specific user.", response = Response.class)
@ApiResponses({
        @ApiResponse(code = 200, message = ""),
        @ApiResponse(code = 401, message = "Authorization header is invalid"),
        @ApiResponse(code = 403, message = "Authorization header is missing in request"),
        @ApiResponse(code = 404, message = "Could not find settings for user %s.")
})
@GetMapping public ResponseEntity<Response> get(
        @ApiParam(value = "The user's sub identifier grabbed from a valid Google ID Token.", required = true)
        @RequestHeader("id") String userId) {

        log.info(String.format("Received request to get settings for user %s.", userId));
        var settings = _repository.findById(userId);

        if (settings.isEmpty()) {
                log.warn(String.format(
                        "Tried to get Settings object for user %s but found no match.", userId)
                );
                return ResponseEntity.status(HttpStatus.NOT_FOUND).body(
                        Response.builder()
                        .message(String.format("Could not find settings for user %s.", userId))
                        .build()
                );
        }

        log.info(String.format("Responded to request for settings for user %s.", userId));

        return ResponseEntity.ok().body(
                Response.builder()
                        .data(settings)
                        .build()
        );
}
```

## Future implementation

Currently, the events are logged directly and only to the console. This is fine for developement, but another approach is preferred in production. 

These logs are valuable information and need to be stored in some kind of datastore via a logging service. The API would send logging requests to the logging service, which in part would save these logs in a secure place.

Popular choices for logging infrastructure in Spring are:

* ELK Stack (Elastic Search, Logstash and Kibana)
* Zipkin, an Open Tracing API , and Jaeger for Distributed Tracing
* Graylog (Elastisearch, MongoDB, Scala) -> [see here](https://dzone.com/articles/spring-boot2-graylog)