

## Problem statement
This pattern is used to solve an issue of how to implement a query that retrieves data from multiple services in a microservice architecture?

## Solution

Define a view database, which is a read-only replica that is designed to support that query. The application keeps the replica up to data by subscribing to Domain events published by the service that own the data.

