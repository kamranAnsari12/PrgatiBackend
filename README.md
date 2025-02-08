# PrgatiBackend
<!-- this is LLD backend project -->
1. System Architecture

Backend: Node.js with Express.js

Database: MongoDB (with Mongoose ORM)

Authentication: JWT for Admin & Providers

Caching: Redis for performance optimization

Search & Filters: MongoDB Aggregation & Indexing

Deployment: Initially Monolithic, scalable to Microservices

2. Database Schema (MongoDB)

2.1 Users Collection

{
  "_id": ObjectId,
  "name": String,
  "email": String,
  "password": String,
  "role": Enum("admin", "provider", "public"),
  "createdAt": Date,
  "updatedAt": Date
}

2.2 Services Collection

{
  "_id": ObjectId,
  "name": String,
  "category": String,
  "description": String,
  "image": String,
  "createdAt": Date,
  "updatedAt": Date
}

2.3 Providers Collection

{
  "_id": ObjectId,
  "providerName": String,
  "email": String,
  "password": String,
  "serviceId": ObjectId (Ref: Services),
  "address": String,
  "phone": String,
  "status": Enum("pending", "approved", "rejected"),
  "image": String,
  "createdAt": Date,
  "updatedAt": Date
}

2.4 Reviews Collection

{
  "_id": ObjectId,
  "providerId": ObjectId (Ref: Providers),
  "userId": ObjectId (Ref: Users),
  "rating": Number (1-5),
  "comment": String,
  "createdAt": Date,
  "updatedAt": Date
}

3. API Endpoints

3.1 Authentication APIs

POST /auth/register - Provider Registration

POST /auth/login - Login (Admin & Provider)

3.2 Admin APIs

GET /admin/providers - List all providers (with status filtering)

PUT /admin/providers/:id********/approve - Approve a provider

DELETE /admin/providers/************:id - Delete a provider

POST /admin/services - Add new service

PUT /admin/services/************:id - Update service details

DELETE /admin/services/************:id - Delete a service

3.3 Provider APIs

GET /provider/profile - Get provider details

PUT /provider/profile - Update name, address, and image

POST /provider/request-update - Request admin to update other details

3.4 Public User APIs

GET /services - List services (with filters by category, location, etc.)

GET /providers/************:serviceId - List providers offering a service

GET /reviews/************:providerId - Get reviews of a provider

POST /reviews - Submit a review (authenticated users only)

4. Caching & Pagination

Redis will cache frequently requested services and providers

Pagination using limit and skip in MongoDB queries

5. Error Handling & Logging

Centralized error handler for API responses

Winston for logging

6. Future Scalability Considerations

Microservices architecture can be adopted later

Separate databases for authentication and services

This LLD provides a structured backend design for the Service Provider project.



