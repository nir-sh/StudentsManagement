# StudentsManagement
# **Student Management System**

A RESTful API application built with Spring Boot for managing students and their grades. This system includes endpoints for CRUD operations on students and their grades, along with advanced filtering capabilities.

## **Features**

- **Student Management**: Add, update, view, and delete students.
- **Grade Management**: Add, update, and delete grades for students.
- **Search Functionality**: Filter students by name, birth date range, SAT score range, and average score.
- **Image Upload**: Upload profile pictures for students.
- **SMS Notifications**: Send SMS messages to all students.

---

## **Installation and Setup**

### **Prerequisites**

- Java 11 or higher
- Maven
- PostgreSQL database
- Docker (optional for containerized deployment)

---

### **Running the Application**

1. **Clone the Repository**:

   ```bash
   git clone <repository_url>
   cd <repository_directory>
   
2. **Database Setup:**
 Ensure a PostgreSQL database is running. Create a database named students_db. Configure your credentials in the application.properties file as described below.

3. **Prepare the Configuration:**
 Copy the provided application.properties.template to application.properties and fill in your database details and secrets.

**Example** application.properties.template:
```
spring.datasource.url=jdbc:postgresql://<DB_HOST>:5432/<DB_NAME>
spring.datasource.username=<DB_USERNAME>
spring.datasource.password=<DB_PASSWORD>
spring.jpa.hibernate.ddl-auto=update

aws.accessKeyId=<AWS_ACCESS_KEY>
aws.secretKey=<AWS_SECRET_KEY>
aws.s3.bucketName=<S3_BUCKET_NAME>

jwt.secret=<JWT_SECRET>
jwt.expirationMs=<JWT_EXPIRATION_TIME>
```

4. **Build the Project:**
```mvn clean install```

5. **Run the Application:**
```
java -jar target/<your-app-name>.jar
```
### **Run with Docker**

To simplify deployment, use Docker Compose:

1. **Start the Services:**
```docker-compose up --build```

2. **Access the Application:**
API: ```http://localhost:8080/api```
Swagger UI: ```http://localhost:8080/swagger-ui/index.html```

### **API Documentation**

The API documentation is available through Swagger UI at:
```http://localhost:8080/swagger-ui/index.html```

**Endpoints Overview**

Student Endpoints

GET /api/students - Search and filter students.

POST /api/students - Add a new student.

GET /api/students/{id} - Get details of a specific student.

PUT /api/students/{id} - Update a student's details.

DELETE /api/students/{id} - Remove a student.

POST /api/students/sms/all - Send SMS notifications to all students.

Student Grades Endpoints

POST /api/students/{studentId}/grades - Add a grade for a student.

PUT /api/students/{studentId}/grades/{id} - Update a student's grade.

DELETE /api/students/{studentId}/grades/{id} - Remove a student's grade.

Security Configuration

This project uses JWT (JSON Web Token) for securing API endpoints.

Key Security Details

Authentication: Use the /authenticate endpoint to log in and receive a JWT. Include this token in the Authorization header as Bearer <token> to access protected endpoints.

Password Encryption: Passwords are encrypted using BCryptPasswordEncoder.

Configuration: Set up the JWT secret and expiration in application.properties.

Accessible Endpoints

The /authenticate, /user, and Swagger-related endpoints are publicly accessible without authentication. Most other endpoints require a valid JWT.

Development Notes

Key Files

StudentsController.java - Handles student-related operations.

StudentsGradesController.java - Handles grade-related operations for students.

Custom Services

AWSService: Manages file uploads to an S3 bucket.

SmsService: Sends SMS messages to students.

Contributing

Feel free to fork the repository and submit pull requests. Ensure all contributions adhere to the project's coding standards.

License

This project is licensed under the MIT License.
