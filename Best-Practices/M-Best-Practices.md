# ⚙️ Power Query & M: Limpieza de Datos Ética
El lenguaje M es el motor de transformación. Un buen proceso de ETL reduce el peso del archivo de Power BI en un 50% o más.

## 1. La Regla de "Carga Selectiva"
* **Eliminar Columnas Innecesarias:** Es el primer paso de cualquier flujo. Menos columnas = menos consumo de memoria RAM.
* **Filtrar Filas al Inicio:** Si solo necesitas los últimos 2 años, filtra de entrada para que Power Query no procese datos históricos irrelevantes.

## 2. Optimización de Tipos de Datos
* **Definición Explícita:** Nunca dejes columnas con el tipo "Any" (Cualquiera). Define siempre si es Texto, Número Entero o Fecha para evitar errores en DAX.
* **Redondeo Temprano:** Redondea los decimales en Power Query si no necesitas precisión extrema; esto mejora la compresión del motor VertiPaq.

## 3. Transformaciones Pro
* **Nombres de Pasos:** Renombra los pasos en el panel derecho (ej: "Filtrado de Ventas 2024" en lugar de "Filtered Rows").
* **Uso de Parámetros:** Si la fuente de datos cambia (ej: de una carpeta local a una de SharePoint), usa parámetros para actualizar la ruta en un solo clic.
