#TAREA 1

# Base de Datos - Tienda de Abarrotes

Este proyecto describe una base de datos inicial para una tienda de abarrotes que atiende aproximadamente 500 personas por día. La base está pensada para un manejo sencillo pero funcional, con 7 tablas principales y sus relaciones básicas.

---

## Tablas y Atributos

### 1. Tabla `Productos`
| Atributo         | Tipo de Dato  | Descripción                  |
|------------------|---------------|------------------------------|
| `id_producto`    | entero        | Identificador único          |
| `nombre`         | texto         | Nombre del producto          |
| `descripcion`    | texto         | Descripción del producto     |
| `precio_unitario`| decimal       | Precio por unidad            |
| `stock`          | entero        | Cantidad disponible          |

### 2. Tabla `Categorías`
| Atributo          | Tipo de Dato  | Descripción                 |
|-------------------|---------------|-----------------------------|
| `id_categoria`    | entero        | Identificador único         |
| `nombre_categoria`| texto         | Nombre de la categoría      |

### 3. Tabla `Proveedores`
| Atributo         | Tipo de Dato  | Descripción                  |
|------------------|---------------|------------------------------|
| `id_proveedor`   | entero        | Identificador único          |
| `nombre_proveedor`| texto        | Nombre del proveedor         |
| `telefono`       | texto         | Teléfono de contacto         |
| `direccion`      | texto         | Dirección del proveedor      |

### 4. Tabla `Clientes`
| Atributo         | Tipo de Dato  | Descripción                  |
|------------------|---------------|------------------------------|
| `id_cliente`     | entero        | Identificador único          |
| `nombre`         | texto         | Nombre completo              |
| `telefono`       | texto         | Número de contacto           |
| `email`          | texto         | Correo electrónico           |

### 5. Tabla `Ventas`
| Atributo         | Tipo de Dato  | Descripción                  |
|------------------|---------------|------------------------------|
| `id_venta`       | entero        | Identificador único          |
| `fecha_venta`    | fecha         | Día de la venta              |
| `id_cliente`     | entero        | Referencia a Clientes        |
| `total`          | decimal       | Monto total de la venta      |

### 6. Tabla `Detalle_Venta`
| Atributo         | Tipo de Dato  | Descripción                  |
|------------------|---------------|------------------------------|
| `id_detalle`     | entero        | Identificador único          |
| `id_venta`       | entero        | Referencia a Ventas          |
| `id_producto`    | entero        | Referencia a Productos       |
| `cantidad`       | entero        | Cantidad vendida             |
| `precio_unitario`| decimal       | Precio al momento de la venta|

### 7. Tabla `Empleados`
| Atributo          | Tipo de Dato  | Descripción                  |
|-------------------|---------------|------------------------------|
| `id_empleado`     | entero        | Identificador único          |
| `nombre_empleado` | texto         | Nombre del empleado          |
| `puesto`          | texto         | Rol o puesto en la tienda    |
| `fecha_contratacion`| fecha      | Fecha en que empezó a trabajar|

---

## 🔗 Relaciones entre Tablas
- Cada **producto** pertenece a una **categoría**.
- Cada **producto** puede estar asociado a un **proveedor**.
- Una **venta** se asocia a un **cliente** (o puede quedar como genérica).
- Una **venta** incluye varios **detalles de venta** (productos y cantidades).
- Los **empleados** pueden asociarse a las ventas (posible expansión futura).

# Sistema de Gestión de Bases de Datos (SGBD)

Un sistema de gestión de bases de datos (SGBD) es un software utilizado para gestionar, almacenar y recuperar bases de datos. Proporciona una interfaz que permite a los usuarios leer, crear, borrar y actualizar datos. Los SGBD funcionan mediante comandos del sistema. Al introducir un comando, el administrador de la base de datos da instrucciones para recuperar, modificar o cargar los datos existentes.

## Ejemplos de SGBD más populares

### 1. MySQL
MySQL es un gestor de bases de datos relacionales que se basa en SQL y en la arquitectura cliente-servidor. Es uno de los SGBD más utilizados, ya que es compatible con varias plataformas informáticas, incluidas las distribuciones de Linux, Windows y macOS. MySQL también es compatible con C, C++, Java, Perl, PHP, Python y Ruby.

- Es un SGBDR (Sistema de Gestión de Bases de Datos Relacional), lo que significa que utiliza el formato tabular para organizar los datos y mantiene relaciones entre los elementos.
- De código abierto, distribuido bajo la Licencia Pública General de GNU.
- Para uso comercial, se requiere adquirir la versión con licencia.
- Desarrollado en C y C++ con un analizador sintáctico SQL basado en Yacc y un tokenizador propio.
- Destaca por su amplio soporte de sistemas operativos.

### 2. PostgreSQL
PostgreSQL es un gestor de bases de datos empresarial de código abierto que soporta SQL para consultas relacionales y JSON para consultas no relacionales.

- Permite definir tipos de datos personalizados, crear funciones y escribir código en varios lenguajes sin recompilar las bases de datos.
- Compila los datos en un formato de catálogo, utilizando tablas, columnas y metadatos sobre métodos de acceso y funciones.

### 3. Oracle
Oracle es un sistema de gestión de bases de datos utilizado principalmente por grandes empresas para gestionar grandes volúmenes de datos desde un solo archivo.

- Ofrece control de acceso avanzado y gestión segura de los datos.
- Copias de seguridad automáticas y gestión de vistas materializadas (tablas en formato de filas y columnas).
- Interfaz intuitiva y fácil de usar.

## Razones para Elegir MySQL

En mi caso, he decidido utilizar **MySQL** por las siguientes razones:

- Fue la recomendada.
- Popularidad y comunidad sólida.
- Facilidad de uso y aprendizaje.
- Amplia compatibilidad tecnológica.
- Rendimiento adecuado para proyectos pequeños y medianos.
- Flexibilidad de licencias y costos reducidos.
- Instalación y administración sencillas.
