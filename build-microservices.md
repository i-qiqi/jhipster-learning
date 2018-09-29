# Building Microservices with JHipster
## Generate a Gateway application
> JHipster follows the proxy microservice pattern in which there is an aggregator/proxy in front of the services, which acts as the gateway for the end users.

 <hr>
- To avoid slow network latency , tick out the front end test framework (protractor) from this app.

### Gateway configuration
- `AccessControlFilter` :
- `SwaggerBasePathRewritingFilter`:
- `TokenRelayFilter` :

### JWT Authentication
- `Compact` : small and can be sent to each request
- `Self-contained` : The payload contains all the neccessary details about the user, which prevents us from querying the database for user authentication.
-  `Structure` : header+`.`+payload+`.`+signature, all are base64  encoded strings.
- `format` : Authorization : Bearer < token >
    - In JHipster , we use `JJWT( Java-based JSON Web Tokens)` from `okta`
    -  Okta is a simplified `bulider pattern-based` used to generate and sign the token as a `producer` and parse and validate the token as a `consumer`.
- `TokenProvider` :
  - Creating the token : `createToken(Authentication authentication, boolean rememberMe)`
  - Validating the token : `validateToken(String authToken)`\]

## Generate a microservices applications
- Use the Spring cache abstraction :
  - `HazelCast` : a distributed cache, it provides a shared cache among all sessions. It's possible to hold the persisted data across the cluster or at the JVM level. We can have different modes available, with single or multiple nodes.
  - `Ehcache` : a local cache and it's useful for storing infomation in a single node.
  - `Infinispan` : a hybrid cache, like HazelCast , Infinispan is capable  of creating a cluster and sharing information among multiple nodes.

### Microservice configuration
- `SecurityConfiguration` :
    - Ignore all the frontend related request.
    - Disable `CSRF(Cross Site Request Forgery)` by default.
    - Enable `STATELESS` session policy. It makes our our application unable to create and maintain any sessions. Every request is authenticated and authorized based on the token.
    -`bootstrap.yml` :
      - `JHipster registry` : define registry-related  information.
      - Spring Boot service name
      - Default Spring Cloufd Cofiguration parameters
