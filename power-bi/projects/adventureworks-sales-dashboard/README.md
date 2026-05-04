# Dashboard de Desempeño de Ventas de AdventureWorks

## Descripción del proyecto

Este dashboard en Power BI analiza el desempeño comercial de **AdventureWorks** durante el periodo **2017 a 2020**, con enfoque en ventas, rentabilidad a nivel producto, desempeño regional, comportamiento de resellers, estrategia de precios y monitoreo de KPIs.

El objetivo de este proyecto no fue solamente crear visualizaciones, sino construir un reporte orientado a negocio, donde cada página responde una pregunta analítica específica.

El archivo de Power BI está incluido en esta carpeta del proyecto:

```text
adventureworks-sales-performance-dashboard.pbix
```

Como los archivos `.pbix` no pueden visualizarse directamente en GitHub, se incluyen capturas de pantalla de cada página del reporte.

---

## Vista previa del reporte

### 1. Executive Overview

<img width="1261" height="707" alt="image" src="https://github.com/user-attachments/assets/d05296a5-b3a1-4b62-be72-582d9c490119" />

### 2. Product Category Performance

<img width="1185" height="697" alt="image" src="https://github.com/user-attachments/assets/87d297d7-ce28-4f20-abde-7f8a496eb167" />

### 3. Product Profitability Analysis

<img width="1231" height="641" alt="image" src="https://github.com/user-attachments/assets/701ae5b1-b525-434c-8936-c8edcfb29fb8" />

### 4. Regional Sales Performance

<img width="1278" height="716" alt="image" src="https://github.com/user-attachments/assets/2075b1f5-7c54-46cc-ab51-83b630cd03b7" />


### 5. Customer and Reseller View

<img width="1291" height="722" alt="image" src="https://github.com/user-attachments/assets/deb0c2b7-b23b-4801-8a04-35ac2202bc90" />


### 6. Pricing and Margin Strategy

<img width="1292" height="722" alt="image" src="https://github.com/user-attachments/assets/eb722ea7-5b68-46df-8543-5125fcf4fd6c" />


### 7. KPI Performance

<img width="1230" height="713" alt="image" src="https://github.com/user-attachments/assets/c72c0b9e-b863-4bf4-97b9-33b318fdf09c" />


---

## Dataset

El reporte utiliza el dataset de ejemplo **AdventureWorks Sales**.

El modelo sigue una lógica de **modelo estrella**, donde `Sales` funciona como la tabla central de hechos y varias tablas de dimensión se utilizan para filtrar y analizar la información.

### Tabla principal de hechos

- `Sales`

### Principales tablas de dimensión

- `Date`
- `Product`
- `Customer`
- `Reseller`
- `SalesTerritory`
- `SalesOrder`

---

## Notas sobre el modelo de datos

La tabla central de este reporte es `Sales`, ya que contiene los principales hechos comerciales:

- Importe de ventas
- Costo del producto
- Cantidad vendida
- Precio unitario
- Llaves de producto
- Llaves de cliente
- Llaves de reseller
- Llaves de territorio
- Llaves de fecha

La relación principal utilizada en el reporte es:

```text
Date[DateKey] → Sales[OrderDateKey]
```

Esto significa que las ventas se analizan con base en la **fecha en que se realizó la orden**.

La tabla `Sales` también contiene el campo `DueDateKey`, pero este no se utilizó como la relación principal de fecha porque el objetivo del reporte es analizar ventas por fecha de orden, no por fecha de vencimiento o entrega esperada.

En otro tipo de análisis, `DueDateKey` podría ser útil para responder preguntas relacionadas con entregas, vencimientos, tiempos operativos o cumplimiento logístico. Sin embargo, para este dashboard, `OrderDateKey` es el campo correcto porque el reporte se enfoca en cuándo se realizaron las ventas.

---

## Nota importante sobre validación de datos

Aunque la tabla `Date` incluye el año **2021**, la tabla de hechos `Sales` contiene registros de ventas únicamente de **2017 a 2020** con base en `OrderDateKey`.

Por esta razón, el reporte se enfoca en el periodo de ventas **2017–2020**, y la página de KPIs está filtrada a **2020**, que es el último año disponible con datos de ventas.

Este fue un paso importante de validación, porque al seleccionar 2021 en el filtro de fecha, los valores de ventas aparecen en blanco. La presencia de 2021 en la tabla `Date` no significa que existan ventas en 2021. Solo significa que la tabla calendario incluye ese año.

Esta distinción es importante porque una tabla calendario puede contener fechas que no necesariamente existen en la tabla de hechos. En este caso, 2021 existe en la dimensión de fechas, pero no tiene transacciones de ventas relacionadas a través de `OrderDateKey`.

---

## Medidas DAX principales

Las siguientes medidas DAX fueron creadas para el reporte.

### Total Sales

```DAX
Total Sales = SUM(Sales[Sales Amount])
```

Esta medida calcula el ingreso total por ventas.

---

### Total Cost

```DAX
Total Cost = SUM(Sales[Total Product Cost])
```

Esta medida calcula el costo total de producto disponible en el dataset.

---

### Total Profit

```DAX
Total Profit = [Total Sales] - [Total Cost]
```

Esta medida calcula la utilidad con base en el importe de ventas menos el costo total de producto.

---

### Profit Margin

```DAX
Profit Margin = DIVIDE([Total Profit], [Total Sales])
```

Esta medida calcula el porcentaje de ventas que permanece después de restar el costo del producto.

---

### Total Quantity

```DAX
Total Quantity = SUM(Sales[Order Quantity])
```

Esta medida calcula la cantidad total vendida.

---

### Average Unit Price

```DAX
Average Unit Price = AVERAGE(Sales[Unit Price])
```

Esta medida se utiliza en la página de análisis de precios.

---

## Interpretación de Profit

En este reporte, `Profit` se calcula como:

```text
Sales Amount - Total Product Cost
```

Por lo tanto, `Profit Margin` debe interpretarse como un margen a nivel producto basado en los datos de costo disponibles.

No debe interpretarse como margen neto final de la empresa, porque el dataset no incluye gastos operativos como:

- Salarios
- Renta
- Luz
- Marketing
- Impuestos
- Gastos administrativos
- Gastos financieros

En un contexto real de negocio, un análisis completo de utilidad neta requeriría información adicional sobre gastos operativos.

Esta es una limitación importante del dataset. El reporte permite analizar margen después del costo directo del producto, pero no permite evaluar la rentabilidad final de la empresa después de todos sus gastos.

---

## Medidas de objetivo

Como el dataset no incluye metas oficiales de negocio, se crearon benchmarks ilustrativos con fines de diseño y práctica del dashboard.

En un contexto real, estas metas deberían validarse con el equipo financiero, de planeación comercial o con dirección.

---

### Target Sales

```DAX
Target Sales = 25000000
```

La meta de ventas se estableció en **25M** para 2020. Este valor se definió como un benchmark ilustrativo razonable porque las ventas totales de 2020 fueron aproximadamente **24.47M**.

---

### Min Sales

```DAX
Min Sales = 0
```

---

### Max Sales

```DAX
Max Sales = 50000000
```

El valor máximo de ventas se estableció en **50M** para tener una escala legible en el gauge, considerando que el mayor valor anual de ventas en el dataset fue aproximadamente **42.90M** en 2019.

---

### Target Profit Margin

```DAX
Target Profit Margin = 0.15
```

La meta de margen de utilidad se estableció en **15%** con base en el rango histórico observado.

Márgenes de utilidad anuales observados:

```text
2017 → 15.77%
2018 → 9.55%
2019 → 9.97%
2020 → 14.23%
Total → 11.43%
```

La meta de 15% se encuentra cerca del mejor desempeño histórico, por lo que funciona como un benchmark ambicioso pero realista.

---

### Min Profit Margin

```DAX
Min Profit Margin = 0
```

---

### Max Profit Margin

```DAX
Max Profit Margin = 0.20
```

El margen máximo se estableció en **20%** en lugar de 100%, porque los márgenes observados son mucho menores. Esto hace que el gauge sea más legible y útil para el análisis.

---

# Páginas del reporte

---

## 1. Executive Overview

### Pregunta de negocio

¿Cómo se desempeñó AdventureWorks de forma general entre 2017 y 2020 en términos de ventas, utilidad y margen?

### Preguntas que responde

- ¿Cuáles fueron las ventas totales?
- ¿Cuánta utilidad se generó?
- ¿Cuál fue el margen general de utilidad?
- ¿Qué año tuvo el mayor desempeño en ventas?
- ¿La utilidad se movió en la misma dirección que las ventas?
- ¿Cómo se comportó el negocio durante el periodo disponible?

### Visualizaciones utilizadas

- Tarjeta: Total Sales
- Tarjeta: Total Profit
- Tarjeta: General Profit Margin
- Gráfico combinado: Total Sales y Total Profit por año
- Segmentador: Año

### Interpretación de la página

La página muestra ventas totales de aproximadamente **109.81M**, utilidad total de aproximadamente **12.55M** y un margen general de utilidad de **11.43%**.

La tendencia anual muestra que **2019 fue el año más fuerte en ventas**, alcanzando aproximadamente **42.90M**. La utilidad también aumentó de 2017 a 2019 y después disminuyó en 2020.

Esta página ofrece una vista ejecutiva general del negocio antes de pasar a los análisis por producto, región, reseller y pricing.

### Observación de negocio

La tendencia general sugiere que las ventas y la utilidad se mueven en una dirección similar. Sin embargo, la caída en 2020 indica que el último año disponible tuvo un desempeño menor que 2019.

Esta página funciona como punto de partida ejecutivo porque responde la primera pregunta del reporte:

> ¿Cómo se está desempeñando el negocio en general?

### Notas de diseño

Se utilizaron tarjetas para las métricas clave porque permiten entender rápidamente la escala general del negocio. El gráfico combinado se utilizó porque permite comparar dos medidas relacionadas: ventas totales y utilidad total.

La página también incluye un segmentador de año para que el usuario pueda explorar el periodo disponible de 2017 a 2020.

---

## 2. Product Category Performance

### Pregunta de negocio

¿Qué categorías de producto generan mayores ventas y utilidad?

### Preguntas que responde

- ¿Qué categoría vende más?
- ¿Qué categoría genera más utilidad?
- ¿La categoría que más vende también es la que más utilidad genera?
- ¿Qué tan concentradas están las ventas por categoría?
- ¿Qué subcategorías explican la mayor parte de las ventas?

### Visualizaciones utilizadas

- Treemap: Sales by Category and Subcategory
- Gráfico de barras: Total Profit by Category
- Segmentador: Año

### Interpretación de la página

El treemap muestra que **Bikes** domina las ventas totales. El gráfico de utilidad por categoría también muestra que Bikes genera la mayor utilidad total.

Esto indica que AdventureWorks depende fuertemente de la categoría Bikes tanto como generadora de ingresos como de utilidad.

### Observación de negocio

Esta concentración puede ser positiva porque Bikes es claramente una categoría fuerte. Sin embargo, también puede representar un riesgo si la empresa depende demasiado de una sola categoría.

Si la demanda de Bikes disminuye, si existen problemas de suministro o si hay presión en precios, el negocio completo podría verse afectado de forma importante.

### Notas de diseño

El treemap se utilizó para mostrar la composición de ventas por categoría y subcategoría. Este visual es útil cuando el objetivo es entender cuánto contribuye cada grupo al total.

El gráfico de barras complementa al treemap porque muestra utilidad total por categoría. Esto es importante porque la categoría con mayores ventas no siempre es la que genera mayor utilidad.

En este caso, Bikes domina tanto ventas como utilidad.

---

## 3. Product Profitability Analysis

### Pregunta de negocio

¿Qué productos venden mucho, pero tienen baja rentabilidad?

### Preguntas que responde

- ¿Qué productos generan mayores ventas?
- ¿Qué productos tienen mayor margen de utilidad?
- ¿Existen productos con ventas altas pero margen bajo?
- ¿Qué productos podrían requerir revisión de precio o costo?
- ¿Qué categorías contienen los productos más rentables?
- ¿Existen productos más pequeños con buenos márgenes?

### Visualización utilizada

Scatter plot:

- Eje X: Total Sales
- Eje Y: Profit Margin
- Tamaño de burbuja: Total Quantity
- Leyenda: Product Category
- Detalle: Product

### Interpretación de la página

Cada burbuja representa un producto. La posición de cada producto muestra su desempeño en ventas y su margen de utilidad, mientras que el tamaño de la burbuja muestra la cantidad vendida.

El scatter plot puede interpretarse usando cuatro grupos:

```text
Ventas altas + Margen alto
→ Productos estrella

Ventas altas + Margen bajo
→ Productos de alto volumen que podrían necesitar revisión de margen

Ventas bajas + Margen alto
→ Productos más pequeños pero rentables, con potencial de crecimiento

Ventas bajas + Margen bajo
→ Productos débiles o de baja prioridad
```

### Observación de negocio

Esta página va más allá de identificar simplemente los productos más vendidos. Ayuda a distinguir entre productos que generan ingresos y productos que realmente son rentables.

Algunos productos pueden tener ventas altas pero márgenes relativamente bajos. Esos productos podrían requerir una revisión más profunda de precios, estructura de costos o estrategia comercial.

Por otro lado, productos con ventas más bajas pero márgenes fuertes podrían representar oportunidades de crecimiento.

### Notas de diseño

Se seleccionó un scatter plot porque la página compara dos variables numéricas al mismo tiempo: ventas totales y margen de utilidad.

El tamaño de cada burbuja agrega una tercera capa de análisis al mostrar la cantidad total vendida.

Esta página también ilustra un concepto importante de DAX: `Profit Margin` es una medida dinámica. No se calcula automáticamente “por producto” a menos que el visual proporcione un contexto a nivel producto. En este scatter plot, como `Product` se usa como campo de detalle, Power BI evalúa la medida para cada producto.

---

## 4. Regional Sales Performance

### Pregunta de negocio

¿Qué regiones o territorios impulsan las ventas y la rentabilidad?

### Preguntas que responde

- ¿Qué regiones generan mayores ventas?
- ¿Qué regiones tienen mayor margen de utilidad?
- ¿Las regiones con mayores ventas también tienen buenos márgenes?
- ¿Existen regiones con bajo desempeño?
- ¿Cómo se distribuye geográficamente el desempeño comercial?

### Visualizaciones utilizadas

- Mapa: Total Sales by Region
- Gráfico de barras: Profit Margin by Region
- Segmentador: Año

### Interpretación de la página

El mapa ofrece una vista geográfica de la distribución de ventas. El gráfico de margen por región complementa el mapa al permitir una comparación más precisa de rentabilidad por región.

Esta página muestra que una región puede tener ventas fuertes, pero no necesariamente el margen más alto. Por esta razón, ventas y margen deben analizarse en conjunto.

### Observación de negocio

El desempeño regional no debería evaluarse únicamente con volumen de ventas. Una región con menores ventas puede tener una rentabilidad fuerte si sus márgenes son más altos.

De la misma forma, una región con ventas altas puede requerir atención si su margen es débil.

### Notas de diseño

El mapa se utilizó para dar contexto geográfico. Sin embargo, los mapas no siempre son ideales para comparar valores exactos. Por esa razón, se incluyó un gráfico de barras para comparar el margen de utilidad por región de manera más clara.

Esta página combina exploración geográfica con una comparación más precisa de rentabilidad.

---

## 5. Customer and Reseller View

### Pregunta de negocio

¿El negocio depende fuertemente de ciertos resellers o tipos de negocio?

### Preguntas que responde

- ¿Qué reseller genera mayores ventas?
- ¿Qué tipo de negocio contribuye más a las ventas?
- ¿Qué resellers tienen márgenes fuertes?
- ¿Existen resellers con ventas altas pero utilidad negativa o baja?
- ¿Qué significa “Not Applicable” en el análisis por Business Type?

### Visualizaciones utilizadas

- Tabla: Total Sales, Reseller, Total Profit, Profit Margin
- Treemap: Total Sales by Business Type
- Segmentador: Region

### Interpretación de la página

La tabla permite comparar de forma detallada a los resellers, incluyendo ventas, utilidad y margen de utilidad.

El treemap muestra la distribución de ventas por tipo de negocio. Warehouse aparece como un contribuyente importante, seguido por otros tipos de negocio como Value Added Reseller y Specialty Bike Shop.

### Nota sobre “Not Applicable”

La categoría “Not Applicable” probablemente representa ventas que no están asociadas con un tipo de negocio específico de reseller. Esto no necesariamente significa que exista un error en los datos.

Significa que, para esos registros de ventas, el tipo de negocio de reseller no aplica o no está disponible.

Dependiendo de la pregunta de negocio, esta categoría podría mantenerse por transparencia o filtrarse si la página se enfoca únicamente en desempeño específico de resellers.

### Observación de negocio

Esta página ayuda a identificar si las ventas están concentradas en resellers o tipos de negocio específicos.

Si un número pequeño de resellers o tipos de negocio aporta una gran proporción de ventas, el negocio puede depender fuertemente de esos canales.

### Notas de diseño

La tabla proporciona valores detallados a nivel reseller. El treemap ofrece una composición visual de ventas por tipo de negocio.

Durante el análisis, fue importante validar que “Not Applicable” no era necesariamente un error, sino una categoría que aparece porque algunas ventas no tienen un tipo de negocio de reseller aplicable.

---

## 6. Pricing and Margin Strategy

### Pregunta de negocio

¿Qué productos tienen una relación favorable o desfavorable entre precio promedio, ventas y margen de utilidad?

### Preguntas que responde

- ¿Los productos con mayor precio tienen mejores márgenes?
- ¿Qué productos tienen precios altos pero márgenes bajos?
- ¿Qué productos tienen precios bajos pero márgenes fuertes?
- ¿Qué categorías se comportan mejor en términos de precio y rentabilidad?
- ¿Los descuentos explican diferencias en rentabilidad?

### Visualizaciones utilizadas

- Scatter plot: Average Unit Price vs Profit Margin
- Tamaño de burbuja: Total Sales
- Leyenda: Product Category
- Tabla: Category, Product, Average Unit Price, Total Sales, Profit Margin
- Segmentador: Año

### Interpretación de la página

El scatter plot analiza la relación entre el precio de los productos y su rentabilidad.

Los productos con precios altos y márgenes fuertes pueden considerarse productos premium y rentables. Los productos con precios altos pero márgenes débiles podrían requerir una revisión más profunda de costos o estrategia de precios.

La tabla complementa el scatter plot porque permite identificar productos específicos por nombre y valor.

### Nota sobre análisis de descuentos

Inicialmente se consideró realizar un análisis de descuentos, pero el campo `Unit Price Discount Pct` mostró poca o nula variación en el dataset.

Por esta razón, la página de pricing se enfoca en:

- Average Unit Price
- Total Sales
- Product Cost
- Profit Margin

en lugar de analizar impacto de descuentos.

Esta fue una decisión analítica importante porque no todos los campos disponibles aportan información significativa.

### Observación de negocio

La página ayuda a identificar si los niveles de precio están alineados con la rentabilidad.

Un producto de precio alto con margen bajo puede indicar costos elevados o una estrategia de precios ineficiente. Un producto de precio bajo con margen fuerte podría ser buen candidato para promoción o crecimiento.

### Notas de diseño

La idea original era analizar descuentos y rentabilidad. Sin embargo, después de validar el campo de descuentos, se observó que los descuentos no eran un driver útil en este dataset.

En lugar de forzar una visualización débil, la página se rediseñó alrededor de estrategia de precio y margen. Esto hace que el análisis sea más significativo.

---

## 7. KPI Performance

### Pregunta de negocio

¿El negocio está cumpliendo sus objetivos de ventas y rentabilidad en 2020?

### Preguntas que responde

- ¿Las ventas de 2020 alcanzaron la meta?
- ¿El margen de utilidad de 2020 alcanzó la meta?
- ¿Qué tan cerca estuvo el negocio de sus objetivos?
- ¿Cómo se comportó el margen de utilidad durante 2020?

### Filtro de página

Esta página está filtrada a:

```text
Date - Year = 2020
```

La página se enfoca en 2020 porque es el último año con datos de ventas en la tabla `Sales`.

Aunque la tabla `Date` incluye 2021, no existen registros de ventas relacionados en 2021 usando `OrderDateKey`.

### Visualizaciones utilizadas

- Gauge: Total Sales vs Target Sales
- KPI: Profit Margin vs Target Profit Margin
- Gráfico de línea: Profit Margin by Month

### Interpretación del gauge de ventas

El gauge muestra:

```text
Total Sales 2020: 24.47M
Target Sales: 25M
Max Sales: 50M
```

Esto significa que AdventureWorks alcanzó aproximadamente:

```text
24.47 / 25 = 97.9%
```

de la meta ilustrativa de ventas para 2020.

### Interpretación del KPI de margen

El KPI muestra:

```text
Profit Margin 2020: 14.23%
Target Profit Margin: 15.00%
```

Power BI muestra una diferencia relativa aproximada de:

```text
-5.15%
```

Esto no significa que el margen esté 5.15 puntos porcentuales por debajo de la meta.

La diferencia en puntos porcentuales es:

```text
15.00% - 14.23% = 0.77 puntos porcentuales
```

El `-5.15%` representa la brecha relativa comparada con el objetivo:

```text
(14.23% - 15.00%) / 15.00% ≈ -5.15%
```

### Nota sobre el diseño del KPI

Cuando se usa Month como eje de tendencia en el KPI, Power BI muestra el último valor mensual, no el margen anual de 2020. Esto provocó que el KPI mostrara un valor mucho más bajo para el último mes.

Por esa razón:

```text
Gauge / KPI → mejor para comparación contra objetivo
Line chart → mejor para análisis de tendencia mensual
```

El diseño final separa la comparación anual contra objetivo de la interpretación de tendencia mensual.

### Observación de negocio

La página de KPIs muestra que las ventas de 2020 estuvieron muy cerca del objetivo ilustrativo, mientras que el margen de utilidad quedó ligeramente por debajo del benchmark de 15%.

Esta página ofrece una
