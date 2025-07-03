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
