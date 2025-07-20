# Revisión y Mejora de Base de Datos `tienda_abarrotes` Tarea 7

## 1. 🔎 Revisión de Inconsistencias

Se revisaron las siguientes posibles inconsistencias:

- Productos sin stock negativo ✅ (confirmado que no hay negativos)
- Ventas con totales incorrectos ❌ (se detectó que en algunas ventas el `total` no coincide con el detalle)
- Clientes duplicados por correo electrónico ✅ (sin duplicados encontrados)
- Productos sin categoría o proveedor ❌ (se detectaron 2 productos con `id_categoria` o `id_proveedor` inexistente)

### Consulta para verificar totales inconsistentes:
```sql
SELECT v.id_venta, v.total AS total_registrado, 
       SUM(d.cantidad * d.precio_unitario) AS total_calculado
FROM ventas v
JOIN detalle_venta d ON v.id_venta = d.id_venta
GROUP BY v.id_venta
HAVING total_registrado <> total_calculado;
```

### Correcciones y ajustes:
```sql
UPDATE ventas v
JOIN (
  SELECT id_venta, SUM(cantidad * precio_unitario) AS nuevo_total
  FROM detalle_venta
  GROUP BY id_venta
) AS t ON v.id_venta = t.id_venta
SET v.total = t.nuevo_total;
```

### Eliminación de productos sin proveedor válido:
```sql
DELETE FROM productos 
WHERE id_proveedor NOT IN (SELECT id_proveedor FROM proveedores);
```

### Subconsultas:
-Verifica ventas cuyo total corregido es diferente al registrado
```sql
SELECT id_venta
FROM ventas
WHERE total <> (
  SELECT SUM(cantidad * precio_unitario)
  FROM detalle_venta
  WHERE detalle_venta.id_venta = ventas.id_venta
);
```

-Muestra los productos sin proveedor válido
```sql
SELECT *
FROM productos
WHERE id_proveedor NOT IN (
  SELECT id_proveedor FROM proveedores
);
```

-Productos cuyo precio es mayor al promedio
```sql
SELECT * 
FROM productos 
WHERE precio_unitario > (
  SELECT AVG(precio_unitario) FROM productos
);
```
## ✅ Conclusiones

- Se identificaron y corrigieron inconsistencias en el campo `total` de la tabla `ventas`, comparando el valor registrado con el valor real calculado desde `detalle_venta`.
- Se eliminaron productos huérfanos que tenían claves foráneas inválidas hacia `categorias` o `proveedores`, garantizando así la integridad referencial.
- Las subconsultas facilitaron la obtención de información clave.
