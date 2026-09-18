### MANUAL LABORATORIO1



#### Primer problema detectado, no me dejaba hacer Git : Clone en VS, he instalado una extensión de Git(Git Extension). 
### 1. Paso
#### Instalar el Managment Studio 22, una vez instalado e iniciado el servidor en localhost, tiro el primer script de la tardea para crear la bbdd:
CREATE DATABASE EcommerceDB;
 GO

 USE EcommerceDB;
 GO

### 2. Paso
#### Tirar el script de la creación de tablas. El use EcommerceDB sirve para trabajar sobre esa bbdd.####Script de creacion de tablas:   USE EcommerceDB;
 GO

 -- Create Supplier table
 CREATE TABLE Supplier (
     SupplierID INT PRIMARY KEY IDENTITY(1,1),
     SupplierName NVARCHAR(100) NOT NULL UNIQUE,
     Country NVARCHAR(50) NOT NULL,
     Email NVARCHAR(100),
     Phone NVARCHAR(20),
     CreatedDate DATETIME2 DEFAULT GETUTCDATE()
 );

 -- Create Category table
 CREATE TABLE Category (
     CategoryID INT PRIMARY KEY IDENTITY(1,1),
     CategoryName NVARCHAR(100) NOT NULL UNIQUE,
     Description NVARCHAR(500)
 );

 -- Create Product table with constraints
 CREATE TABLE Product (
     ProductID INT PRIMARY KEY IDENTITY(1,1),
     ProductName NVARCHAR(100) NOT NULL,
     CategoryID INT NOT NULL,
     SupplierID INT NOT NULL,
     BasePrice DECIMAL(10,2) NOT NULL,
     StockQuantity INT NOT NULL DEFAULT 0,
     CreatedDate DATETIME2 DEFAULT GETUTCDATE(),
     CHECK (BasePrice > 0),
     CHECK (StockQuantity >= 0),
     FOREIGN KEY (CategoryID) REFERENCES Category(CategoryID),
     FOREIGN KEY (SupplierID) REFERENCES Supplier(SupplierID),
 );

 -- Create indexes
 CREATE INDEX IX_Category ON Product(CategoryID);
 CREATE INDEX IX_Supplier ON Product(SupplierID);

 GO

