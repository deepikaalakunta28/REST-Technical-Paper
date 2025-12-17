### 1.REST
- REST (Representational State Transfer) is not a single technology.
- It is a set of architectural principles and design practices used to build HTTP-based APIs.
### What is a resource?
A resource is simply data.
Examples of resources:
- Employee
- User
- Order
- Product
- Each resource is identified using a URL.

Examples:
```
/employees        → all employees
/employees/21     → one employee
```
### 2.HTTP Methods (How we work with resources)
REST uses existing HTTP methods to say what we want to do with a resource.
```
| Method | Meaning              |
| ------ | -------------------- |
| GET    | Read data            |
| POST   | Create new data      |
| PUT    | Update existing data |
| PATCH  | Update part of data  |
| DELETE | Remove data          |
```
### 3.HTTP Status Codes (How server replies)
The server uses status codes to tell the result of a request.
##### Main groups:
- 2xx → Success
- 4xx → Client error
- 5xx → Server error
##### Common examples:
- 200 → OK
- 201 → Created
- 400 → Bad Request
- 404 → Not Found
- 500 → Server Error
### 4. Resource Representation (JSON)
REST APIs exchange data in JSON format.
```
{
  "data": {
    "id": 21,
    "name": "Larry"
  }
}
```
- Data is wrapped in a data object
- JSON represents the resource state
### 5.Statelessness
REST APIs are stateless.
##### What does that mean?
- Server does not remember previous requests
- Each request is complete by itself
##### Example:
- Every request contains authentication info
- No server-side session
### 6. Client–Server Separation (Detailed & Clear)
REST follows a client–server architecture.

**Client** → handles UI, user input, presentation

**Server** → handles business logic, data processing, database access
They communicate only through HTTP requests and responses.
```
Example
GET /employees/21
```
**Client**:
- Sends request
- Does not know how data is stored
**Server**:
- Fetches data
- Applies business logic
- Returns response
```
{
  "data": {
    "id": 21,
    "name": "Larry"
  }
}
```
### 7.Resource Relationships
REST defines how related resources are accessed.
Using Links (HATEOAS)
```
{
  "data": {
    "id": 1,
    "name": "Larry",
    "links": {
      "manager": "/employees/5"
    }
  }
}
```
- The server provides URLs for related resources
### 8. Pagination
REST APIs must not return all data at once.
**Offset-based pagination**
```
GET /employees?offset=0&limit=10
```
**Keyset (cursor-based) pagination**
```
{
  "pagination": {
    "continuationToken": "1504224000000_10"
  },
  "links": {
    "next": "/employees?continue=1504224000000_10"
  }
}
```
### 9.What is a resource in REST and how is it identified?
A resource in REST represents any data or entity that can be accessed through an API, such as a user, employee, or order. Resources are identified using Uniform Resource Locators (URLs). Each URL uniquely represents either a collection of resources or a single resource, enabling consistent and predictable access patterns in RESTful systems.
### 10.Why is statelessness an important principle of REST architecture?
Statelessness means that each client request contains all the information required for the server to process it, and the server does not store client-specific session data. This principle improves scalability and reliability, as servers can handle requests independently and easily recover from failures. Statelessness also allows load balancing and simplifies server-side implementation.
### 11. Error Handling
Errors are returned using proper status codes and messages.
```
{
  "error": {
    "code": 400,
    "message": "Invalid request data"
  }
}
```
This helps clients understand failures clearly.
