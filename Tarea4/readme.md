# Creación base de datos - Tarea 4

-- Creación base de datos

create database tienda_abarrotes;
use tienda_abarrotes;

-- Creación de tablas 

-- Tabla de Categorías
create table categorias(
	id_categoria INT primary key,
	nombre_categoria VARCHAR(100)
);

-- Tabla de Proveedores
create table proveedores(
	id_proveedor INT primary key,
	nombre_proveedor VARCHAR(100),
	telefono VARCHAR(20),
	direccion VARCHAR(255)
);

-- Tabla de Productos
create table productos(
	id_producto INT primary key,
	nombre VARCHAR(100),
	descripcion TEXT,
	precio_unitario DECIMAL(10,2),
	stock INT,
	id_categoria INT,
	id_proveedor INT,
	foreign key (id_categoria) references categorias(id_categoria),
	foreign key (id_proveedor) references proveedores(id_proveedor)
);

-- Tabla de Clientes
create table clientes(
	id_cliente INT primary key,
	nombre VARCHAR(100),
	telefono VARCHAR(20),
	email VARCHAR(100)
);

-- Tabla de Ventas
create table ventas(
	id_venta INT primary key,
	fecha_venta DATE,
	id_cliente INT,
	total DECIMAL(10,2),
	foreign key (id_cliente) references clientes(id_cliente)
);

-- Tabla de Detalle_Venta
create table detalle_venta(
	id_detalle INT primary key,
	id_venta INT,
	id_producto INT,
	cantidad INT,
	precio_unitario DECIMAL(10,2),
	foreign key (id_venta) references ventas(id_venta),
	foreign key (id_producto) references productos(id_producto)
);

-- Tabla de Empleados
create table empleados(
	id_empleado INT primary key,
	nombre_empleado VARCHAR(100),
	puesto VARCHAR(100),
	fecha_contratacion DATE
);

-- Insertamos información

insert into categorias values
(1, 'Bebidas'),
(2, 'Lácteos'),
(3, 'Snacks'),
(4, 'Abarrotes'),
(5, 'Dulces');

insert into proveedores values
(1, 'Distribuidora Norte', '8112345678', 'Av. Principal 123, Monterrey'),
(2, 'Alimentos del Sur', '8123456789', 'Calle Central 45, Monterrey'),
(3, 'Súper Centro Distribuidor', '8187654321', 'Carretera Nacional 789, Monterrey'),
(4, 'Proveedora Express', '8133344556', 'Av. Revolución 321, Monterrey'),
(5, 'Surtidora del Norte', '8111112222', 'Colonia Centro 234, Monterrey');

insert into productos values
(101, 'Coca-Cola 600ml', 'Refresco embotellado', 15.50, 120, 1, 1),
(102, 'Leche Entera 1L', 'Leche pasteurizada', 23.90, 80, 2, 2),
(103, 'Papas Sabritas', 'Papas saladas 45g', 14.00, 50, 3, 1),
(104, 'Arroz 1kg', 'Arroz extra calidad', 19.50, 200, 4, 3),
(105, 'Galletas María', 'Galletas tradicionales', 25.00, 150, 5, 4);

insert into clientes values
(201, 'Juan Pérez', '8111223344', 'juan.perez@email.com'),
(202, 'Ana López', '8122334455', 'ana.lopez@email.com'),
(203, 'Luis García', '8119988777', 'luis.garcia@email.com'),
(204, 'María Torres', '8125566778', 'maria.torres@email.com'),
(205, 'José Hernández', '8181234567', 'jose.hdz@email.com');

insert into ventas values
(301, '2025-07-01', 201, 53.40),
(302, '2025-07-02', 202, 37.90),
(303, '2025-07-03', 203, 44.40),
(304, '2025-07-03', 204, 56.70),
(305, '2025-07-04', 205, 28.90);

insert into detalle_venta values
(401, 301, 101, 2, 15.50),
(402, 301, 103, 1, 14.00),
(403, 302, 102, 1, 23.90),
(404, 302, 103, 1, 14.00),
(405, 303, 104, 2, 19.50);

insert into empleados values
(501, 'Carlos Martínez', 'Cajero', '2023-03-01'),
(502, 'Laura Gómez', 'Almacenista', '2024-08-15'),
(503, 'Marcos Ruiz', 'Repartidor', '2023-06-10'),
(504, 'Sandra Herrera', 'Cajera', '2022-09-15'),
(505, 'Eduardo Tamez', 'Encargado', '2021-01-22');

-- Validación de valores

select * from tienda_abarrotes.productos limit 3;
select * from tienda_abarrotes.ventas limit 3;
select * from tienda_abarrotes.detalle_venta limit 3;
