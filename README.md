# 🛒 E-Commerce Product Management REST API

A backend E-Commerce application developed using **Java 21** and **Spring Boot 4.1.1**. It provides RESTful APIs for creating, retrieving, updating, deleting, and searching products, as well as uploading and retrieving product images.

The application follows a layered architecture using Spring Boot, Spring Data JPA, Hibernate, and PostgreSQL.

## 🚀 Technologies Used

| Technology | Purpose |
|---|---|
| Java 21 | Backend programming language |
| Spring Boot 4.1.1 | Backend application framework |
| Spring Web MVC | REST API development |
| Spring Data JPA | Database operations |
| Hibernate | ORM and entity management |
| PostgreSQL | Relational database |
| Maven | Dependency management |
| Lombok | Reduces boilerplate code |
| Postman | API testing |

## ✨ Features

- **Product CRUD:** Create, retrieve, update, and delete products.
- **Product image upload:** Upload product images using `MultipartFile`.
- **Product image retrieval:** Retrieve an image using the product ID.
- **Product search:** Search products using keywords.
- **Case-insensitive search:** Search across product name, description, brand, and category.
- **PostgreSQL integration:** Persist product information in a PostgreSQL database.
- **JPA and Hibernate:** Simplify database operations and entity management.
- **Layered architecture:** Separate Controller, Service, Repository, and Model layers.

## 📁 Project Structure

```text
ecom-project/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/springboot/ecom_project/
│   │   │       ├── controller/
│   │   │       │   └── ProductController.java
│   │   │       ├── model/
│   │   │       │   └── Product.java
│   │   │       ├── repo/
│   │   │       │   └── ProductRepo.java
│   │   │       ├── service/
│   │   │       │   └── ProductService.java
│   │   │       └── EcomProjectApplication.java
│   │   └── resources/
│   │       ├── static/
│   │       ├── templates/
│   │       └── application.properties
│   └── test/
├── .gitignore
├── HELP.md
├── mvnw
├── mvnw.cmd
└── pom.xml
```

## 🏗️ Application Architecture

The application uses a layered architecture to separate responsibilities and improve maintainability.

```text
             Client (Postman)
                    |
                    v
           ProductController
                    |
                    v
             ProductService
                    |
                    v
              ProductRepo
                    |
                    v
                Hibernate
                    |
                    v
              PostgreSQL
```

### Layers Explained

1. **Controller Layer – `ProductController`**
   - Handles incoming HTTP requests.
   - Defines REST API endpoints.
   - Returns API responses.
   - Handles product image upload and retrieval.

2. **Service Layer – `ProductService`**
   - Contains product-related business logic.
   - Handles CRUD operations.
   - Processes uploaded image files.
   - Communicates with the repository layer.

3. **Repository Layer – `ProductRepo`**
   - Extends `JpaRepository`.
   - Uses built-in database operations.
   - Defines a custom JPQL query for product searching.

4. **Model Layer – `Product`**
   - Represents the Product entity.
   - Maps product attributes to database columns.
   - Stores product image metadata and binary image data.

## 📦 Product Entity

| Field | Data Type | Description |
|---|---|---|
| `id` | Integer | Auto-generated product ID |
| `name` | String | Product name |
| `description` | String | Product description |
| `brand` | String | Product brand |
| `price` | BigDecimal | Product price |
| `category` | String | Product category |
| `productAvailable` | Boolean | Product availability |
| `releaseDate` | Date | Product release date |
| `stockQuantity` | Integer | Available stock quantity |
| `imageName` | String | Uploaded image filename |
| `imageType` | String | Image content type |
| `imageData` | byte[] | Binary image data |

## 🔗 REST API Endpoints

**Base URL:** `http://localhost:8080/api`

### Welcome API

| Method | Endpoint | Description |
|---|---|---|
| GET | `/` | Returns a welcome message |

### Product CRUD APIs

| Method | Endpoint | Description |
|---|---|---|
| GET | `/products` | Retrieve all products |
| GET | `/product/{prodId}` | Retrieve a product by ID |
| POST | `/product` | Add a new product |
| PUT | `/product/{prodId}` | Update an existing product |
| DELETE | `/product/{prodId}` | Delete a product by ID |

### Product Image API

| Method | Endpoint | Description |
|---|---|---|
| GET | `/product/{prodId}/image` | Retrieve a product image |

### Product Search API

| Method | Endpoint | Description |
|---|---|---|
| GET | `/products/search?keyword=value` | Search products by keyword |

## 🧪 API Request Examples

You can test the APIs using Postman.

### 1. Get All Products

```http
GET http://localhost:8080/api/products
```

Returns a list of all products.

### 2. Get Product By ID

```http
GET http://localhost:8080/api/product/1
```

Returns the product details for the specified ID.

### 3. Add a New Product

```http
POST http://localhost:8080/api/product
Content-Type: multipart/form-data
```

Request body (form-data):

| Key | Type | Value |
|---|---|---|
| `product` | Text | Product JSON |
| `imageFile` | File | Product image |

Example JSON for the `product` part:

```json
{
  "name": "iPhone 16",
  "description": "Apple smartphone",
  "brand": "Apple",
  "price": 79999.00,
  "category": "Electronics",
  "productAvailable": true,
  "releaseDate": "2025-01-15T00:00:00.000+00:00",
  "stockQuantity": 10
}
```

In Postman, set the `product` part's content type to `application/json` and select the image file for `imageFile`.

### 4. Update Product

```http
PUT http://localhost:8080/api/product/1
Content-Type: multipart/form-data
```

Request parts:

- `product` – Updated product details in JSON format.
- `imageFile` – Updated product image.

### 5. Delete Product

```http
DELETE http://localhost:8080/api/product/1
```

Deletes the product associated with the specified ID.

### 6. Search Products

```http
GET http://localhost:8080/api/products/search?keyword=Apple
```

Searches products by keyword. The search is case-insensitive and checks:

- Product name
- Product description
- Product brand
- Product category

### 7. Retrieve Product Image

```http
GET http://localhost:8080/api/product/1/image
```

Returns the image associated with the specified product ID.

## ⚙️ Installation and Setup

### Prerequisites

Make sure you have installed:

- Java JDK 21
- Maven (or use the included Maven wrapper)
- PostgreSQL
- Postman (optional, for API testing)

### Step 1: Clone the Repository

Replace the placeholder URL with your actual GitHub repository URL.

```bash
git clone https://github.com/your-username/ecom-project.git
```

### Step 2: Navigate to the Project Directory

```bash
cd ecom-project
```

### Step 3: Create the PostgreSQL Database

Connect to PostgreSQL and execute:

```sql
CREATE DATABASE projectDB;
```

### Step 4: Configure the Database Connection

Open `src/main/resources/application.properties` and configure:

```properties
spring.application.name=ecom-project

spring.datasource.url=jdbc:postgresql://localhost:5432/projectDB
spring.datasource.username=${DB_USERNAME}
spring.datasource.password=${DB_PASSWORD}
spring.datasource.driver-class-name=org.postgresql.Driver

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
spring.jpa.database-platform=org.hibernate.dialect.PostgreSQLDialect
```

Set the following environment variables with your PostgreSQL credentials:

```text
DB_USERNAME=postgres
DB_PASSWORD=your_database_password
```

**Security note:** Never commit actual database passwords or credentials to GitHub.

### Step 5: Build the Project

Using Maven:

```bash
mvn clean install
```

Or, on Windows, use the Maven wrapper:

```bash
mvnw.cmd clean install
```

### Step 6: Run the Application

Using Maven:

```bash
mvn spring-boot:run
```

Or, on Windows:

```bash
mvnw.cmd spring-boot:run
```

### Step 7: Access the Application

Once the application starts successfully, open:

```text
http://localhost:8080/api/
```

Expected response:

```text
Welcome to Home Page
```

## 🔍 Product Search Implementation

The project uses a custom JPQL query in `ProductRepo.java` to perform case-insensitive searches across multiple product attributes.

```java
@Query("SELECT p FROM Product p WHERE " +
"LOWER(p.name) LIKE LOWER(CONCAT('%',:keyword,'%')) OR " +
"LOWER(p.description) LIKE LOWER(CONCAT('%',:keyword,'%')) OR " +
"LOWER(p.brand) LIKE LOWER(CONCAT('%',:keyword,'%')) OR " +
"LOWER(p.category) LIKE LOWER(CONCAT('%',:keyword,'%'))")
List<Product> searchProducts(@Param("keyword") String keyword);
```

This query allows users to find products by matching a keyword against the product name, description, brand, or category, regardless of letter case.

## 🖼️ Image Handling

Product images are uploaded using Spring's `MultipartFile`.

The application stores:

- Image filename
- Image content type
- Image binary data

The image binary data is stored in the database using the JPA `@Lob` annotation. Images can be retrieved using the product ID through the image retrieval endpoint.

## 🔮 Future Enhancements

Potential improvements for future versions include:

- User registration and authentication.
- Spring Security integration.
- Shopping cart management.
- Order management.
- Payment gateway integration.
- Product categories and advanced filtering.
- Pagination and sorting.
- Input validation and centralized exception handling.
- Frontend integration using React or Angular.

---

**Project focus:** Backend development using Java, Spring Boot, REST APIs, Spring Data JPA, Hibernate, and PostgreSQL.
