# Generación de Datos Ficticios con Mockaroo - Tarea 5 🧪

Este documento resume los hallazgos, dificultades, recomendaciones y recursos relevantes tras utilizar la herramienta [Mockaroo](https://mockaroo.com/) para agregar datos ficticios a la base de datos del proyecto `tienda_abarrotes`.

---

## ✅ Hallazgos

- **Mockaroo** permite generar datos ficticios de manera personalizada y en diferentes formatos (`CSV`, `SQL`, `JSON`, etc.).
- Es posible definir los nombres de los campos, tipos de datos específicos (nombre, correo, teléfono, fecha, etc.) e incluso relaciones entre ellos.
- Los esquemas generados pueden guardarse para futuras ediciones o exportarse directamente como scripts `INSERT` en SQL, lo que facilita la carga automática de información a la base de datos.

---

## ⚠️ Dificultades encontradas

- Los tipos de datos generados a veces **no coinciden con los tipos definidos en la base**, lo que puede causar errores al ejecutar los scripts SQL (ejemplo: `VARCHAR(20)` vs cadenas de 30+ caracteres).
- Si los nombres de los campos no se configuran exactamente como en las tablas reales, hay que **modificar manualmente los nombres en el script SQL**.
- La **versión gratuita de Mockaroo** limita la descarga a **1000 registros por archivo**, lo cual puede ser restrictivo en bases más grandes.

---

## 💡 Recomendaciones

- Utilizar el tipo de campo `Custom List` o `Formula` para valores que deben seguir un patrón específico (por ejemplo: puestos, tipos de producto, zonas geográficas).
- Exportar los archivos como `.SQL` y **validarlos previamente en un editor** de texto o consola SQL para evitar errores.
- Asegurarse de que los `id`s generados **no se dupliquen** con los registros ya existentes en la base de datos.

---

## 🔗 Recursos relevantes

- 🌐 Sitio oficial: [https://mockaroo.com](https://mockaroo.com)
- 📚 Documentación de tipos de datos: [https://mockaroo.com/schemas](https://mockaroo.com/schemas)

## 📦 Datos generados

### 🗂️ Tablas

```sql
### 🗂️ Tabla `Categorias`
INSERT INTO categorias (id_categoria, nombre_categoria) VALUES (1, 'Food - Beverages');
INSERT INTO categorias (id_categoria, nombre_categoria) VALUES (2, 'Food - Prepared Meals');
INSERT INTO categorias (id_categoria, nombre_categoria) VALUES (3, 'Pets');
INSERT INTO categorias (id_categoria, nombre_categoria) VALUES (4, 'Food - Snacks');
INSERT INTO categorias (id_categoria, nombre_categoria) VALUES (5, 'Food - Bakery');
INSERT INTO categorias (id_categoria, nombre_categoria) VALUES (6, 'Toys');
INSERT INTO categorias (id_categoria, nombre_categoria) VALUES (7, 'Accessories');
INSERT INTO categorias (id_categoria, nombre_categoria) VALUES (8, 'Food - Snacks');
INSERT INTO categorias (id_categoria, nombre_categoria) VALUES (9, 'Outdoor');
INSERT INTO categorias (id_categoria, nombre_categoria) VALUES (10, 'Kitchen');

### 🗂️ Tabla `Proveedores`

INSERT INTO proveedores (id_proveedor, nombre_proveedor, direccion, telefono) VALUES (1, 'Quaxo', '6 Superior Way', '741-242-7932');
INSERT INTO proveedores (id_proveedor, nombre_proveedor, direccion, telefono) VALUES (2, 'Eadel', '5858 John Wall Road', '598-382-5700');
...
INSERT INTO proveedores (id_proveedor, nombre_proveedor, direccion, telefono) VALUES (20, 'JumpXS', '27 Moland Plaza', '896-820-2726');
-Se generó 20 proveedores ficticios

### 🗂️ Tabla `Productos`
INSERT INTO productos (id_producto, nombre, descripcion, precio_unitario, stock, id_categoria, id_proveedor) VALUES
(1, 'Electric Wine Opener', 'Rechargeable electric wine opener for effortless uncorking.', 29.99, 100, 1, 1),
(2, 'Hiking Water Bottle with Filter', '8oz water bottle with built-in filter for clean drinking water.', 29.99, 100, 2, 2),
...
(50, 'Almond Joy Bars', 'Chocolate-covered candy bars with coconut and almonds.', 1.29, 100, 50, 50);
-Se generó 50 registrso de productos ficticios




