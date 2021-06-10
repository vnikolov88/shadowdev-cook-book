# Vertical Slice Architecture (Advanced CQRS)

## Traditional monoliths
In a traditional monolith application developers often follow traditional architecture patterns to reduce complexity and preserve maintainability for as much as possible. A traditional clean/onion/layered architecture tries to provide clear separation of concerns by splitting the code in to horizontal or concentric layers to control the flow of data from the front-end to the back. This however creates a set of one size fits all rules around how we separate code and how we write features. Many times this leads to performance and maintenance degradation, alongside this the code base can become herd to navigate for newcomers. 

## Microservice and Service Oriented Architecture
In the past decade developers have been on a quest to achieve low coupling and strong cohesion in there code. Splitting the code into small units that encapsulate business logic and data persistence in to one entity. This in most cases require some kind of a centralized communication method, event bus or a service registry. This makes implementing specific features in the best way possible, easy as you don't need to concern yourself with anything outside of your service boundary and rely on the other services to handle there part respectively. This shift in architecture is highly scalable and if done correctly leads to good stability and incremental updates. However it's not ideal in every case. the minimum level of complexity is significantly hire then a monolith application. Sometimes the complexity is so high it's impractical to run the whole code base on one machine as DevOps tasks start to overwhelm development ones. 

## Feature boundaries
Most projects require an agile approach to developing new features and the self contained nature of Vertical Slice Architecture makes focusing only on what you are building very easy. CQRS as a pattern can be very useful for separating our read and write concerns but most people that practice it still rely on parts from the concentric design like repositories and controllers. Thanks to tools like MediatoR and MediatR.AspNetCore.Endpoints we can create self contained features that allow us to easily write new functionality in isolation of the other features in our code-base.

Jimmy Bogard describes it well in his blog, where he gives examples of a couple of query and a couple of command operations, each focused on the **value** it delivers and not trying to follow an arbitrary one size fits all pattern. 

<IMG  src="https://jimmybogardsblog.blob.core.windows.net/jimmybogardsblog/3/2018/Picture0031.png"/>

Patterns and Architecture in general should naturally evolve from the code and is not something that should be enforced at all costs. Basically if the code fight's you are probably pushing in the wrong direction.

## ASP.Net implementation
Using MediatoR and MediatR.AspNetCore.Endpoints we are able to create a self contained feature in a single file.

```csharp
using System;
using System.Threading;
using System.Threading.Tasks;
using MediatR;
using Microsoft.AspNetCore.Mvc;

namespace BasicSample.Features.Demo
{
    public class CurrentTime
    {
        public class Request : IRequest<Response>
        {
            public int Id { get; set; }
        }

        public class RequestHandler : IRequestHandler<Request, Response>
        {
            [HttpPost("demo/current-time")]
            public async Task<Response> Handle(Request request, CancellationToken cancellationToken)
            {
                await Task.Delay(200);

                return new Response
                {
                    Name = "Current Time",
                    Timestamp = DateTime.Now
                };
            }
        }

        public class Response
        {
            public string Name { get; set; }

            public DateTime Timestamp { get; set; }
        }
    }
}
```
The reference design will include probably AutoMapper in witch case you can create a separate mapping configuration file that folds neatly in VS 2019 by following the naming convention of
```
[FeatureName].cs
[FeatureName].MappingProfile.cs
```

### DTO's and shared models
The concept of Data Transfer Objects is a good practice overall but many developers try to apply strict OOP principles when designing them. In a traditional CQRS architecture DTO's are held in a separate folder or shared library. This many times leads to reuse, which most of you reading are probably thinking, "well, duh...", but reusing something just because it looks like something else now is a terrible idea. If we have two identically structured responses using the same DTO for both of them seems like a good idea at fist, but what if one of the requests no longer needs part of the response, we are going to need to refactor both of them, if this is on a scale of tens of features that reuse the same DTO your job becomes a lot harder and testing effort is increased. Developers should not be afraid of duplicating Request or Response DTO's as at the end of the day even if they look the same now they are logically different and at some point very soon, will probably look drastically different.

## Composite UI
This particular architecture falls nicely with the emerging trend of composite UI architecture. This is out of the scope of this article but if someone is interested I suggest they read up on:

- https://github.com/tannerlinsley/react-table
- https://docs.microsoft.com/en-us/dotnet/architecture/microservices/architect-microservice-container-applications/microservice-based-composite-ui-shape-layout
