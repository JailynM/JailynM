CREATE DATABASE TiendaManolito;
USE TiendaManolito;


CREATE TABLE Clientes (
    ClienteID INT PRIMARY KEY IDENTITY(1,1),
    Nombre NVARCHAR(100) NOT NULL,
    Cedula NVARCHAR(20) NOT NULL
);


CREATE TABLE Productos (
    ProductoID INT PRIMARY KEY IDENTITY(1,1),
    Nombre NVARCHAR(100) NOT NULL,
    Categoria NVARCHAR(50) NOT NULL,
    FechaSalida DATE NOT NULL,
    Precio DECIMAL(10, 2) NOT NULL
);


CREATE TABLE Proveedores (
    ProveedorID INT PRIMARY KEY IDENTITY(1,1),
    Nombre NVARCHAR(50) NOT NULL
);


INSERT INTO Proveedores (Nombre) VALUES ('Apple'), ('Samsung');
INSERT INTO Proveedores (Nombre) Values ('Xiaomi');

CREATE TABLE Ventas (
    VentaID INT PRIMARY KEY IDENTITY(1,1),
    ClienteID INT FOREIGN KEY REFERENCES Clientes(ClienteID),
    ProductoID INT FOREIGN KEY REFERENCES Productos(ProductoID),
    ProveedorID INT FOREIGN KEY REFERENCES Proveedores(ProveedorID),
    MontoPagado DECIMAL(10, 2) NOT NULL,
    FechaCompra DATE NOT NULL,
    GarantiaExpiracion DATE NOT NULL
);

INSERT INTO Clientes (Nombre, Cedula) VALUES
('Juan Perez', '1234567890'),
('Maria Rodriguez', '0987654321');

INSERT INTO Productos (Nombre, Categoria, FechaSalida, Precio) VALUES
('iPhone 15', 'Smartphone', '2023-09-22', 1200.00),
('Galaxy S20', 'Smartphone', '2023-09-22', 1000.00);

INSERT INTO Productos (Nombre, Categoria, FechaSalida, Precio) VALUES
('Xiaomi', 'Smartphone', '2023-08-20', 900.00);

INSERT INTO Ventas (ClienteID, ProductoID, ProveedorID, MontoPagado, FechaCompra, GarantiaExpiracion) VALUES
(1, 1, 1, 1200.00, '2023-09-22', '2023-09-22'),
(2, 2, 2, 1000.00, '2023-09-23', '2023-09-23');

SELECT 
    V.VentaID,
    C.Nombre AS Cliente,
    P.Nombre AS Producto,
    PR.Nombre AS Proveedor,
    V.MontoPagado,
    V.FechaCompra
FROM Ventas V
JOIN Clientes C ON V.ClienteID = C.ClienteID
JOIN Productos P ON V.ProductoID = P.ProductoID
JOIN Proveedores PR ON V.ProveedorID = PR.ProveedorID
ORDER BY V.FechaCompra ASC;

SELECT 
    Nombre,
    Categoria,
    FechaSalida,
    Precio
FROM Productos


SELECT 
    Nombre
FROM Proveedores;


SELECT 
    Nombre
	Cedula
FROM Clientes;      
