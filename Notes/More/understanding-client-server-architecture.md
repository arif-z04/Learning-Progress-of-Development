# **Client-Server Architecture**

Client-Server Architecture is a software architecture model where two main components communicate over a network:

1. **Client:** Requests services or resources.
2. **Server:** Receives requests, processes them, and sends responses.

In simple terms:

> The client asks for something, and the server provides it.

For example, when you open Facebook in your browser, your browser acts as the client and Facebook's backend servers process your requests.

## **1. Basic Architecture**

[Client-Server Architecture Explained | Colabcodes](https://images.openai.com/static-rsc-4/66TnuPoShqMKjqS_50RcXqD2Xs8vzIBkBcdi3u3kTKkbkHLuJZNyA_4v5PkXXNcF_Rl4V10v13MY6uFBrfy1eAiH-mJaH2mSqfqYfD1vyw-5YH5mERjNjotBUISbQygczJePHz7usqJ_DoOv4_H-kUGBW251W2-JEgzxENdVhkc?purpose=inline)

[colabcodes.com](https://www.colabcodes.com/post/client-server-architecture?utm_source=chatgpt.com)

The communication generally follows this process:

1. Client sends a request.
2. Request travels through the network.
3. Server receives the request.
4. Server processes business logic.
5. Server communicates with the database if necessary.
6. Server sends a response.
7. Client displays the result.

### **Example: Logging into a website**

Suppose you enter:

```
Email: david@example.com
Password: ********
```

The process:

```
Browser (Client)
      |
      | POST /api/login
      v
Backend Server
      |
      | Validate credentials
      v
Database
      |
      | Return user information
      v
Backend Server
      |
      | HTTP Response
      v
Browser (Client)
```

The server validates your credentials against stored password hashes and returns an appropriate response.

## **2. Main Components**

### **A. Client**

The client is the application or device that initiates requests.

Examples:

- Web browsers (Chrome, Firefox).
- Mobile applications.
- Desktop applications.
- IoT devices.
- Command-line applications.

Responsibilities:

- Display user interfaces.
- Collect user input.
- Send requests to servers.
- Receive and display responses.
- Perform client-side validation.

Technologies:

| Purpose            | Technologies          |
| ------------------ | --------------------- |
| Web frontend       | HTML, CSS, JavaScript |
| Frontend framework | React                 |
| Mobile             | Flutter               |
| Desktop            | Electron, .NET        |
| API communication  | HTTP, HTTPS           |

### **B. Server**

The server receives client requests and provides services.

Responsibilities:

- Process incoming requests.
- Execute business logic.
- Authenticate users.
- Authorize access.
- Validate data.
- Communicate with databases.
- Return responses.

Examples of backend technologies:

- ASP.NET Core
- Node.js / Express
- Django
- Spring Boot
- Laravel

### **C. Database**

A database stores application information persistently.

Examples:

- PostgreSQL
- MySQL
- Oracle Database
- Microsoft SQL Server
- MongoDB

The server typically communicates with the database rather than allowing the client to access it directly.

## **3. How Client and Server Communicate**

One of the most common communication protocols is HTTP (Hypertext Transfer Protocol).

Consider this example:

**Client request:**

```
GET /api/products HTTP/1.1
Host: example.com
Accept: application/json
```

**Server response:**

```
HTTP/1.1 200 OK
Content-Type: application/json

[
  {
    "id": 1,
    "name": "Laptop",
    "price": 75000
  }
]
```

The client requests products, and the server returns product information in JSON format.

### **Common HTTP methods**

| Method | Purpose               |
| ------ | --------------------- |
| GET    | Retrieve data         |
| POST   | Create or submit data |
| PUT    | Replace existing data |
| PATCH  | Partially update data |
| DELETE | Delete data           |

### **Common HTTP status codes**

| Status | Meaning               |
| ------ | --------------------- |
| 200    | OK                    |
| 201    | Created               |
| 400    | Bad Request           |
| 401    | Unauthorized          |
| 403    | Forbidden             |
| 404    | Not Found             |
| 500    | Internal Server Error |
| 503    | Service Unavailable   |

## **4. Types of Client-Server Architecture**

### **1-Tier Architecture**

[Fundamentals of Software Architecture — single tier, two tier, three tier and n-tier architecture. | by Syed Amaan | Medium](https://images.openai.com/static-rsc-4/_RyUNmPAd3JLnJGVGa3JiR1zh-fHGLg7a4P7DvFU6oBYGUvDKzoCSxisxg2rcoaRhcRUKbiGG1PvD1pSX5hlDSR5R-dCMjtpcaW0ZCp8AjOFKx0EKh_JdJbYH_N4XvGvNydd8eno93yDLoBGFhw04YZWLTr_T_2P11x94mrQjtY?purpose=inline)

[medium.com](https://medium.com/%40syedamaann/fundamentals-of-software-architecture-single-tier-two-tier-three-tier-and-n-tier-architecture-3d7c4c7da1?utm_source=chatgpt.com)

Everything runs on one machine.

Example:

\- A standalone desktop application with a local database.

### **2-Tier Architecture**

[DBMS Architecture: Everything You Need to Know](https://images.openai.com/static-rsc-4/b8r4ZE_ZyXfXMYNAAvNj-OOrOQtq0oJ7fng5sueGHYWEYmDHoclK4H-y-41TgOxpvfgdQfdTsyuDe1n1wWMOehkywsUGGVyFquJ0v4Ip01uRJhVV4Y6gcNho3evZE-xY_zCh09aQzv9-CsKvX21vyHI6quMgc2C_VuWDc1FN9gU?purpose=inline)

[webandcrafts.com](https://webandcrafts.com/blog/dbms-architecture?utm_source=chatgpt.com)

Two layers:

1. Client application.
2. Database server.

The client communicates directly with the database.

Example:

\- A desktop banking application connected directly to a database server.

**Problem:** Exposing database access to clients can create security and maintenance problems.

### **3-Tier Architecture**

Common in modern web applications

[Medium](https://images.openai.com/static-rsc-4/6jH7wip2Rzp82DaHMLAdJhOOH_c36jgynO-J858YtR9Ahf_46I1qYmET01ofstNF750GAWK67eTXc8g_X9cfTj9-up6_58moW0IwUjIckb64XCx7OD6zG3Y2TSf7HRGtGm-8RhZXJOkRdryMAEZgWBC0DcvdFoZTgVzkh8BMIj4?purpose=inline)

[medium.com](https://medium.com/%40kaveeshadhanasekara/demystifying-3-tier-application-architecture-6b3b8495d616?utm_source=chatgpt.com)

Three layers:

1. **Presentation Layer:** User interface.
2. **Application Layer:** Business logic and processing.
3. **Data Layer:** Database and data storage.

Example:

| Layer        | Technology           |
| ------------ | -------------------- |
| Presentation | React                |
| Application  | ASP.NET Core Web API |
| Data         | PostgreSQL           |

This architecture separates responsibilities and makes applications easier to maintain.

## **5. Real-World Example: E-commerce Website**

Imagine you're building an online shopping platform.

[API Test Strategy: 7 Proven Practices for High-Impact Results](https://images.openai.com/static-rsc-4/KoGiQu3g4rCgOcxcQsOCODnE1Hz39AlxLRBqnyRfBZe_YrCkWMLYWV-toKSwKJcSXD2sXhyddQNqqyepC2U-329CO3n6gFheHKmsBTNghIPRhCm898VSYhjWI-HnTgDi-uckWmpR2kV2hvvGRcYSKFQaWy75djiBTIOpFguPP34?purpose=inline)

[frugaltesting.com](https://www.frugaltesting.com/blog/api-test-strategy-7-proven-practices-for-high-impact-results?utm_source=chatgpt.com)

When a customer purchases a product:

1. Customer opens the website.
2. Frontend requests product information.
3. Backend retrieves products from the database.
4. Customer adds a product to the cart.
5. Backend validates product availability.
6. Customer submits an order.
7. Backend creates the order and processes payment through a payment provider.
8. Backend updates order status.
9. Frontend displays order confirmation.

Notice that the frontend does not directly modify the database.

## **6. Important Concepts You Should Understand**

| Concept          | Explanation                                             |
| ---------------- | ------------------------------------------------------- |
| API              | Interface through which software components communicate |
| REST API         | An API architectural style commonly using HTTP          |
| HTTP/HTTPS       | Protocols for web communication                         |
| Request/Response | Communication pattern between client and server         |
| Authentication   | Identifying who the user is                             |
| Authorization    | Determining what the user can access                    |
| Middleware       | Components that process requests in a pipeline          |
| Load Balancer    | Distributes incoming requests across servers            |
| Caching          | Stores frequently accessed data for faster retrieval    |
| Scalability      | Ability to handle increasing workloads                  |

## **7. What Happens When Millions of Users Access a Server?**

A single server may struggle when too many clients send requests simultaneously.

Modern systems use additional infrastructure:

[How to scale a Nodejs app based on number of users | Adrian Mejia Blog](https://images.openai.com/static-rsc-4/7LKh6fdUa7y4eZtU3fIzNhgBxwqfWYLBuSHUlDt7fGiqRHVOoou-ddlj8vKEBblvIw3XhDObcCptGFlnzBUHjGEpNt7WKMiavgHX4dP95gEqsaEm6qRZ4JGbmZilDiawjdUqLZoCjzoFqx6C8yvWw-XpY00BzVtCgNVfMO0y0Ag?purpose=inline)

[adrianmejia.com](https://adrianmejia.com/how-to-scale-a-nodejs-app-based-on-number-of-users/?utm_source=chatgpt.com)

Typical architecture:

```
         Millions of Clients
                 |
                 v
          Load Balancer
                 |
        +--------+--------+
        |        |        |
        v        v        v
      Server  Server  Server
        |        |        |
        +--------+--------+
                 |
                 v
               Cache
                 |
                 v
              Database
```

Some technologies used:

- Nginx: Reverse proxy and load balancing.
- Redis: Caching.
- Docker: Application containerization.
- Kubernetes: Container orchestration.
- PostgreSQL: Database.
- Cloudflare: CDN and edge protection.

This is where system design becomes important.

## **8. Practical Implementation: Your Full-Stack Stack**

Let's connect the architecture to a real application using your intended technologies.

Client / Presentation Layer

**React + Tailwind CSS**

User interface running in the browser

HTTP / HTTPS + JSON

Application / Business Layer

**ASP.NET Core Web API**

Controllers → Services → Business Logic

Entity Framework Core

Data Layer

**PostgreSQL**

Persistent application data

For example, your React frontend might call:

```
const response = await fetch(
  "https://localhost:7001/api/products"
);

const products = await response.json();

console.log(products);
```

Your ASP.NET Core backend:

```
[ApiController]
[Route("api/[controller]")]
public class ProductsController : ControllerBase
{
    [HttpGet]
    public IActionResult GetProducts()
    {
        var products = new[]
        {
            new { Id = 1, Name = "Laptop", Price = 75000 },
            new { Id = 2, Name = "Mouse", Price = 800 }
        };

        return Ok(products);
    }
}
```

The browser sends an HTTP request, ASP.NET Core executes the endpoint, and the response returns as JSON.

## **9. Advantages and Disadvantages**

| Advantages                           | Disadvantages                   |
| ------------------------------------ | ------------------------------- |
| Centralized data management          | Server can become a bottleneck  |
| Easier maintenance                   | Network dependency              |
| Better access control                | Server downtime affects clients |
| Multiple clients can use one service | Requires server infrastructure  |
| Easier scalability                   | Network latency                 |

## **10. Knowledge Check**

**Test your understanding**

0/4 answered

**1. Which component usually handles business logic?**

Client

Application Server

Browser

Monitor



**2. In a 3-tier architecture, where is the database located?**

Presentation Layer

Application Layer

Data Layer

Client Layer



**3. Which HTTP method is commonly used to retrieve data?**

POST

DELETE

GET

PATCH



**4. Should a React frontend normally connect directly to a production database?**

Yes

No



Check answers

**Next learning topic:** Understanding how a browser communicates with a backend through HTTP, DNS, TCP/IP, ports, and REST APIs. This will help you understand what actually happens behind every full-stack application.