# Backend for Frontend (BFF)

BFF is essentially a variant of the API Gateway pattern. It also provides an additional layer between microservices and clients.

<center> <img src="../../images/custom-service-api-gateway.png" width="85%"> </center>

But rather than being a single point of entry, it introduces multiple gateways for each client as shown below.

<center> <img src="../../images/multiple-custom-api-gateways.png" width="85%"> </center>

With BFF, you can add an API tailored to the needs of each client, removing a lot of the bloat caused by keeping it all in one place.

!!! abstract
    BFF is a variant of the API Gateway pattern, but it also provides an additional layer between microservices and each client type separately. Instead of a single point of entry, it introduces multiple gateways. Because of that, you can have a tailored API that targets the needs of each client (mobile, web, desktop, voice assistant, etc.), and remove a lot of the bloat caused by keeping it all in one place.

## Benefits

### Decoupling
Decoupling of Backend and Frontend​ for sure gives us faster time to market as frontend teams can have dedicated backend teams serving their unique needs. The release of new features of one frontend does not affect the other.

### Faster development
We can much easier maintain and modify APIs​ and even provide API versioning dedicated for specific frontend, which is a big plus from a mobile app perspective as many users do not update the app immediately.

### Multiple device types can call the backend in parallel 

While the browser is making a request to the browser BFF, the mobile devices can do the same. It will help obtain responses from the services faster.

###  Better security

Certain sensitive information can be hidden, and unnecessary data to the frontend can be omitted when sending back a response to the frontend. The abstraction will make it harder for attackers to target the application.



