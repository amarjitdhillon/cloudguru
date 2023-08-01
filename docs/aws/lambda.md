
# Lambda basics

- Serverless computing allows you to build and run applications and services without thinking about servers 🖥️
-  With serverless computing, your application still runs on servers, but all the server management is done by AWS ☁️

- It scales out instead of scaling up ⬆️ with the number of requests.
- Lambda functions are independent, meaning that they will get replicated with each event 🔥


!!! Note
    Using AWS and its Serverless Platform, you can build and deploy applications on cost-effective services that provide built-in application availability and flexible scaling capabilities. This lets you focus on your application code instead of worrying about provisioning, configuring, and managing servers.


## Which services are serverless?
- Lambda is serverless.
- RDS is not serverless as it has downtime.
- Aurora is serverless.
- Dynamo, S3 is serverless.

## Concepts

### Function

- A function is a resource that you can invoke to run your code in Lambda.
- A function has code to process the events that you pass into the `function` or that other AWS services send to the function.

### Trigger

A trigger is a resource or configuration that invokes a Lambda function. Triggers include AWS services that you can configure to invoke a function and event source mappings. 

!!! tip
    An `event source mapping` is a resource in Lambda that reads items from a stream or queue and invokes a function.


### Event

An event is a JSON-formatted document that contains data for a `Lambda function` to process. The runtime converts the event to an object and passes it to your function code. When you invoke a function, you determine the structure and contents of the event.


```json title='Example custom event – Weather data'
{
  "TemperatureK": 281,
  "WindKmh": -3,
  "HumidityPct": 0.55,
  "PressureHPa": 1020
}
```

When an AWS service invokes your function, the service defines the shape of the event.


```json title='Example service event – Amazon SNS notification'
{
  "Records": [
    {
      "Sns": {
        "Timestamp": "2019-01-02T12:45:07.000Z",
        "Signature": "tcc6faL2yUC6dgZdmrwh1Y4cGa/ebXEkAi6RibDsvpi+tE/1+82j...65r==",
        "MessageId": "95df01b4-ee98-5cb9-9903-4c221d41eb5e",
        "Message": "Hello from SNS!",
        ...
```


### Execution environment

An execution environment provides a secure and isolated runtime environment for your Lambda function. An execution environment manages the processes and resources that are required to run the function. 


### Instruction set architecture
The instruction set architecture determines the type of computer processor that Lambda uses to run the function. Lambda provides a choice of instruction set architectures:

- `arm64` – 64-bit ARM architecture, for the AWS Graviton2 processor.

- `x86_64` – 64-bit x86 architecture, for x86-based processors.


### Deployment package

You deploy your Lambda function code using a deployment package. Lambda supports two types of deployment packages:

- **A .zip file archive** that contains your function code and its dependencies. Lambda provides the operating system and runtime for your function.

- **A container image** that is compatible with the `Open Container Initiative (OCI)` specification. You add your function code and dependencies to the image. You must also include the operating system and a Lambda runtime.


### Runtime

The runtime provides a language-specific environment that runs in an execution environment. The runtime relays invocation events, context information, and responses between Lambda and the function. You can use runtimes that Lambda provides, or build your own. If you package your code as a .zip file archive, you must configure your function to use a runtime that matches your programming language. For a container image, you include the runtime when you build the image.



### Layer
A Lambda layer is a `.zip file archive` that can contain additional code or other content. A layer can contain libraries, a custom runtime, data, or configuration files.

!!! remember

    Layers provide a convenient way to package libraries and other dependencies that you can use with your Lambda functions. Using layers reduces the size of uploaded deployment archives and makes it faster to deploy your code. Layers also promote code sharing and separation of responsibilities so that you can iterate faster on writing business logic.

    You can include up to five layers per function. Layers count towards the standard Lambda deployment size quotas. When you include a layer in a function, the contents are extracted to the /opt directory in the execution environment.

By default, the layers that you create are private to your AWS account. You can choose to share a layer with other accounts or to make the layer public. If your functions consume a layer that a different account published, your functions can continue to use the layer version after it has been deleted, or after your permission to access the layer is revoked. However, you cannot create a new function or update functions using a deleted layer version.

!!! tldr
    Functions deployed as a container image do not use layers. Instead, you package your preferred runtime, libraries, and other dependencies into the container image when you build the image.

### Destination

`Destinations` are AWS resources that receive a `record of an invocation` after success or failure. You can configure Lambda to send invocation records when your function is invoked asynchronously, or if your function processes records from a stream. The contents of the invocation record and supported destination services vary by source.


### Extension

`Lambda extensions` enable you to augment your functions. For example, you can use extensions to integrate your functions with your preferred monitoring, observability, security, and governance tools. 

### Concurrency

Concurrency is the number of requests that your function is serving at any given time. When your function is invoked, Lambda provisions an instance of it to process the event. When the function code finishes running, it can handle another request. If the function is invoked again while a request is still being processed, another instance is provisioned, increasing the function's concurrency.

### Throtlling

!!! question "what is Throtlling?"
    At the highest level, throttling just means that Lambda will intentionally reject one of your requests and so what we see from the user side is that when making a client call, Lambda will throw a throttling exception, which you need to handle. Typically, people handle this by backing off for some time and retrying. But there are also some different mechanisms that you can use, so that’s interesting, Lambda will reject your request. 
    
    **Why does it occur?**
    Throttling occurs when your `concurrent execution count` > `concurrency limit`.

Now, just as a reminder, if this wasn’t clear, Lambda can handle multiple instance invocations at the same time and the sum of all of those invocations amounts to your concurrency execution count. So, assume we’re at a particular instant in time if you have more invocations that are running that exceed your configured limit, all new requests to your Lambda function will get a throttling exception.


!!! remember "What are the configure limits?" 
    Lambda has a default `1000 concurrency limit` that’s specified per region within an account. But it does get a little bit more complicated in terms of how this rule applies when you have multiple Lambda functions in the same region and the same account.

## Function URL

A function URL is a dedicated HTTP(S) endpoint for your Lambda function. You can create and configure a function URL through the Lambda console or the Lambda API. When you create a function URL, Lambda automatically generates a unique URL endpoint for you. Once you create a function URL, its URL endpoint never changes. Function URL endpoints have the following format:


```json
https://<url-id>.lambda-url.<region>.on.aws
```
!!! info
    Function URLs are dual stack-enabled, supporting IPv4 and IPv6.


## Code editor

The `code editor` supports languages that do not require compiling, such as `Node.js` and `Python`. The code editor suppports only `.zip` archive deployment packages, and the size of the deployment package must be less than 3 MB.




