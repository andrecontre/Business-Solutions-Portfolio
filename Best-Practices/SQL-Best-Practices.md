# 📖 SQL: Guía de Estilo y Comandos Críticos
Este manual define el estándar de escritura de consultas para asegurar que el motor de base de datos (MySQL/SQL Server) trabaje de forma eficiente.

## 1. Reglas de Escritura (Clean Code)
* **Palabras clave en MAYÚSCULAS:** Para diferenciar comandos de nombres de tablas/columnas. (Ej: `SELECT`, `FROM`, `WHERE`).
* **Identación Clara:** Cada cláusula principal debe ir en una nueva línea para facilitar la lectura.
* **Alias Descriptivos:** Usa `AS` para dar nombres claros a las columnas calculadas, especialmente si irán a un reporte.

## 2. Operadores y Filtros
* **Exactitud vs. Flexibilidad:**
    * `=` para coincidencias exactas (Case Sensitive según la DB).
    * `LIKE '%texto%'` para búsquedas parciales (Fuzzy Match).
* **Filtros Eficientes:** Usa `IN` para listas de valores y `BETWEEN` para rangos de fechas, evitando múltiples `OR` que ralentizan la consulta.

## 3. Funciones de Agregación y Lógica
* **Matemática Segura:** Siempre que uses `SUM`, `COUNT` o `AVG`, recuerda que todas las columnas que NO tengan una función deben estar en el `GROUP BY`.
* **Lógica Condicional:** Usa `CASE WHEN... THEN... ELSE... END` para crear categorías o etiquetas directamente desde la base de datos, ahorrando trabajo en el dashboard.

## 4. Joins (Relaciones)
* **Punto de Unión:** Siempre verifica que las columnas de unión (Keys) tengan el mismo tipo de dato.
* **Integridad de Datos:** Prefiere `LEFT JOIN` cuando la prioridad es no perder registros de la tabla principal, incluso si no hay coincidencia en la tabla secundaria.
