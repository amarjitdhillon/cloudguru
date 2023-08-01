AWS AppSync provides a robust, scalable GraphQL interface for application developers to combine data from multiple sources, including Amazon DynamoDB, AWS Lambda, and HTTP APIs.

## Features

- Powerful GraphQL schema editing through the AWS AppSync console, including automatic GraphQL schema generation from DynamoDB

- Efficient data caching

- Integration with Amazon Cognito user pools for fine-grained access control at a per-field level

## Arcitecture

<center> <img src="../images/appsync_architecture.png" width="90%"> </center>

## Concepts
### GraphQL Proxy
A component that runs the GraphQL engine for processing requests and mapping them to logical functions for data operations or triggers. The data resolution process performs a batching process (called the Data Loader) to your data sources. This component also manages conflict detection and resolution strategies.

### Operation
AWS AppSync supports the three GraphQL operations: query (read-only fetch), mutation (write followed by a fetch), and subscription (long-lived requests that receive data in response to events).

### Action
There is one action that AWS AppSync defines. This action is a notification to connected subscribers, which is the result of a mutation. Clients become subscribers through a handshake process following a GraphQL subscription.

### Data Source
A persistent storage system or a trigger, along with credentials for accessing that system or trigger. Your application state is managed by the system or trigger defined in a data source. Examples of data sources include NoSQL databases, relational databases, AWS Lambda functions, and HTTP APIs.

### Resolver
A function that converts the GraphQL payload to the underlying storage system protocol and executes if the caller is authorized to invoke it. Resolvers are comprised of request and response mapping templates, which contain transformation and execution logic.

### Unit Resolver
A unit resolver is a resolver that performs a single operation against a predefined data source.

### Pipeline Resolver
A pipeline resolver is a resolver that allows executing multiple operations against one or more data sources. A pipeline resolver is composed of a list of functions. Each function is executed in sequence and can execute a single operation against a predefined data source.

### Function
A function defines a single operation that can be used across pipeline resolvers. Functions can be reused to perform redundant logic throughout the GraphQL Proxy. Functions are comprised of a request and a response mapping template, a data source name, and a version.

### Identity
A representation of the caller based on a set of credentials, which must be sent along with every request to the GraphQL proxy. It includes permissions to invoke resolvers. Identity information is also passed as context to a resolver and the conflict handler to perform additional checks.

### AWS AppSync Client
The location where GraphQL operations are defined. The client performs appropriate authorization wrapping of request statements before submitting to the GraphQL proxy. Responses are persisted in an offline store and mutations are made in a write-through pattern.


