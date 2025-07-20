# Funciones de Agregación - Tarea 6

Este documento contiene ejemplos de consultas SQL aplicadas sobre la base de datos `tienda_abarrotes`, para el análisis de datos mediante funciones de agregación.

---

## 📊 1. Funciones de Agregación

### 🔸 Data
```sql
#Media del precio de los productos
SELECT AVG(precio_unitario) AS media_precio 
FROM productos;

#Conteo de ventas por cliente
SELECT id_cliente, COUNT(*) AS total_ventas 
FROM ventas 
GROUP BY id_cliente;

#Mínimos y máximos
SELECT MIN(precio_unitario) AS precio_minimo, 
       MAX(precio_unitario) AS precio_maximo 
FROM productos;

#Cuantil
SELECT precio_unitario
FROM (
  SELECT precio_unitario, 
         NTILE(4) OVER (ORDER BY precio_unitario) AS cuartil
  FROM productos
) AS sub
WHERE cuartil = 4;

#Moda
SELECT id_producto, COUNT(*) AS veces_vendido
FROM detalle_venta
GROUP BY id_producto
ORDER BY veces_vendido DESC
LIMIT 1;

## 📝 Reporte

### 🔍 Hallazgos

- El precio promedio de los productos en el inventario es representativo del mercado minorista.
- La mayoría de los productos más caros se concentran en el cuartil superior (Q4), donde el precio es mayor a la media.
- El producto más vendido es el que aparece más veces en la tabla `detalle_venta` es la coca-cola, lo cual podría usarse para promociones o gestión de inventario.

---

### ⚠️ Dificultades

- En MySQL 5.x no existen funciones estadísticas avanzadas como `PERCENTILE_CONT`, por lo que fue necesario simular el cuartil usando `NTILE()`.
- La moda se obtuvo de manera manual agrupando y ordenando por frecuencia.

---

### ✅ Soluciones

- Se usó la función `NTILE(4)` para dividir los precios en cuartiles y seleccionar el superior.
- Para calcular la moda se utilizó `GROUP BY` junto con `ORDER BY COUNT(*) DESC`.



