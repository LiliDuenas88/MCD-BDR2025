# Vistas y Disparadores Tarea 8

## 1. 🔎 Creación de Vistas (View)

### Vista con JOIN (INNER JOIN): productos con su proveedor

```sql
CREATE VIEW vista_productos_proveedor AS
SELECT p.id_producto, p.nombre, pr.nombre_proveedor, p.precio_unitario
FROM productos p
JOIN proveedores pr ON p.id_proveedor = pr.id_proveedor;
```
### Vista con LEFT JOIN: todos los productos aunque no tengan ventas

```sql
CREATE VIEW vista_productos_ventas AS
SELECT p.id_producto, p.nombre, dv.id_venta, dv.cantidad
FROM productos p
LEFT JOIN detalle_venta dv ON p.id_producto = dv.id_producto;
```

### Vista con RIGHT JOIN: ventas con detalle, incluso si el producto ya no existe (caso hipotético)

```sql
CREATE VIEW vista_detalle_completo AS
SELECT p.nombre, dv.id_venta, dv.cantidad, dv.precio_unitario
FROM productos p
RIGHT JOIN detalle_venta dv ON p.id_producto = dv.id_producto;
```

### Vista con subconsulta: productos más caros que el promedio

```sql
CREATE VIEW vista_productos_caros AS
SELECT id_producto, nombre, precio_unitario
FROM productos
WHERE precio_unitario > (
  SELECT AVG(precio_unitario) FROM productos
);
```
## 2. 🔎 Creación de un TRIGGER

```sql
DELIMITER //

CREATE TRIGGER actualizar_stock
AFTER INSERT ON detalle_venta
FOR EACH ROW
BEGIN
  UPDATE productos
  SET stock = stock - NEW.cantidad
  WHERE id_producto = NEW.id_producto;
END;
//

DELIMITER ;
```

## 📘 Vistas creadas

### `vista_productos_proveedor`
Muestra los productos con su proveedor. Se usa `INNER JOIN` para combinar ambas tablas.

### `vista_productos_ventas`
Muestra todos los productos y si tienen o no ventas (`LEFT JOIN`).

### `vista_detalle_completo`
Relaciona ventas con productos incluso si el producto no existe (caso raro). `RIGHT JOIN`.

### `vista_productos_caros`
Filtra los productos cuyo precio es mayor al promedio. Subconsulta como filtro.

---

## ⚙️ Trigger

### `actualizar_stock`
Este trigger se ejecuta **después de insertar** en `detalle_venta`. Disminuye el stock del producto vendido automáticamente, restando la cantidad comprada.

---

## ✅ Beneficios

- Las **vistas** facilitan la consulta de datos complejos con nombres amigables.
- El **trigger** automatiza tareas y mantiene integridad del inventario sin intervención manual.
