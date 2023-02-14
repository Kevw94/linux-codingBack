# Backend structure explication
>>>

## Module definition
Each application has at least one module, a root module (cf. `src/app.module.ts`).
A module is a collection of related components, such as controllers, models, and views, that work together to provide a specific functionality or feature.
The current backend framework is NEST.js and is perfect to manage the `Model-View-Controller` (MVC) framework.
Each folder located in `src/base` possess a `folder.module.ts` exporting at least a `Service` and a `Repository`.
The module controller will stay attached to the `folder.module.ts` and will not be exported outside of its range.

## Controller definition
A `Controller` is a `core component` of a `Model-View-Controller` framework that handles user interactions and incoming requests.
Its goal is to retrieves sanitized data, pass and await data from its model `Service` and send a specific data back to the client in a desired format.
In a NEST application, the controller is attached to the module and doesn't go outside of it.
Note : A module can contains multiple controllers (cf. Use case can concern `api versionning`).

## Service definition
A `Service` is a `core component` of a `Model-View-Controller` that provides a specific functionality or feature to other components in the application.
The components used by the Service can be : `Service` : `Controller` : `Middlewares` : `Guard` : `Strategy`...
For this NEST application, its best that we keep it contenerized even if it's exported by a `Module`.
Important note : That does not concern the `providers` located in `src/common/providers`, but they act the same way.

## Repository definition
A repository is an `optional component` of a `Model-View-Controller` that provides an interface of multiple methods for accessing data from a database.
It is opitional because it depends what you're using to comunicate with the database and what database you are using.
For this NEST application, we could potentially use `mongoose` with what we call `schema` but the utility of the library if extremely small.

## Middleware definition
A middleware is software that acts as an intermediary between different systems or software components. 
It can be used to handle incoming requests, perform preliminary operations on those requests, and route them to the appropriate components of the framework for further processing. Middleware can also be used to perform post-processing operations on responses generated by the framework before sending them back to the client. In general, middleware in an MVC framework is used to add additional functionality to the framework, such as session management, access control, or error handling.

## DTO definition
Data Transfer Object (DTO) is an object that carries data between layers or components of an application.
Coupled with a validator library, they're used to validate or reject the data received before processing the request.

## Events definition
An emitter is a software component that is used to send events or messages to other components within a system. 
In our case, an emitter might be used to send notifications to other parts of the system when certain events are needed, such as :
Write data to a sub-party software hosted online that needs a request API, like an `email service` for example.

>>>

# Backend structure visual : NEST MODULE

```bash
├── moduleName
│   ├── dto
│   │   ├── moduleName.dto.ts
│   ├── events
│   │   ├── moduleName.events.ts
│   ├── interfaces
│   │   ├── moduleName.interface.ts
│   ├── moduleName.controller.ts
│   ├── moduleName.module.ts # core of the folder, import, provide and export
│   ├── moduleName.repository.ts # optional
│   └── moduleName.service.ts
│   
├── moduleName2
│   └── ... repeat
└── ... repeat
```