# CLOUD SKILLS CHALLENGE Azure Developer

## Module:  Choose the best Azure service to automate your business processes

### Identify the technology options

Business processes modeled in software are often called workflows.
Azure includes four different technologies that you can use to build and implement workflows that integrate multiple systems:

+ Logic Apps - to automate, orchestrate, and integrate disparate components of a distributed application.  over 200 connectors are included.
+ Microsoft Power Automate to create workflows even when you have no development or IT Pro experience.
+ WebJobs
+ Azure Functions

All PaaS? I think so.

All involve inputs, actions, conditions, outputs. Scheduled or triggered.

Logic Apps and Microsoft Power Automate both include user interfaces in which you can draw out the workflow.
We call this approach a design-first approach.

_Code-first (imperative), Design-first (declarative)_

Microsoft Power Automate has four different types of flow that you can create:

+ Automated: A flow that is started by a trigger from some event. For example, the event could be the arrival of a new tweet or a new file being uploaded.
+ Button: Use a button flow to run a repetitive task with a single click from your mobile device.
+ Scheduled: A flow that executes on a regular basis such as once a week, on a specific date, or after 10 hours.
+ Business process: A flow that models a business process such as the stock ordering process or the complaints procedure. The flow process can have: notification to required people; with their approval recorded; calendar dates for steps; and recorded time of flow steps.

Under the hood, Microsoft Power Automate is built on Logic Apps.

WebJobs (PHP, python etc) and the WebJobs SDK (The WebJobs SDK only supports C# and the NuGet package manager.)

The Azure App Service is a cloud-based hosting service for web applications, mobile back-ends, and RESTful APIs.

WebJobs are a part of the Azure App Service that you can use to run a program or script automatically.

+ Continuous. These WebJobs run in a continuous loop. For example, you could use a continuous WebJob to check a shared folder for a new photo.
+ Triggered. These WebJobs run when you manually start them or on a schedule.

An Azure Function is a simple way for you to run small pieces of code in the cloud, without having to worry about the infrastructure required to host that code. You can write the Function in C#, Java, JavaScript, etc. You only pay for the time when the code runs. Azure automatically scales your function in response to the demand from users.

To create, choose from a template:

+ HTTPTrigger. Use this template when you want the code to execute in response to a request sent through the HTTP protocol.
+ TimerTrigger. Use this template when you want the code to execute according to a schedule.
+ BlobTrigger. Use this template when you want the code to execute when a new blob is added to an Azure Storage account.
+ CosmosDBTrigger. Use this template when you want the code to execute in response to new or updated documents in a NoSQL database.

comparing web jobs and functions:

|Azure WebJobs|	Azure Functions
Supported languages |	C# if you are using the WebJobs SDK	| C#, Java, JavaScript, PowerShell, etc.
Automatic scaling |	No |	Yes
Development and testing in a browser |	No |	Yes
Pay-per-use pricing |	No |	Yes
Integration with Logic Apps |	No |	Yes
Package managers |	NuGet if you are using the WebJobs SDK |x	Nuget and NPM
Can be part of an App Service application |	Yes |	No
Provides close control of JobHost |	Yes |	No

### Analyze the decision criteria

See diagram [https://docs.microsoft.com/en-gb/learn/modules/choose-azure-service-to-integrate-and-automate-business-processes/media/3-service-choice-flow-diagram.png]

[https://docs.microsoft.com/en-gb/learn/modules/choose-azure-service-to-integrate-and-automate-business-processes/3-analyze-the-decision-criteria]

### Choose the best design-first technology to automate your business process

[business process](https://docs.microsoft.com/en-gb/learn/modules/choose-azure-service-to-integrate-and-automate-business-processes/media/4-bike-hire-workflow.png)

Any of the 4 Az workflows could be used. the requirements narrow this down to design-first approach > Azure Logic Apps.

### When to choose Azure Functions to run your business logic

[business process](https://docs.microsoft.com/en-gb/learn/modules/choose-azure-service-to-integrate-and-automate-business-processes/media/5-bike-maintenance-workflow.png)

Design-first or code-first? code-first > Azure Function

[knowledge check](https://docs.microsoft.com/en-gb/learn/modules/choose-azure-service-to-integrate-and-automate-business-processes/6-knowledge-check)

got all 4 wrong. I hate these questions!

tips:

+ webjobs are the only technology of the 4 that permits developers to control retry policies
+ Implement the workflow using Microsoft Power Automate because this allows the creative team, who are not developers, to manage the flow.
+ Azure Logic Apps is the only one of the four technologies that provides a design-first approach intended for developers.

## module: Create serverless logic with Azure Functions

### Decide if serverless computing is right for your business needs

Serverless compute can be thought of as a function as a service (FaaS), or a microservice that is hosted on a cloud platform. our app is automatically scaled out or down depending on load. Azure has several ways to build this sort of architecture. The two most common approaches are Azure Logic Apps and Azure Functions, which we focus on in this module.

Azure Functions - Functions are event driven. You are charged based on what is used — not on reserved time. If state is required, it can be stored in an associated storage service.

Bindings are a declarative way to connect data and services to your function. [supported-bindings](https://docs.microsoft.com/en-us/azure/azure-functions/functions-triggers-bindings?tabs=csharp#supported-bindings)

Declare where the data comes from (trigger/input binding) and where it goes (output binding).

eg: we want to write a new row to Azure Table storage whenever a new message appears in Azure Queue storage. This scenario can be implemented using an Azure Queue storage trigger and an Azure Table storage output binding.

#### Triggers (1 per function)

Blob storage: Starts a function when a new or updated blob is detected.
Azure Cosmos DB: Start a function when inserts and updates are detected.
Event Grid: Starts a function when an event is received from Event Grid.
HTTP: Starts a function with an HTTP request.
Microsoft Graph Events: Starts a function in response to an incoming webhook from the Microsoft Graph. Each instance of this trigger can react to one Microsoft Graph resource type.
Queue storage: Starts a function when a new item is received on a queue. The queue message is provided as input to the function.
Service Bus: Starts a function in response to messages from a Service Bus queue.
Timer: Starts a function on a schedule.

By default, functions have a timeout of 5 minutes. This timeout is configurable to a maximum of 10 minutes. if your service is initiated through an HTTP request and you expect that value as an HTTP response, the timeout is further restricted to 2.5 minutes.  also an option called Durable Functions that allows you to orchestrate the executions of multiple functions without any timeout.

While scaling, only one function app instance can be created every 10 seconds, for up to 200 total instances.

### Create a function app in the Azure portal

uses a sandbox ... tech.1@ account.

Functions are hosted in an execution context called a function app. You define function apps to logically group and structure your functions and a compute resource in Azure.
function app: a collection of functions that are published together into the same environment. All of the functions in an app share a common set of configuration values, and must all be built for the same language runtime. Each function app is an Azure resource that can be configured and managed independently.

Behind the scenes, an Azure Functions app is a collection of one or more virtual machines (VMs), running a web server.

Function apps may use one of two types of service plans: Consumption service plan, and Azure App Service plan (The plan allows you to avoid timeout periods by having your function run continuously on a VM that you define - so not technically serverless.)

When you create a function app, it must be linked to a storage account. The function app uses this storage account for internal operations such as logging function executions and managing execution triggers. On the Consumption service plan, this is also where the function code and configuration file are stored.

In Azure, function apps run the function host automatically when they start.

You must configure a function with exactly one trigger.

.. ran the boiler plate javascript basic http trigger function

```cmd
curl --header "Content-Type: application/json" --header "x-functions-key: dCyK5VFsnUiBCI1a3aBAOBxe78yltbtvFibuy361aitk5Ht6/j9zzw==" --request POST --data "{\"name\": \"Hello Neil\"}" https://escalator-functions-njt1502.azurewebsites.net/api/HttpTrigger1
```

and then did another simple demo that passed json in the POST body.

## module: Execute an Azure Function with triggers

### HTTP trigger

One setting that's important to understand is Request parameter name. This setting is a string that represents the name of the parameter that contains the information about an incoming HTTP request. By default, the name of the parameter is req.

```cmd
curl https://4timertriggernjt1502.azurewebsites.net/api/HttpTrigger1?name=bob
```

returns "Hello, bob"

### Execute an Azure function when a blob is created

Azure Storage? Highly available, Secure, Scalable, Managed.

Azure Blob storage? Storing files, Serving files, , Streaming video and audio, Logging data.

There are three types of blobs: block blobs, append blobs, and page blobs. Block blobs are the most common type. They allow you to store text or binary data efficiently. Append blobs are like block blobs, but they're designed more for append operations like creating a log file that's being constantly updated. Finally, page blobs are made up of pages and are designed for frequent random read and write operations.

Monitor a storage path, rg: `samples-workitems/{name}.png` will fire the function trigger for every upload/update of .png files in samples-workitems.
The name represents a parameter in your Azure function that receives the name of the added file. For example, if we upload a file named resume.txt, my Azure function receives that value as a string through a parameter called name.

## module: Chain Azure Functions together using input and output bindings

### Explore input (source) and output (destination) binding types (type = blob storage, cosmos db etc)

All bindings have Name, Type, Direction. Most have Connection.

### Read data with input bindings

A binding expression is specialized text in function.json, function parameters, or code that is evaluated when the function is invoked to yield a value. 

(this module only skims the surface of using a cosmos input)

```javascript
module.exports = function (context, req) {
    var bookmark = context.bindings.bookmark // get the binding named bookmark (the 'Document parameter name' of the cosmos input we made). it's build upon the context which automagically passes the paramter (id, name - whatever we defined earlier). The search happens in of there is a result, a bookmark object is returned. i think.
    if(bookmark){}
    else {}
    // ^^ stuff
    context.done(); // return http output result.
    
```

### Write data with output bindings

```javascript
module.exports = function (context, req) {

    var bookmark = context.bindings.bookmark
    if(bookmark){
            context.res = {
            status: 422,
            body : "Bookmark already exists.",
            headers: {
            'Content-Type': 'application/json'
            }
        };
    }
    else {
        
        // Create a JSON string of our bookmark.
        var bookmarkString = JSON.stringify({ 
            id: req.body.id,
            url: req.body.url
        });

        // Write this bookmark to our database.
        context.bindings.newbookmark = bookmarkString;

        // Push this bookmark onto our queue for further processing.
        context.bindings.newmessage = bookmarkString; // queue defined in binding gets created automatically

        // Tell the user all is well.
        context.res = {
            status: 200,
            body : "bookmark added!",
            headers: {
            'Content-Type': 'application/json'
            }
        };
    }
    context.done();
};
```

## module:  Create a long-running serverless workflow with Durable Functions 

Durable Functions (an extension of Azure Functions) enables you to implement complex stateful functions in a serverless-environment.
Durable Functions can retain state between function calls. This approach enables you to simplify complex stateful executions in a serverless-environment.

You can use three durable function types: Client, Orchestrator, and Activity.

Client functions are the entry point for creating an instance of a Durable Functions orchestration. They can run in response to an event from many sources, such as a new HTTP request arriving, a message being posted to a message queue, an event arriving in an event stream. You can write them in any of the supported languages.

Orchestrator functions describe how actions are executed, and the order in which they are run. You write the orchestration logic in code (C# or JavaScript).

Activity functions are the basic units of work in a durable function orchestration. An activity function contains the actual work performed by the tasks being orchestrated.

### Application patterns

Function chaining - In this pattern, the workflow executes a sequence of functions in a specified order. The output of one function is applied to the input of the next function in the sequence. The output of the final function is used to generate a result.

Fan out/fan in - This pattern runs multiple functions in parallel and then waits for all the functions to finish. The results of the parallel executions can be aggregated or used to compute a final result.

Async HTTP APIs - This pattern addresses the problem of coordinating state of long-running operations with external clients. An HTTP call can trigger the long-running action. Then, it can redirect the client to a status endpoint. The client can learn when the operation is finished by polling this endpoint.

Monitor - This pattern implements a recurring process in a workflow, possibly looking for a change in state. For example, you could use this pattern to poll until specific conditions are met.

Human interaction - This pattern combines automated processes that also involve some human interaction. A manual process within an automated process is tricky because people aren't as highly available and as responsive as most computers. Human interaction can be incorporated using timeouts and compensation logic that runs if the human fails to interact correctly within a specified response time. An approval process is an example of a process that involves human interaction.

### Comparison with Logic Apps

Durable Functions and Logic Apps are both Azure services that enable serverless workload. Azure Durable Functions is intended as a powerful serverless compute option to run custom logic. Azure Logic Apps is better suited for integrating Azure services and components. You can use either technology to create complex orchestrations. With Azure Durable Functions, you develop orchestrations by writing code and using the Durable Functions extension. With Logic Apps, you create orchestrations by using the design surface or editing configuration files.

### sanbox demo

You should use durable timers in orchestrator functions instead of the setTimeout() and setInterval() functions.

## module: Develop, test, and publish Azure Functions by using Azure Functions Core Tools

The Azure Functions Core Tools are command-line utilities that enable you to develop and run functions locally and publish them to Azure.

A functions project on your computer is equivalent to a function app in Azure, and can contain multiple functions that use the same language runtime.

You can use the Core Tools to generate function projects and functions from scratch. `func init`, `func new`.  publish your functions to Azure.

[https://docs.microsoft.com/en-us/cli/azure/?view=azure-cli-latest]

[https://docs.microsoft.com/en-us/azure/azure-functions/]  .. see How-to-guides > Develop > Local Development > Core Tools

## module: Develop, test, and deploy an Azure Function with Visual Studio

An Azure Function is implemented as a static class. The class provides a static, asynchronous method named Run, which acts as the entry point for the class.

You can configure continuous deployment from the Azure portal, using the Deployment Center feature of an Azure Functions app. Deployment is configured on a per-function app basis.

Azure Functions can be deployed from a zip file using the push deployment technique. You can do this with the Azure CLI, or by using the REST interface.

```cmd
az functionapp deployment source config-zip \
-g <resource-group> \
-n <function-app-name> \
--src <zip-file>
```

## module: Monitor GitHub events by using a webhook with Azure Functions

Webhooks offer a lightweight mechanism for apps to be notified by another service when something of interest happens via an HTTP endpoint. 

## module: Enable automatic updates in a web application using Azure Functions and SignalR Service

Start = see E:\Wunderpus\Miniprojects\ignite-az-functions-signalr for polling version. Essentially vue.js axios on timer hitting api to pull from cosmos db.

End (i)

### Use a storage account to host a static website

When you copy files to a storage container named $web, those files are available to web browsers via a secure server using the [https://<ACCOUNT_NAME>.<ZONE_NAME>.web.core.windows.net/<FILE_NAME>] URI scheme.

(the demo just used the code tools to do it all as part of Azure create function f1 command)

## module: Expose multiple Azure Function apps as a consistent API by using Azure API Management

You can use Azure Functions and Azure API Management (APIM) to build complete APIs with a microservices architecture. Azure API Management (APIM) is a fully managed cloud service that you can use to publish, secure, transform, maintain, and monitor APIs. It helps organizations publish APIs to external, partner, and internal developers to unlock the potential of their data and services. API Management handles all the tasks involved in mediating API calls, including request authentication and authorization, rate limit and quota enforcement, request and response transformation, logging and tracing, and API version management. APIM enables you to create and manage modern API gateways for existing backend services no matter where they are hosted.

Because you can publish Azure Functions through API Management, you can use them to implement a microservices architecture; each function implements a microservice. By adding several functions to a single API Management product, you can build those microservices into an integrated distributed application. Once the application is built, you can use API Management policies to implement caching or ensure security requirements.

In the demo, took two Azure functions (one xml, one Json, both on different urls) and imported them into APIM. result = a unified url and json for both

```bash
// set the variables in cloud shell, then tested each endpoint with a curl
GATEWAY_URL=https://productfunctioneced48e61e-apim.azure-api.net
SUB_KEY=a3fc0c68770d4ff788aa2aaf4e0a922f

curl -X GET "$GATEWAY_URL/products/ProductDetails?id=2" -H "Ocp-Apim-Subscription-Key: $SUB_KEY"
```

## module: Choose a messaging model in Azure to loosely connect your services

Here, you will learn how to choose the right messaging technology in Azure for each communication task in a distributed application.

+ Azure Storage queues (simple, blob storage based)
+ Azure Event Hubs (big data, streaming data analytics)
+ Azure Event Grid (normal events)
+ Azure Service Bus (messages. has queues,topics,relays, transactions etc)

Event Grid is designed for events, which notify recipients only of an event and do not contain the raw data associated with that event. Azure Event Hubs is designed for high-flow analytics types of events. Azure Service Bus and storage queues are for messages, which can be used for binding the core pieces of any application workflow

### Messages or Events

In the terminology of distributed applications, messages have the following characteristics:

+ A message contains raw data, produced by one component, that will be consumed by another component.
+ A message contains the data itself, not just a reference to that data (which is more brittle (needs lookup)))
+ the sender and receiver of a message are often coupled by a strict data contract.
+ The sending component expects the message content to be processed in a certain way by the destination component. The integrity of the overall system may depend on both sender and receiver doing a specific job. You can think of sending a message as one component passing the baton of a workflow to a different component. The entire workflow may be a vital business process, and the message is the mortar that holds the components together.

For example, suppose a user uploads a new song by using the mobile music-sharing app. The mobile app must send that song to the web API that runs in Azure. The song media file itself must be sent, not just an alert that indicates that a new song has been added. The mobile app expects that the web API will store the new song in the database and make it available to other users. This is an example of a message.

Events have the following characteristics:

+ An event is a lightweight notification that indicates that something happened.
+ The event may be sent to multiple receivers , or to none at all.
+ Events are often intended to "fan out," or have a large number of subscribers for each publisher.
+ The publisher of the event has no expectation about the action a receiving component takes.
+ Some events are discrete units and unrelated to other events.
+ Some events are part of a related and ordered series.

For each communication, consider the following question: Does the sending component expect the communication to be processed in a particular way by the destination component?

If the answer is yes, choose to use a message. If the answer is no, you may be able to use events.

### Choose a message-based delivery with queues: Azure Queue Storage / Azure Service Bus

Queue storage is a service that uses Azure Storage to store large numbers of messages that can be securely accessed from anywhere in the world using a simple REST-based interface. Queues can contain millions of message.

Service Bus is a message broker system intended for enterprise applications. These apps often utilize multiple communication protocols, have different data contracts, higher security requirements, and can include both cloud and on-premises services. Service Bus is built on top of a dedicated messaging infrastructure designed for exactly these scenarios.

Azure Service Bus topics are like queues, but can have multiple subscribers. When a message is sent to a topic instead of a queue, multiple components can be triggered to do their work. Imagine in a music-sharing application, a user is listening to a song. The mobile app might send a message to the "Listened" topic. That topic will have a subscription for "UpdateUserListenHistory", and a different subscription for "UpdateArtistsFanList". Each of those functions is handled by a different component that receives its own copy of the message. Use Service Bus topics if you need multiple receivers to handle each message

Internally, topics use queues. When you post to a topic, the message is copied and dropped into the queue for each subscription. The queue means that the message copy will stay around to be processed by each subscription branch even if the component processing that subscription is too busy to keep up.

Topics are not supported in the Basic pricing tier.

A relay is an object that performs synchronous, two-way communication between applications. Unlike queues and topics, it is not a temporary storage location for messages. Instead, it provides bidirectional, unbuffered connections across network boundaries such as firewalls. Don't need to know more at this stage.

Benefits of queues

+ Increased reliability (during  high demand, messages can wait until a destination component is ready to process them.)
+ Message delivery guarantees (At-Least-Once Delivery / At-Most-Once Delivery/ First-In-First-Out (FIFO))
+ Transactional support (like a db: al messages in the transaction succeed or all fail)

Use Service Bus queues if you:

+ Need an At-Most-Once delivery guarantee (choose between a very small chance that a message is lost or a very small chance it is handled twice).
+ Need a FIFO guarantee (i think Az Storage accounts does not guarantee this, it's just likely).
+ Need to group messages into transactions.
+ Want to receive messages without polling the queue.
+ Need to provide a role-based access model to the queues.
+ Need to handle messages larger than 64 KB but less than 256 KB.
+ Queue size will not grow larger than 80 GB.
+ Want to publish and consume batches of messages.

Queue storage isn't quite as feature rich, but if you don't need any of those features, it can be a simpler choice. In addition, it's the best solution if your app has any of the following requirements.

Use Queue storage if you:

+ Need an audit trail/logs of all messages that pass through the queue.
+ Expect the queue to exceed 80 GB in size.
+ Want to track progress for processing a message inside of the queue.
+ A queue is a simple, temporary storage location for messages sent between the components of a distributed application. Use a queue to organize messages and gracefully handle unpredictable surges in demand.

Use Storage queues when you want a simple and easy-to-code queue system. For more advanced needs, use Service Bus queues. If you have multiple destinations for a single message, but need queue-like behavior, use Service Bus topics.

### Choose Azure Event Grid

Azure Event Grid is a fully-managed event routing service running on top of Azure Service Fabric. Event Grid distributes events from different sources, such as Azure Blob storage accounts or Azure Media Services, to different handlers, such as Azure Functions or Webhooks. Event Grid was created to make it easier to build event-based and serverless applications on Azure. Event Grid supports most Azure services as a publisher or subscriber and can be used with third-party services. It provides a dynamically scalable, low-cost, messaging system that allows publishers to notify subscribers about a status change

There are several concepts in Azure Event Grid that connect a source to a subscriber:

+ Events: What happened.
+ Event sources: Where the event took place.
+ Topics: The endpoint where publishers send events.
+ Event subscriptions: The endpoint or built-in mechanism to route events, sometimes to multiple handlers. Subscriptions are also used by handlers to filter incoming events intelligently.
+ Event handlers: The app or service reacting to the event.

The event sources send events to the Event Grid and the Event Grid forwards relevant events to the subscribers.

Events have a defined schema

```json
[
  {
    "topic": string,
    "subject": string,
    "id": string,
    "eventType": string,
    "eventTime": string,
    "data":{
      object-unique-to-each-publisher
    },
    "dataVersion": string,
    "metadataVersion": string
  }
]
```

Event Source - my custom app w/ my custom event || Azure Storage  w/ BlobCreated etc.

Event topics categorize events into groups. Topics are represented by a public endpoint and are where the event source sends events to.

System topics are built-in topics provided by Azure services. You don't see system topics in your Azure subscription because the publisher owns the topics, but you can subscribe to them

Custom topics are application and third-party topics. When you create or are assigned access to a custom topic, you see that custom topic in your subscription.

Event Subscriptions define which events on a topic an event handler wants to receive. A subscription can also filter events by their type or subject, so you can ensure an event handler only receives relevant events.

An event handler (sometimes referred to as an event "subscriber") is any component (application or resource) that can receive events from Event Grid. For example, Azure Functions can execute code in response to the new song being added to the Blob storage account. Subscribers can decide which events they want to handle and Event Grid will efficiently notify each interested subscriber when a new event is available - no polling required.

The following object types in Azure can receive and handle events from Event Grid:

+ Azure Functions: Custom code that runs in Azure, without the need for explicit configuration of a host virtual server or container. Use an Azure function as an event handler when you want to code a custom response to the event.
+ Webhooks: A webhook is a web API that implements a push architecture.
+ Azure Logic Apps: An Azure logic app hosts a business process as a workflow.
+ Microsoft Power Automate: Flow also hosts workflows, but it is easier for non-technical staff to use.

Use Event Grid when you need these features:

+ Simplicity: It is straightforward to connect sources to subscribers in Event Grid.
+ Advanced filtering: Subscriptions have close control over the events they receive from a topic.
+ Fan-out: You can subscribe to an unlimited number of endpoints to the same events and topics.
+ Reliability: Event Grid retries event delivery for up to 24 hours for each subscription.
+ Pay-per-event: Pay only for the number of events that you transmit.

but not for delivering a large stream of events. for that use Event Hubs

### Choose Azure Event Hubs

There are certain applications that produce a massive number of events from almost as many sources. Big Data apps

Event Hubs is an intermediary for the publish-subscribe communication pattern. Unlike Event Grid, however, it is optimized for extremely high throughput, a large number of publishers, security, and resiliency.

Event Grid fits perfectly into the publish-subscribe pattern in that it simply manages subscriptions and routes communications to those subscribers, Event Hubs performs quite a few additional services.

+ Partitions
+ Capture (to data lake, blob storage)
+ Authentication (publishers are issued tokens - so can accept events from external systems)

Event Hubs has support for pipelining event streams to other Azure services.

## module: Implement message-based communication workflows with Azure Service Bus (topics and queues)

ASB contained within a namespace, with two encryption keys

if you want to control that specific messages sent to the topic are delivered to particular subscriptions, you can place filters on each subscription in the topic. In the pizza application, for instance, our storefronts are running Universal Windows Platform (UWP) applications. Each store can subscribe to the "OrderCancellation" topic but filter for its own StoreId. We save internet bandwidth because we are not sending unnecessary messages to distant store locations. Meanwhile, the payment processing component subscribes to all our cancellation messages. ie: I want to subscribe to OrderCancelation where storeid = 6.

## module: Communicate between applications with Azure Queue storage

A storage queue is a high-performance message buffer that can act as a broker between the front-end components (the "producers") and the middle tier (the "consumer").

Application components access a queue using a REST API or an Azure-supplied client library. Typically, you will have one or more sender components and one or more receiver components. Sender components add messages to the queue. Receiver components retrieve messages from the front of the queue for processing.

A message in a queue is a byte array of up to 64 KB. 
