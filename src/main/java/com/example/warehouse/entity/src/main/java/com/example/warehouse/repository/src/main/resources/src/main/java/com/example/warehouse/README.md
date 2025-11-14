# Warehouse Management System - Spring Boot

## Overview
A Spring Boot 3 application for managing warehouse operations with CRUD operations for Items, Warehouses, Stocks, Movements, and Suppliers.

## Project Structure
```
warehouse-demo/
├── pom.xml
├── src/main/java/com/example/warehouse/
│   ├── WarehouseApplication.java (Main Entry Point)
│   ├── entity/
│   │   ├── Item.java
│   │   ├── Warehouse.java
│   │   ├── Stock.java
│   │   ├── Movement.java
│   │   └── Supplier.java
│   ├── repository/
│   │   └── WarehouseRepository.java (+ others)
│   └── controller/
│       └── (CRUD Controllers for all entities)
└── src/main/resources/
    └── application.properties
```

## Entities

### Item
- **id**: Long (Auto-generated Primary Key)
- **name**: String (Product name)
- **sku**: String (Stock Keeping Unit)

### Warehouse
- **id**: Long (Auto-generated Primary Key)
- **name**: String (Warehouse name)
- **location**: String (Physical location)

### Stock
- **id**: Long (Auto-generated Primary Key)
- **item**: Many-to-One relationship with Item
- **warehouse**: Many-to-One relationship with Warehouse
- **quantity**: int (Current stock quantity)

### Movement
- **id**: Long (Auto-generated Primary Key)
- **item**: Many-to-One relationship with Item
- **fromWarehouse**: Nullable Many-to-One (null = incoming stock)
- **toWarehouse**: Many-to-One relationship with Warehouse
- **quantity**: int (Quantity moved)
- **timestamp**: LocalDateTime (Movement time)

### Supplier
- **id**: Long (Auto-generated Primary Key)
- **name**: String (Supplier name)
- **contactInfo**: String (Contact information)

## Key Features

1. **CRUD Operations**: Create, Read, Update, Delete for all entities
2. **Stock Consistency**: Automatic validation that stock doesn't go negative
3. **Movement Tracking**: Record all stock movements between warehouses
4. **Transactional Integrity**: Database transactions ensure data consistency
5. **H2 In-Memory Database**: Default configuration for easy testing

## Running the Application

### Prerequisites
- Java 17+
- Maven 3.8+

### Build and Run
```bash
# Clone the repository
git clone https://github.com/Clocker34/warehouse-demo.git
cd warehouse-demo

# Build with Maven
./mvnw clean package

# Run the application
./mvnw spring-boot:run
```

The application will start on `http://localhost:8080`

## API Endpoints (Future Implementation)

### Items
- `POST /items` - Create new item
- `GET /items/{id}` - Get item by ID
- `GET /items` - Get all items
- `PUT /items/{id}` - Update item
- `DELETE /items/{id}` - Delete item

### Warehouses
- `POST /warehouses` - Create new warehouse
- `GET /warehouses/{id}` - Get warehouse by ID
- `PUT /warehouses/{id}` - Update warehouse
- `DELETE /warehouses/{id}` - Delete warehouse

### Stock Management
- `POST /stocks` - Add stock
- `GET /stocks/{id}` - Get stock by ID
- `PUT /stocks/{id}` - Update stock
- `DELETE /stocks/{id}` - Delete stock

### Movements
- `POST /movements` - Create movement (Move stock between warehouses)
- `GET /movements/{id}` - Get movement history

### Suppliers
- `POST /suppliers` - Add supplier
- `GET /suppliers/{id}` - Get supplier
- `PUT /suppliers/{id}` - Update supplier
- `DELETE /suppliers/{id}` - Delete supplier

## Business Logic

### Stock Consistency Rules
- When creating a movement, the system validates:
  1. Source warehouse has sufficient stock
  2. Source quantity is positive
  3. Stock cannot go below zero
- Operations are transactional to ensure atomicity

### Future Enhancements
- REST API for all CRUD operations
- Movement history queries
- Stock level analytics
- Low stock alerts
- Supplier integration with purchase orders
- Multi-level warehouse hierarchies

## Technologies Used
- **Spring Boot 3.2.0**
- **Spring Data JPA**
- **H2 Database** (Configurable to PostgreSQL, MySQL)
- **Lombok** (For reducing boilerplate)
- **Maven**

## Database Configuration

Default: H2 In-Memory

To use PostgreSQL or MySQL, modify `application.properties`:

```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/warehouse
spring.datasource.driver-class-name=org.postgresql.Driver
spring.datasource.username=postgres
spring.datasource.password=yourpassword
spring.jpa.database-platform=org.hibernate.dialect.PostgreSQLDialect
```

## Development Notes
- All entities use Lombok annotations (@Data, @Entity, @NoArgsConstructor, @AllArgsConstructor)
- Repositories extend JpaRepository for CRUD operations
- Entities use @ManyToOne relationships with @JoinColumn
- Movement tracking includes nullable fromWarehouse for incoming stock

## Author
Created as a warehouse management system demonstration for educational purposes.

## License
MIT License
