# Microservices Project Documentation

Welcome to the documentation for our microservices project! Here you'll find everything you need to know about the architecture, technologies used, API endpoints, database structure, setup instructions, and usage examples.

## Table of Contents

- [Project Overview](#project-overview)
- [Architecture](#architecture)
- [Technologies Used](#technologies-used)
- [API Endpoints](#api-endpoints)
  - [GraphQL](#graphql)
  - [REST](#rest)
- [Database Structure](#database-structure)
- [Setup Instructions](#setup-instructions)
- [Usage Examples](#usage-examples)

## Project Overview

Our project consists of a client-server application utilizing REST and GraphQL. Clients interact with two microservices: the Department Microservice and the Teacher Microservice. An API Gateway serves as an intermediary, facilitating communication with the microservices via gRPC and utilizing Protobuf for data serialization. Apollo is employed for GraphQL implementation. Additionally, a MySQL database named `db_dep_teacher` manages two tables: `teachers` and `departments`.

## Architecture

Our architecture follows a microservices pattern, with dedicated microservices handling departments and teachers. The API Gateway acts as a unified entry point for clients, communicating with the microservices through gRPC. Here's an overview:

```
Client <-> API Gateway <-> Department Microservice
                     <-> Teacher Microservice
```

## Technologies Used

We leverage the following technologies in our project:

- **REST** (Representational State Transfer): An architectural style for designing networked applications.
- **GraphQL**: A query language and runtime for APIs, providing flexible and efficient data fetching.
- **gRPC**: A high-performance, open-source framework for remote procedure calls (RPC).
- **Protobuf** (Protocol Buffers): A language-agnostic binary serialization format for efficient data interchange.
- **Apollo**: An open-source GraphQL toolkit offering libraries and tools for building GraphQL applications.
- **Node.js**: A JavaScript runtime enabling execution of JavaScript code outside a web browser.
- **Express.js**: A web application framework for Node.js simplifying API and web server development.

## API Endpoints

Our project offers both GraphQL and REST endpoints for interacting with the Department and Teacher microservices.

### GraphQL

The GraphQL API, implemented with Apollo, is accessible through the API Gateway running on port 3000. Supported operations include:

#### Queries

- `department(id: Int!): Department`: Retrieve a department by its ID.
- `departments: [Department]`: Retrieve all departments.
- `teacher(id: Int!): Teacher`: Retrieve a teacher by their ID.
- `teachers: [Teacher]`: Retrieve all teachers.

#### Mutations

- `createDepartment(name: String!): Department!`: Create a new department.
- `updateDepartment(id: Int!, name: String!): Department!`: Update an existing department.
- `deleteDepartment(id: Int!): Boolean!`: Delete a department.
- `createTeacher(name: String!, lastname: String!, email: String!, departmentCode: Int!): Teacher!`: Create a new teacher.
- `updateTeacher(id: Int!, name: String, lastname: String, email: String!, departmentCode: Int!): Teacher!`: Update an existing teacher.
- `deleteTeacher(id: Int!): Boolean!`: Delete a teacher.

### REST

The REST API can be accessed through the API Gateway running on port 3000. Available endpoints include:

- **Department Endpoints**:
  - `GET /departments/:id`: Retrieve a department by its ID.
  - `GET /departments`: Retrieve all departments.
  - `POST /department`: Create a new department.
  - `PUT /departments/:id`: Update an existing department.
  - `DELETE /departments/:id`: Delete a department.

- **Teacher Endpoints**:
  - `GET /teachers/:id`: Retrieve a teacher by their ID.
  - `GET /teachers`: Retrieve all teachers.
  - `POST /teacher`: Create a new teacher.
  - `PUT /teachers/:id`: Update an existing teacher.
  - `DELETE /teachers/:id`: Delete a teacher.
  - `GET /teachers/department/:id`: Retrieve teachers by department ID.

## Database Structure

Our project includes a MySQL database named `db_dep_teacher` comprising two tables:

- **teachers**: Stores information about teachers.
  - `id` (INT): Teacher ID (primary key).
  - `name` (VARCHAR): Teacher's first name.
  - `lastname` (VARCHAR): Teacher's last name.
  - `email` (VARCHAR): Teacher's email address.
  - `departmentCode` (INT): Foreign key referencing the `departments` table.

- **departments**: Stores information about departments.
  - `id` (INT): Department ID (primary key).
  - `name` (VARCHAR): Department name.

## Setup Instructions

To set up the project locally, follow these steps:

1. Clone the repository from our Git repository.
2. Install the required dependencies using your preferred package manager.
3. Set up the MySQL database named `db_dep_teacher` and import the provided file.
4. Start the Department Microservice on port 5005.
5. Start the Teacher Microservice on port 5005.
6. Start the API Gateway on port 3000.
7. The project is now set up locally and ready for use.

## Usage Examples

Below are some examples demonstrating interaction with our project's API endpoints:

### GraphQL Examples

- Retrieve all departments:

  ```graphql
  query {
    departments {
      id
      name
    }
  }
  ```

- Create a new teacher:

  ```graphql
  mutation {
    createTeacher(name: "John", lastname: "Doe", email: "john.doe@example.com", departmentCode: 1) {
      id
      name
      lastname
      email
    }
  }
  ```

### REST Examples

- Retrieve a teacher by ID:

  ```
  GET /teachers/1
  ```

- Update an existing department:

  ```
  PUT /departments/2
  Body: { "name": "New Department Name" }
  ```

For additional details on available operations and request/response formats, refer to the API endpoints section.
