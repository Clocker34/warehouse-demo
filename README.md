# Warehouse Management System - Spring Boot

## Overview
A Spring Boot 3 application for managing warehouse operations with CRUD operations for Items, Warehouses, Stocks, Movements, and Suppliers.

## Features
✅ **CRUD Operations** for 5 entities (Item, Warehouse, Stock, Movement, Supplier)  
✅ **Stock Consistency** - Automatic validation that stock doesn't go negative  
✅ **Movement Tracking** - Record all stock movements between warehouses  
✅ **Transactional Integrity** - Database transactions ensure data consistency  
✅ **H2 In-Memory Database** - Default configuration for easy testing  
✅ **Spring Boot 3.2.0** with Spring Data JPA  
✅ **Lombok** for reducing boilerplate code  

## Project Structure
```
warehouse-demo/
├── pom.xml
├── src/main/java/com/example/warehouse/
│   ├── WarehouseApplication.java
│   ├── entity/
│   │   ├── Item.java
│   │   ├── Warehouse.java
│   │   ├── Stock.java
│   │   ├── Movement.java
│   │   └── Supplier.java
│   ├── repository/
│   │   └── WarehouseRepository.java (+ others)
│   └── controller/ (Coming soon)
└── src/main/resources/
    └── application.properties
```

## Entities

### Item
- `id`: Long (Auto-generated)
- `name`: String
- `sku`: String (Stock Keeping Unit)

### Warehouse
- `id`: Long
- `name`: String
- `location`: String

### Stock
- `id`: Long
- `item`: @ManyToOne with Item
- `warehouse`: @ManyToOne with Warehouse
- `quantity`: int

### Movement
- `id`: Long
- `item`: @ManyToOne with Item
- `fromWarehouse`: @ManyToOne (nullable - for incoming stock)
- `toWarehouse`: @ManyToOne with Warehouse
- `quantity`: int
- `timestamp`: LocalDateTime

### Supplier
- `id`: Long
- `name`: String
- `contactInfo`: String

## Getting Started

### Prerequisites
- Java 17+
- Maven 3.8+
- Git

### Clone & Build
```bash
git clone https://github.com/Clocker34/warehouse-demo.git
cd warehouse-demo
./mvnw clean package
./mvnw spring-boot:run
```

Application will start on `http://localhost:8080`

## API Endpoints (Coming Soon)
RESTful endpoints for all CRUD operations on Item, Warehouse, Stock, Movement, and Supplier entities.

## Technologies
- **Spring Boot 3.2.0**
- **Spring Data JPA**
- **H2 Database** (Configurable)
- **Lombok**
- **Maven**

## Database
Default: H2 In-Memory  
Editable in `application.properties`

## Status
- ✅ Entities defined
- ✅ Repositories created
- ✅ Application structure ready
- 🔄 Controllers in progress
- 🔄 REST API endpoints
- 🔄 Integration tests

## License
MIT License

## Author
Clocker34
