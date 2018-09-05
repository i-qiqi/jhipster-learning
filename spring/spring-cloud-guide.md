# Spring Cloud Context

## Application Context Services

>  Spring boot has an opinionated view

### The Bootstrap Application Context
- Two Context : `Bootstrap context` + `Main context`

- bootstrap context

  - parent context for the main application.

  - responible for loading configuration properties from the  <font color="red">external sources</font> and for decrypting properties in the local external configuration files.
