#### Describe the fundamental differences between SQL and NoSQL databases. Why might MongoDB be preferred in certain situations?

SQL databases are relational databases that use Structured Query Language for defining and manipulating data

They have a fixed schema and store data in tables, like a spreadsheet

e.g.
- MySQL
- PostgreSQL
- SQL Server

NoSQL databases are non-relational databases that can store and retrieve data in ways other than tabular relations

They can have a dynamic schema and can be document-based, key-value pairs, graph databases or wide-column stores

e,g,
- MongoDB
- CouchDB
- Redis

MongoDB might be preferred in situations where:
- Rapid development is required and the schema may evolve
- The data is hierarchical or document-oriented
- The application requires scalability and can benefit from [[Horizontal Scaling]] capabilities

#### How do you handle security concerns when designing APIs, especially when they interact with a database like MongoDB?

Implement authentication and authorization mechanisms such as JWT or OAuth to ensure only authorized users can access the API

Use HTTPS to encrypt data in transit

Regularly backup the database and update MongoDB to the latest version to benefit from security patches

#### In C#, explain how you'd go about building an API endpoint to retrieve user data from a MongoDB instance

You would first need to setup a connection to MongoDB using a driver or library such as the MongoDB ..NET driver

In your API application, you could define a route that maps to a controller method

In this method, use the MongoDB driver to query the database for the user with the specified ID

Return the retrieved user data as a JSON response

#### Discuss the importance of indexing in MongoDB and how it can affect API performance.

#### How would you handle version control in a collaborative environment, especially when multiple devs are working on the same API?