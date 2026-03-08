# 📊 DAX: Reglas de Oro para Power BI
Este manual establece los estándares de desarrollo para asegurar modelos de datos rápidos, precisos y fáciles de mantener.

## 1. La Regla de Oro: Medidas vs. Columnas
* **Usa Medidas siempre que sea posible:** Las medidas se calculan en tiempo de ejecución y no consumen memoria RAM del modelo de manera estática.
* **Columnas Calculadas solo para dimensiones:** Solo usa columnas calculadas si necesitas usarlas como **filtros (Slicers)** o en las **filas/columnas** de una matriz. Nunca para operaciones matemáticas simples.

## 2. Funciones de Agregación Seguras
* **Usa `DIVIDE()` en lugar de `/`:** La función `DIVIDE` maneja automáticamente el error de división por cero, devolviendo un blanco en lugar de un error que rompa el visual.
    * *Bien:* `DIVIDE([Ventas], [Meta])`
    * *Mal:* `[Ventas] / [Meta]`
* **Medidas Explícitas:** Nunca uses las "medidas implícitas" (arrastrar un campo y que Power BI le ponga suma). Crea siempre la medida: `Total Ventas = SUM(Fact_Ventas[Monto])`. Esto permite que otras medidas reutilicen esta lógica.

## 3. Mejores Prácticas de Rendimiento
* **Variables (`VAR` / `RETURN`):** Usa variables para evitar que Power BI calcule lo mismo dos veces. Las variables mejoran la lectura y el rendimiento.
* **Filtros Inteligentes:** Prefiere `KEEPFILTERS` o filtros específicos en lugar de `FILTER(ALL(Tabla)...)` si no es estrictamente necesario, para no sobrecargar el motor vertical (VertiPaq).

## 4. Estándares de Formato
* **Nombres Claros:** Las medidas deben tener nombres de negocio (ej. `Crecimiento Ventas YoY` en lugar de `medida_v1`).
* **Comentarios:** Si una lógica de `CALCULATE` es compleja, usa `//` para explicar qué filtro se está aplicando para mi "yo del futuro".

---
> "Un buen modelo de datos hace que el DAX sea sencillo. Si el DAX es demasiado complejo, probablemente el modelo de datos (Power Query) necesita trabajo."
