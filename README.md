# Employee-Management
Phase 1 – MuleSoft Fundamentals
________________________________________
1. Introduction
This document describes the design and implementation of an Employee Management System using MuleSoft Anypoint Platform, following the API led Connectivity approach.
The system enables CRUD operations (Create, Retrieve, Update, Delete) on employee records through layered APIs, demonstrating fundamental MuleSoft concepts.
________________________________________
2. Use Case Statement
Phase 1: MuleSoft Fundamentals
Objective
To understand and implement core MuleSoft concepts including API led connectivity, REST API development, Mule application structure, and DataWeave transformations.
Detailed Use Case
Develop a layered API solution to manage employee records, enabling creation, retrieval, update, and deletion of employee data.
________________________________________
3. Focus Areas Covered
This project covers the following MuleSoft fundamentals:
•	Anypoint Platform overview
•	API led Connectivity 
o	System API
o	Process API
o	Experience API
•	Mule application structure and flows
•	DataWeave 2.0 fundamentals
•	REST API development using HTTP Listener
•	APIKit with RAML
•	Centralized error handling
________________________________________
4. Tools & Technologies Used
Tool / System	Purpose
MuleSoft Anypoint Studio	API development
HTTP Listener	REST API exposure
APIKit	RAML based routing
DataWeave 2.0	Data transformation
MySQL	Backend database
Postman	API testing
________________________________________
5. API Led Connectivity Architecture
The solution follows MuleSoft’s API led architecture, ensuring loose coupling and scalability.
Postman
        ↓
Experience API (8081)
        ↓
Process API (8082)
        ↓
System API (8083)
        ↓
MySQL Database


Layer Responsibilities
Experience API
•	Exposes APIs to consumers
•	Handles request routing
Process API
•	Applies business rules  and validations
•	Transforms data using DataWeave
•	Orchestrates calls to System API
System API
•	Handles database operations
•	Performs CRUD using MySQL
•	Returns database formatted responses
________________________________________
6. API Specifications (RAML)
All APIs expose the following resources:
Base Resource
/employees
/employees/{employeeId}
Supported Operations
•	POST /employees
•	GET /employees
•	GET /employees/{employeeId}
•	PUT /employees/{employeeId}
•	DELETE /employees/{employeeId}
Employee Data Model
{
  "id": "string",
  "firstName": "string",
  "lastName": "string",
  "email": "string",
  "department": "string",
  "designation": "string",
  "salary": "number",
  "createdAt": "datetime"
}
________________________________________
7. Experience API – employee-exp-api
Purpose
Acts as the entry layer for client requests.
Key Details
•	Port: 8081
•	Uses HTTP Listener and APIKit
•	Forwards requests to Process API
•	Logs incoming requests
________________________________________
8. Process API – employee-proc-api
Purpose
Handles business logic and validation.
Validations Implemented
•	Email format validation
•	Salary must be greater than zero
•	Allowed departments: 
o	Engineering
o	HR
o	Finance
o	Marketing
o	Operations
DataWeave Transformations
•	Converts email to lowercase
•	Adds createdAt timestamp
•	Maps incoming payload to System API format
Error Handling
•	Validation errors 
•	Standard errors
________________________________________
9. System API – employee-sys-api
Purpose
Handles database interaction with MySQL.
Key Details
•	Port: 8083
•	Uses DB Connector (MySQL)
•	Performs CRUD operations
Database Operations
•	Insert employee
•	Select all or by ID
•	Update employee
•	Delete employee
________________________________________
10. Database Design (MySQL)
Database Creation
CREATE DATABASE employee_db;
USE employee_db;
Table Structure
CREATE TABLE employees (
    id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(100) NOT NULL,
    last_name VARCHAR(100) NOT NULL,
    email VARCHAR(150) UNIQUE NOT NULL,
    department VARCHAR(100),
    designation VARCHAR(100),
    salary DECIMAL(10,2),
    created_at DATETIME DEFAULT NOW()
);
Sample Data
INSERT INTO employees
(first_name, last_name, email, department, designation, salary)
VALUES
('Chand', 'Kriti', 'chand.kriti@company.com',
'Engineering', 'Software Engineer', 75000);
``
________________________________________
11. Error Handling Strategy
All APIs implement global error handlers to maintain consistency.
Common Error Response
{
  "code": 404,
  "message": "Resource not found"
}
Supported Error Codes
Error Type	HTTP Status
Bad Request	400
Validation Error	422
Not Found	404
Method Not Allowed	405
Database Connectivity	503
Internal Server Error	500
________________________________________
12. End to End Flow Summary
1.	Client sends request via Postman
2.	Experience API receives request
3.	Process API validates and transforms data
4.	System API interacts with MySQL
5.	Response propagates back to client
________________________________________
13. Deliverables
•	✅ RAML specifications for all APIs
•	✅ Experience, Process, and System APIs implemented
•	✅ MySQL database integration
•	✅ Centralized error handling
•	✅ Postman ready REST APIs
________________________________________
14. Conclusion
This project successfully demonstrates MuleSoft Phase 1 fundamentals by implementing a scalable API led Employee Management System.
It follows enterprise best practices, ensures separation of concerns, and provides a strong foundation for advanced MuleSoft concepts.

