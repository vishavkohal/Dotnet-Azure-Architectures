# Dotnet-Azure-Architectures

Architectural setups using .NET C#, tailored for different services and purposes on Azure. These examples will highlight varying approaches such as microservices, serverless architecture with Durable Functions, and an API-centric web application.

### 1. Microservices Architecture on Azure Kubernetes Service (AKS)

In a microservices architecture, the application is divided into small, independently deployable services, each running in its own process and communicating with lightweight mechanisms, often an HTTP API. Azure Kubernetes Service (AKS) can be utilized to orchestrate and manage these containerized services.

```
MicroservicesSolution/
│
├── src/
│   ├── ServiceA/                     # Microservice A
│   │   ├── Controllers/              # Web API controllers
│   │   ├── Models/                   # Domain models
│   │   ├── Services/                 # Business logic
│   │   └── Dockerfile                # Docker container configuration
│   ├── ServiceB/                     # Microservice B
│   │   ├── Controllers/              # Similar structure to ServiceA
│   │   ├── Models/
│   │   ├── Services/
│   │   └── Dockerfile
│   └── SharedKernel/                 # Shared library, if there's common logic
│       ├── Models/
│       └── Interfaces/
│
├── deployment/
│   ├── serviceA-deployment.yaml      # Kubernetes deployment spec for Service A
│   └── serviceB-deployment.yaml      # Kubernetes deployment spec for Service B
│
└── ingress.yaml                      # For managing external access to the services
```

### 2. Serverless Architecture with Azure Durable Functions

Azure Durable Functions extend Azure Functions with stateful capabilities and orchestration functions to chain together sequences of functions, fan out/fan in patterns, etc. Ideal for complex coordination of function executions.

```
DurableFunctionsApp/
│
├── StarterFunction/              # HTTP triggered function to start orchestrations
├── OrchestratorFunction/         # Orchestrates calls to other functions
├── ActivityFunctions/            # Contains various activity functions called by orchestrator
│   ├── Function1/
│   ├── Function2/
│   └── ...
└── Shared/                       # Shared code, models, helpers, etc.
    ├── Models/
    └── Helpers/
```

### 3. API-Centric Web Application Using Azure App Service

For web applications that primarily serve an API, structuring around ASP.NET Core Web API with a focus on Domain-Driven Design (DDD) elements helps organize by domain functionality.

```
ApiCentricWebApp/
│
├── src/
│   ├── WebAPI/                        # ASP.NET Core Web API project
│   │   ├── Controllers/               # API controllers
│   │   ├── Properties/
│   │   └── appsettings.json           # Configuration settings
│   ├── Application/                   # Handles use cases, DTOs, interfaces
│   ├── Domain/                        # Domain models, business rules
│   └── Infrastructure/                # Data access layer, EF Core, migrations
│       ├── Persistence/
│       │   ├── Repositories/          # Implementation of repository interfaces
│       │   └── ApplicationDbContext.cs# EF Core DbContext
│       └── Services/                  # External services like email, notification
└── tests/                             # Unit and integration tests
    ├── Domain.UnitTests/
    ├── Application.IntegrationTests/
    └── WebAPI.FunctionalTests/
```

### Summary
Each architectural pattern is suited to particular use cases:
- **Microservices** are ideal for large, complex systems requiring high scalability and agility. AKS facilitates management and scaling.
- **Serverless and Durable Functions** offer a cost-effective, scalable way to run workflows with complex execution logic without managing infrastructure.
- **API-centric web application** architectures suit applications that primarily serve web content and APIs, leveraging domain-driven designs for maintainability.

Choosing the right architecture depends on the specific requirements, team expertise, and long-term maintenance considerations of the project.
