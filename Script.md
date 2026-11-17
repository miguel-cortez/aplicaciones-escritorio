# Creación de base de datos

```sql
USE master;
GO
IF DB_ID (N'Inventario') IS NOT NULL
DROP DATABASE Inventario;
GO
CREATE DATABASE Inventario;
GO
USE Inventario;
GO
IF OBJECT_ID(N'Empleados',N'U') IS NULL
CREATE TABLE Empleados(
	Id INT NOT NULL IDENTITY(1,1),
	Codigo CHAR(10) NULL,
	Nombre VARCHAR(50) NOT NULL,
	Apellido VARCHAR(50) NOT NULL,
	Telefono VARCHAR(15) NULL,
	Correo VARCHAR(150) NULL,
	CONSTRAINT EmpleadosPk PRIMARY KEY(Id)
)
GO
IF OBJECT_ID(N'Usuarios',N'U') IS NULL
CREATE TABLE Usuarios(
	Id INT NOT NULL,
	Login VARCHAR(15) NOT NULL,
	Password VARBINARY(255) NOT NULL,
	CONSTRAINT UsuariosPk PRIMARY KEY(Id),
	CONSTRAINT UsuariosFk1 FOREIGN KEY (Id) REFERENCES Empleados(Id)
)
GO
IF OBJECT_ID(N'Categorias',N'U') IS NULL
CREATE TABLE Categorias(
	Id INT NOT NULL IDENTITY(1,1),
	Codigo CHAR(10) NULL,
	Nombre VARCHAR(50) NOT NULL,
	CONSTRAINT CategoriasPk PRIMARY KEY(Id)
)
GO
IF OBJECT_ID(N'Unidades',N'U') IS NULL
CREATE TABLE Unidades(
	Id INT NOT NULL IDENTITY(1,1),
	Codigo CHAR(10) NULL,
	Nombre VARCHAR(50) NOT NULL,
	CONSTRAINT UnidadesPk PRIMARY KEY(Id)
)
GO
IF OBJECT_ID(N'Productos',N'U') IS NULL
CREATE TABLE Productos(
	Id INT NOT NULL IDENTITY(1,1),
	Codigo CHAR(10) NULL,
	Nombre VARCHAR(50) NOT NULL,
	Descripcion VARCHAR(100) NULL,
	CategoriaId INT NOT NULL,
	CONSTRAINT ProductosPk PRIMARY KEY(Id),
	CONSTRAINT ProductosFk1 FOREIGN KEY (CategoriaId) REFERENCES Categorias(Id)
)
GO
IF OBJECT_ID(N'Inventarios',N'U') IS NULL
CREATE TABLE Inventarios(
	Id INT NOT NULL IDENTITY(1,1),
	Codigo CHAR(25) NULL,
	Descripcion VARCHAR(150) NULL,
	ProductoId INT NOT NULL,
	UnidadId INT NOT NULL,
	Stock SMALLINT NOT NULL,
	Precio MONEY NOT NULL,
	CONSTRAINT InventariosPk PRIMARY KEY(Id),
	CONSTRAINT InventariosFk1 FOREIGN KEY (ProductoId) REFERENCES Productos(Id),
	CONSTRAINT InventariosFk2 FOREIGN KEY (UnidadId) REFERENCES Unidades(Id)
)
GO
IF OBJECT_ID(N'Proveedores',N'U') IS NULL
CREATE TABLE Proveedores(
	Id INT NOT NULL IDENTITY(1,1),
	Codigo CHAR(10) NULL,
	Nombre VARCHAR(50) NOT NULL,
	CONSTRAINT ProveedoresPk PRIMARY KEY(Id)
)
GO
IF OBJECT_ID(N'Compras',N'U') IS NULL
CREATE TABLE Compras(
	Id INT NOT NULL IDENTITY(1,1),
	NumeroComprobante VARCHAR(25) NULL,
	Fecha DATE NOT NULL,
	SubTotal MONEY NOT NULL,
	Iva MONEY NOT NULL,
	Total MONEY NOT NULL,
	ProveedorId INT NOT NULL,
	UsuarioId INT NOT NULL,
	CONSTRAINT ComprasPk PRIMARY KEY(Id),
	CONSTRAINT ComprasFk1 FOREIGN KEY (ProveedorId) REFERENCES Proveedores(Id),
	CONSTRAINT ComprasFk2 FOREIGN KEY (UsuarioId) REFERENCES Usuarios(Id)
)
GO
IF OBJECT_ID(N'DetalleCompras',N'U') IS NULL
CREATE TABLE DetalleCompras(
	Id INT NOT NULL IDENTITY(1,1),
	Cantidad SMALLINT NOT NULL,
	PrecioUnitario MONEY NOT NULL,
	Monto MONEY NOT NULL,
	CompraId INT NOT NULL,
	InventarioId INT NOT NULL,
	CONSTRAINT DetalleComprasPk PRIMARY KEY(Id),
	CONSTRAINT DetalleComprasFk1 FOREIGN KEY (CompraId) REFERENCES Compras(Id),
	CONSTRAINT DetalleComprasFk2 FOREIGN KEY (InventarioId) REFERENCES Inventarios(Id)
)
GO

INSERT INTO Categorias(Nombre) VALUES('Materia prima');
INSERT INTO Categorias(Nombre) VALUES('Papelería y útiles');
INSERT INTO Productos(Nombre, CategoriaId) VALUES('Varilla de hierro',1);
INSERT INTO Productos(Nombre, CategoriaId) VALUES('Grava para construcción',1);
INSERT INTO Productos(Nombre, CategoriaId) VALUES('Resma de papel bond',2);
INSERT INTO Productos(Nombre, CategoriaId) VALUES('Borrador de lápiz',2);
INSERT INTO Unidades(Codigo, Nombre) VALUES('U','Unidad');
INSERT INTO Unidades(Codigo, Nombre) VALUES('M3','Metro cúbico');
INSERT INTO Inventarios(Codigo, Descripcion, Stock, Precio, ProductoId, UnidadId) VALUES('40854521','HIERRO REDONDO CORRUGADO 3/8 PLG (9.5 MM) 6 M GRADO 40 N.º 3',60, 9.78,1,1);
INSERT INTO Inventarios(Codigo, Descripcion, Stock, Precio, ProductoId, UnidadId) VALUES('40994521','HIERRO REDONDO LISO 1/4 PLG (5.50 MM) 6 M COMERCIAL',25, 1.22,1 ,1);
INSERT INTO Inventarios(Codigo, Descripcion, Stock, Precio, ProductoId, UnidadId) VALUES('50684527','GRAVA EMBOLSADA N.º 1',17, 66.25, 2,2);
INSERT INTO Inventarios(Codigo, Descripcion, Stock, Precio, ProductoId, UnidadId) VALUES('11856325','PAPEL BOND FACELA TAMANO CART 8.5x11 , 75 GRS, 98% BLANCO',17, 7.30, 3,2);
INSERT INTO Inventarios(Codigo, Descripcion, Stock, Precio, ProductoId, UnidadId) VALUES('10504','BORRADOR PELIKAN PASTEL 2U',5, 0.7, 4,2);
INSERT INTO Empleados(Codigo, Nombre, Apellido, Telefono, Correo) VALUES('MACV', 'Miguel Ángel','Cortez Vásquez',null, 'mcortez_vasquez@yahoo.com');
INSERT INTO Usuarios(Id, Login,Password) VALUES(1,'miguel',HASHBYTES('SHA2_256','admin'));
INSERT INTO Proveedores(Codigo, Nombre) VALUES('LT156', 'Progresa')
```