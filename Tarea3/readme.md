# Modelo Relacional - Tarea 3

```mermaid
erDiagram
    PRODUCTO ||--o{ CATEGORIAS : pertenece
    PRODUCTO }o--|| PROVEEDOR : abastece
    VENTAS ||--o{ DETALLE_VENTAS : contiene
    CLIENTES ||--o{ VENTAS : realiza
    EMPLEADOS ||--o{ VENTAS : atiende
    DETALLE_VENTAS }o--|| PRODUCTO : incluye

    PRODUCTO {
        int id_producto PK
        string nombre
        string descripcion
        decimal precio_unitario
        int stock
    }

    CATEGORIAS {
        int id_categoria PK
        string nombre_categoria
    }

    PROVEEDOR {
        int id_proveedor PK
        string nombre_proveedor
        string telefono
        string direccion
    }

    CLIENTES {
        int id_cliente PK
        string nombre
        string telefono
        string email
    }

    EMPLEADOS {
        int id_empleado PK
        string nombre_empleado
        string puesto
        date fecha_contratacion
    }

    VENTAS {
        int id_venta PK
        date fecha_venta
        decimal total
    }

    DETALLE_VENTAS {
        int id_detalle PK
        int cantidad
        decimal precio_unitario
    }
```

## Operaciones del Álgebra Relacional

| **Operación**                 | **Explicación**                                                                                              | **Expresión**                                                                 |
|-------------------------------|--------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------|
| *1. Selección compuesta*        | Selecciona productos con precio entre 50 y 150, y con stock mayor a 10.                                      | `σ_precio_unitario ≥ 50 ∧ precio_unitario ≤ 150 ∧ stock > 10(PRODUCTO)`      |
| *2. Proyección sobre JOIN*      | Muestra solo el nombre del cliente y fecha de venta al combinar `CLIENTES` y `VENTAS`.                      | `π_nombre, fecha_venta(CLIENTES ⨝ VENTAS)`                                    |
| *3. Join con condición*         | Une productos y detalles de venta cuando el precio actual del producto es mayor al precio vendido.          | `σ PRODUCTO.precio_unitario > DETALLE_VENTAS.precio_unitario(PRODUCTO ⨝ DETALLE_VENTAS)` |
| *4. Renombramiento + selección* | Renombra la tabla `VENTAS` y selecciona ventas hechas por el empleado con ID 3.                             | `ρ ventas_renombradas(VENTAS)`<br>`σ ventas_renombradas.id_empleado = 3(ventas_renombradas)` |
