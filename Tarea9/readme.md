# Funciones o procedimientos de almacenamiento Tarea 9

## ✅ 1. Función: Distancia de Levenshtein

```sql
DELIMITER //

CREATE FUNCTION func_levenshtein(s1 TEXT, s2 TEXT)
RETURNS INT
DETERMINISTIC
BEGIN
  DECLARE s1_len, s2_len, i, j, cost INT;
  DECLARE ch1 CHAR(1);
  DECLARE ch2 CHAR(1);
  DECLARE dist INT;

  SET s1_len = CHAR_LENGTH(s1);
  SET s2_len = CHAR_LENGTH(s2);
  
  IF s1 = s2 THEN
    RETURN 0;
  END IF;
  
  IF s1_len = 0 THEN
    RETURN s2_len;
  END IF;
  
  IF s2_len = 0 THEN
    RETURN s1_len;
  END IF;
  
  CREATE TEMPORARY TABLE dist_table (
    i INT,
    j INT,
    val INT,
    PRIMARY KEY (i, j)
  );

  SET i = 0;
  WHILE i <= s1_len DO
    INSERT INTO dist_table VALUES (i, 0, i);
    SET i = i + 1;
  END WHILE;

  SET j = 0;
  WHILE j <= s2_len DO
    INSERT INTO dist_table VALUES (0, j, j);
    SET j = j + 1;
  END WHILE;

  SET i = 1;
  WHILE i <= s1_len DO
    SET ch1 = SUBSTRING(s1, i, 1);
    SET j = 1;
    WHILE j <= s2_len DO
      SET ch2 = SUBSTRING(s2, j, 1);
      IF ch1 = ch2 THEN
        SET cost = 0;
      ELSE
        SET cost = 1;
      END IF;

      SELECT val FROM dist_table WHERE i = i-1 AND j = j INTO @del;
      SELECT val FROM dist_table WHERE i = i AND j = j-1 INTO @ins;
      SELECT val FROM dist_table WHERE i = i-1 AND j = j-1 INTO @sub;

      SET dist = LEAST(@del + 1, @ins + 1, @sub + cost);
      INSERT INTO dist_table VALUES (i, j, dist);
      SET j = j + 1;
    END WHILE;
    SET i = i + 1;
  END WHILE;

  SELECT val INTO dist FROM dist_table WHERE i = s1_len AND j = s2_len;
  DROP TEMPORARY TABLE dist_table;

  RETURN dist;
END;
//

DELIMITER ;

SELECT func_levenshtein('refresco', 'resfresco');
```

## ✅ 2. Función: Cantidad de elementos de un arreglo
```sql
DELIMITER //

CREATE FUNCTION contar_elementos(texto TEXT)
RETURNS INT
DETERMINISTIC
BEGIN
  DECLARE total INT DEFAULT 1;
  DECLARE pos INT;

  SET pos = LOCATE(',', texto);

  WHILE pos > 0 DO
    SET total = total + 1;
    SET texto = SUBSTRING(texto, pos + 1);
    SET pos = LOCATE(',', texto);
  END WHILE;

  RETURN total;
END;
//

DELIMITER ;

SELECT contar_elementos('queso,jamon,pan,lechuga');
```

# 📊 Reporte de Funciones Almacenadas en MySQL

## 1. Función: `func_levenshtein`

### 🔍 ¿Qué hace?

Esta función calcula la **distancia de Levenshtein**, es decir, el número mínimo de operaciones (inserciones, eliminaciones o sustituciones) necesarias para transformar una cadena en otra. Es útil para comparar cadenas similares como nombres de productos o clientes.

### 🧠 ¿Cómo funciona?

1. Compara cada carácter de una cadena con la otra.
2. Usa una tabla temporal para almacenar los resultados parciales.
3. Itera sobre cada posición de ambas cadenas y calcula el mínimo entre:
   - Eliminar un carácter.
   - Insertar un carácter.
   - Sustituir un carácter.

### 📌 Ejemplo de uso:
```sql
SELECT func_levenshtein('refresco', 'resfresco');
-- Resultado esperado: 1
```

## 2. Función: contar_elementos
### 🔍 ¿Qué hace?
Cuenta la cantidad de elementos en una cadena que simula un arreglo, separados por comas. Útil cuando recibimos listas de ingredientes, productos, o cualquier valor separado por comas.

### 🧠 ¿Cómo funciona?
Usa LOCATE para encontrar las comas.
Por cada coma encontrada, aumenta el contador en 1.
Repite hasta que no haya más comas.

### 📌 Ejemplo de uso:
```sql
SELECT contar_elementos('jamon,queso,lechuga,tomate');
-- Resultado esperado: 4
```

## 3. Consideraciones
Ambas funciones son determinísticas y pueden ser usadas dentro de consultas SELECT o procedimientos.
No requieren tablas específicas, por lo que pueden reutilizarse en otros contextos dentro de la base tienda_abarrotes_lili.

## 4. Recomendaciones de uso
La función de Levenshtein puede ayudar a detectar errores tipográficos en nombres de productos.
La función de contar elementos es útil para datos importados de archivos CSV o campos tipo texto con listas.