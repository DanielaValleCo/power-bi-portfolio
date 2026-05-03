# Guía para crear un buen Pixel Perfect Report en Power BI

Estas notas resumen las principales buenas prácticas que aprendí durante el curso de visualización de datos en Power BI. No están pensadas como una lista de pasos mecánicos, sino como una guía para diseñar reportes más claros, útiles y orientados a negocio.

La idea central es que un dashboard no debe ser solamente una colección de gráficas bonitas. Un buen reporte debe ayudar a responder preguntas importantes, reducir el esfuerzo de interpretación del usuario y facilitar la toma de decisiones.

---

## 1. ¿Qué hace bueno a un dashboard?

Un buen dashboard no es el que tiene más visualizaciones, más colores o más elementos en pantalla. Un buen dashboard es aquel que permite entender rápidamente qué está pasando y qué decisión podría tomarse a partir de los datos.

Antes de construir un reporte conviene preguntarse:

- ¿Qué necesita saber el usuario?
- ¿Qué decisión quiere tomar?
- ¿Qué métricas son realmente importantes?
- ¿Qué visual ayuda mejor a responder esa pregunta?
- ¿Qué puedo quitar para que el tablero sea más claro?

Una de las ideas más importantes del curso fue la reducción de la carga cognitiva. Es decir, evitar que el usuario tenga que esforzarse demasiado para entender la información. Si una página tiene demasiadas gráficas, colores, filtros, textos o historias mezcladas, el usuario puede perderse aunque los datos sean correctos.

Un reporte efectivo debe guiar la mirada del usuario hacia lo importante.

---

## 2. Principios esenciales de diseño de dashboards

### 2.1 Una historia por página

Cada página de un reporte debe responder una historia principal. Esto ayuda a que el usuario no tenga que interpretar demasiadas ideas al mismo tiempo.

No conviene mezclar en una sola página temas como:

- Ventas por producto
- Costos por canal
- Utilidad por mes
- Devoluciones
- Participación por categoría
- Cumplimiento de metas

Todos esos temas pueden ser importantes, pero funcionan mejor si se organizan en páginas separadas.

Una estructura más clara podría ser:

- Página 1: Resumen ejecutivo
- Página 2: Desempeño de productos
- Página 3: Desglose por canal o retailer
- Página 4: Rentabilidad y metas
- Página 5: KPIs y seguimiento

La clave es que cada página tenga un propósito claro.

---

### 2.2 Preguntas antes de agregar cualquier elemento

Antes de agregar una tarjeta, gráfica, slicer, imagen, forma o texto, conviene hacerse tres preguntas:

1. ¿Esto contribuye a la historia?
2. ¿Es el elemento visual correcto?
3. ¿Es necesario?

Si la respuesta a alguna de estas preguntas es “no”, probablemente ese elemento debería quitarse o replantearse.

Por ejemplo, si una página trata sobre ventas por producto en 2021, puede tener sentido mostrar:

- Sales Amount por Product Name
- Profit Margin por Product Category
- Un filtro de Product Category

Pero tal vez no aporta incluir:

- COGS por canal para todos los años
- Devoluciones por mes
- Una imagen decorativa grande
- Una tabla enorme sin propósito claro

Agregar más elementos no siempre mejora el reporte. Muchas veces lo vuelve más difícil de leer.

---

### 2.3 Menos es más

Un error común al crear dashboards es pensar que mientras más lleno esté el reporte, más profesional se ve. En realidad, un dashboard profesional suele ser más limpio, más claro y más intencional.

Un buen reporte normalmente tiene:

- Pocos colores
- Espacio en blanco
- Títulos claros
- Gráficas alineadas
- Números bien formateados
- Filtros útiles
- Una lectura visual ordenada

El espacio vacío no debe verse como desperdicio. El espacio vacío ayuda a separar secciones, da descanso visual y permite que el usuario identifique mejor la información importante.

---

### 2.4 Diseñar para la audiencia

No todos los usuarios necesitan el mismo nivel de detalle. Un reporte para un analista puede tener más tablas, más campos y más profundidad técnica. En cambio, un reporte para una persona ejecutiva debe ser más directo y enfocado en decisiones.

En el curso, la audiencia era una figura ejecutiva interesada en el desempeño comercial de la empresa. Por eso, el reporte se enfocaba en métricas como:

- Ventas
- Costos
- Utilidad
- Margen de ganancia
- Productos con mejor desempeño
- Cumplimiento de objetivos

Una audiencia ejecutiva normalmente quiere responder preguntas como:

- ¿Estamos vendiendo bien?
- ¿Dónde ganamos más?
- ¿Dónde perdemos margen?
- ¿Qué productos o canales necesitan atención?
- ¿Estamos cumpliendo las metas?

Para este tipo de usuario suelen funcionar bien:

- KPIs
- Tarjetas
- Gráficas de tendencia
- Comparaciones claras
- Medidas contra objetivo
- Formato condicional

En cambio, pueden ser menos útiles:

- Tablas demasiado largas
- Demasiadas columnas
- Detalles técnicos del modelo
- Visualizaciones decorativas sin función analítica

---

## 3. Buenas prácticas visuales

### 3.1 Usar color con intención

El color no debería usarse solo para decorar. Debe ayudar a guiar la atención.

Una regla práctica es:

- Colores neutros para dar contexto
- Un color fuerte para destacar algo importante

Por ejemplo, en una gráfica de barras se pueden dejar la mayoría de barras en gris y usar un color más fuerte para resaltar productos debajo del objetivo o productos con desempeño sobresaliente.

Si todo tiene colores fuertes, nada destaca. El color funciona mejor cuando se usa con moderación.

---

### 3.2 Usar títulos que expliquen

Los títulos no deberían limitarse a repetir los campos del gráfico.

Por ejemplo, un título como:

`Sales Amount by Product Name`

describe el gráfico, pero no necesariamente ayuda a interpretar.

Un título como:

`Top products driving 2021 sales`

da más contexto y orienta mejor al usuario.

Un buen título debería ayudar a responder:

- ¿Qué estoy viendo?
- ¿De qué periodo?
- ¿Con qué filtro?
- ¿Qué métrica importa?

Algunos ejemplos de títulos útiles:

- Revenue vs Cost by Product Category
- Gross Profit and Average Profit Margin Over Time
- Total Sales Amount by Product Women
- Orders Above Target Profit Margin
- Total Returns vs Target Returns by Month

---

### 3.3 Dar formato correcto a las métricas

El formato de los valores importa mucho. Un reporte puede verse poco profesional si los números aparecen sin formato, con demasiados decimales o con unidades inconsistentes.

Algunas reglas básicas:

- Ventas → moneda
- Costos → moneda
- Profit → moneda
- Profit Margin → porcentaje
- Order Quantity → número entero
- Fechas → formato legible

Ejemplos:

- `0.4930` debería mostrarse como `49.30%`
- `7084154` debería mostrarse como `£7,084,154.00`
- `4870` debería mostrarse como `4,870`

El formato correcto reduce fricción y hace que el usuario entienda más rápido.

---

### 3.4 Ordenar los visuales según la lectura natural

Normalmente, el usuario lee de arriba hacia abajo y de izquierda a derecha. Por eso, los elementos más importantes deben colocarse primero.

Una página ejecutiva puede organizarse así:

- Arriba: título, filtros globales y KPIs principales
- Centro: tendencia o visual principal
- Abajo: desglose por producto, canal o categoría

El orden visual debe ayudar a contar la historia.

---

## 4. Cómo elegir visualizaciones

Una de las partes más importantes al construir un dashboard es elegir la visualización adecuada. Para eso, conviene empezar por la pregunta de negocio, no por la gráfica.

No se trata de pensar primero:

> ¿Qué gráfica pongo?

Sino:

> ¿Qué pregunta quiero responder?

---

### 4.1 Para mostrar un número clave: tarjeta

Usar tarjetas cuando se quiere mostrar un valor principal.

Ejemplos:

- Total Sales
- Total Profit
- Average Profit Margin
- Total Orders
- Orders Above Target Profit Margin

Preguntas que responde:

- ¿Cuánto vendimos?
- ¿Cuánta utilidad generamos?
- ¿Cuántas órdenes superaron el margen objetivo?

---

### 4.2 Para ver evolución en el tiempo: línea o gráfico combinado

Usar gráficas de línea cuando se quiere analizar una tendencia en el tiempo.

Ejemplos:

- Sales Amount by Month
- Profit by Month
- Revenue, COGS and Profit by Month and Year

Preguntas que responde:

- ¿Las ventas están creciendo o bajando?
- ¿Hay meses con caídas importantes?
- ¿La utilidad sigue el mismo patrón que las ventas?
- ¿Los costos están creciendo más rápido que los ingresos?

También se puede usar un gráfico combinado cuando se quieren ver dos métricas relacionadas, por ejemplo:

- Columnas: Profit
- Línea: Profit Margin

Esto permite ver al mismo tiempo el monto total de utilidad y la eficiencia del negocio.

---

### 4.3 Para comparar categorías: barras

Usar barras horizontales o columnas cuando se quieren comparar categorías.

Ejemplos:

- Sales Amount by Product Name
- Order Quantity by Retailer Channel
- Profit by Product Category

Preguntas que responde:

- ¿Qué producto vendió más?
- ¿Qué categoría tuvo mayor utilidad?
- ¿Qué canal tuvo más pedidos?

Las barras horizontales son especialmente útiles cuando los nombres de las categorías son largos.

---

### 4.4 Para ver composición: barras apiladas, treemap o pie chart

Usar visualizaciones de composición cuando se quiere entender cómo se distribuye un total.

Ejemplos:

- Order Quantity by Retailer Channel and Product Category
- Sales Amount by Channel and Product Category

Preguntas que responde:

- ¿Cómo se distribuyen las órdenes por canal?
- ¿Qué categorías dominan dentro de cada canal?
- ¿Qué parte del total representa cada grupo?

El pie chart puede funcionar con pocas categorías, pero si hay demasiadas se vuelve difícil de leer. En esos casos, un treemap o barras apiladas suelen ser mejores opciones.

---

### 4.5 Para comparar dos variables: scatter plot

Usar scatter plot cuando se quiere analizar la relación entre dos variables numéricas.

Ejemplo:

- Sales Amount vs Cost of Goods Sold by Product Name

Preguntas que responde:

- ¿Qué productos venden mucho pero también cuestan mucho?
- ¿Qué productos tienen ventas altas y costos bajos?
- ¿Hay valores atípicos?
- ¿Existe relación entre ventas y costos?

Este tipo de gráfica es útil para detectar productos que merecen una revisión más detallada.

---

### 4.6 Para comparar contra una meta: gauge, KPI o tarjetas

Usar visualizaciones contra objetivo cuando se quiere medir desempeño frente a una meta.

Ejemplos:

- Avg Profit Margin vs Target Profit Margin
- Total Orders vs Target Orders
- Total Returns vs Target Returns

Preguntas que responde:

- ¿Estamos arriba o abajo del objetivo?
- ¿Qué tan lejos estamos de la meta?
- ¿El resultado va bien o mal?

Los gauges funcionan bien cuando se tiene un valor actual, un objetivo y un máximo. Los KPIs funcionan mejor cuando se quiere ver desempeño en el tiempo contra una meta.

---

### 4.7 Para muchas comparaciones pequeñas: small multiples

Usar small multiples cuando se quiere comparar el mismo tipo de gráfico en varios grupos.

Ejemplo:

- Order Quantity by Product Gender and Product Color

Preguntas que responde:

- ¿Cómo cambia la demanda por género dentro de cada color?
- ¿Qué colores venden más para hombres o mujeres?
- ¿Hay patrones repetidos entre categorías?

Los small multiples permiten comparar muchos grupos sin crear demasiadas gráficas separadas.

---

## 5. Preguntas de negocio del curso y cómo se abordaron

### Pregunta 1: ¿Cómo se relacionan ventas y costos?

Visual usado:

- Scatter plot

Campos:

- X-axis: Sales Amount
- Y-axis: Cost of Goods Sold
- Details: Product Name u Order Date

Lógica:

Si los puntos siguen una línea ascendente, significa que a mayores ventas también hay mayores costos. Si aparece un producto con ventas muy altas y costos relativamente bajos, puede ser muy rentable. Si aparece un producto con costos altos y ventas bajas, puede ser problemático.

Cómo se abordó:

- Se filtró por año.
- Se comparó Sales Amount contra Cost of Goods Sold.
- Se usó el detalle para identificar productos o fechas.

---

### Pregunta 2: ¿Qué productos venden más?

Visual usado:

- Bar chart horizontal

Campos:

- Axis: Product Name
- Values: Sales Amount

Lógica:

Las barras permiten ordenar productos de mayor a menor venta. Este tipo de visual es más claro que una tabla cuando el objetivo es comparar rápidamente productos.

Cómo se abordó:

- Se filtró por segmento o género.
- Se ordenaron las barras por Sales Amount.
- Se usó color para destacar productos relevantes.

---

### Pregunta 3: ¿Qué canales venden más por categoría?

Visual usado:

- Stacked bar chart

Campos:

- Y-axis: Retailer Channel
- X-axis: Order Quantity
- Legend: Product Category

Lógica:

Permite ver tanto el total por canal como la composición por categoría.

Cómo se abordó:

- Se compararon canales como Franchise, Local Store, Supermarket y Small Chain Store.
- Se desglosó cada canal por categorías de producto.

---

### Pregunta 4: ¿Cómo se comporta la utilidad en el tiempo?

Visual usado:

- Line and clustered column chart

Campos:

- Column y-axis: Profit
- Line y-axis: Profit Margin
- X-axis: Month and Year

Lógica:

Las columnas muestran la utilidad total, mientras que la línea muestra el margen promedio. Esto permite detectar si se gana más dinero total, pero con menor eficiencia.

Cómo se abordó:

- Se mostró Profit por mes.
- Se agregó Profit Margin como línea.
- Se aplicó filtro de categoría, por ejemplo Tank Tops.

---

### Pregunta 5: ¿Qué categorías tienen mayor revenue y cost?

Visual usado:

- Tornado chart / comparación Revenue vs Cost

Campos:

- Group: Product Category
- Values: Sales Amount y Product Cost

Lógica:

Permite comparar dos métricas enfrentadas por categoría. Es útil para ver si una categoría genera mucho ingreso pero también mucho costo.

Cómo se abordó:

- Se comparó Revenue vs Cost por categoría.
- Se identificaron categorías con brecha favorable o desfavorable.

---

### Pregunta 6: ¿El margen promedio está cerca del objetivo?

Visual usado:

- Gauge

Medidas DAX:

```DAX
Target Profit Margin = 0.70
```

Lógica:

El gauge permite ver rápidamente si el margen promedio está cerca o lejos de la meta.

Cómo se abordó:

Se calculó el Avg Profit Margin.
Se creó una medida objetivo de 70%.
Se creó una medida máxima de 100%.

### Pregunta 7: ¿Cuántas órdenes están arriba o abajo del margen objetivo?

Visual usado:
- Cards

Medidas:
- Orders Above Target Profit Margin
- Orders Below Target Profit Margin
Lógica:
Las tarjetas muestran cantidades concretas. Son útiles cuando se quiere que el usuario vea rápidamente cuántos casos cumplen o no cumplen una condición.

Cómo se abordó:
- Se creó una medida para contar órdenes con Profit Margin mayor al objetivo.
- Se creó otra medida para contar órdenes por debajo o igual al objetivo.

### Pregunta 8: ¿Las órdenes y devoluciones cumplen sus metas?

Visual usado:
- KPI visual

Campos:
- Indicator: Total Orders / Total Returns
- Trend axis: Month
- Target: Target Orders / Target Returns

Lógica:

Un KPI permite comparar desempeño actual contra una meta y mostrar si el resultado va bien o mal.

Cómo se abordó:

Se creó una meta fija para órdenes.
Se creó una meta fija para devoluciones.
En devoluciones, se configuró la interpretación considerando que menor es mejor.

## 6. Cómo pensar un reporte desde cero

Antes de abrir Power BI, conviene definir el objetivo del reporte. Esto evita construir visualizaciones sin dirección.

## 6.1 Definir el objetivo

Ejemplo:

Analizar el desempeño comercial de una tienda para identificar ventas, utilidad, margen y cumplimiento de metas.

## 6.2 Definir la audiencia

Ejemplo:

El reporte está dirigido a un perfil ejecutivo o comercial que necesita información rápida para tomar decisiones.

## 6.3 Definir las preguntas de negocio

Ejemplos:

¿Cuánto se vendió?
¿Qué productos generaron más ingresos?
¿Qué categorías son más rentables?
¿Cómo evolucionan ventas, costos y utilidad en el tiempo?
¿Qué canales concentran más órdenes?
¿Qué productos están debajo del margen objetivo?
¿Se cumplen las metas de órdenes y devoluciones?
## 6.4 Definir las métricas

Ejemplos:

Sales Amount
Cost of Goods Sold
Profit
Profit Margin
Order Quantity
Total Orders
Returns
Target Profit Margin

## 6.5 Definir las páginas

Ejemplo:

Página 1: Overview
Página 2: Product Performance
Página 3: Channel / Retailer Breakdown
Página 4: Profitability and Targets
Página 5: KPIs

### 7. Guía de lectura por página del Pixel Perfect Report

Esta sección funciona como una guía para explicar el reporte final. También sirve para practicar cómo presentar el dashboard en una entrevista o en un proyecto de portafolio.

Página 1: Order Details / Exploración inicial
<img width="617" height="357" alt="image" src="https://github.com/user-attachments/assets/9ae310d9-5a02-4932-afea-45f5bea9308a" />


En esta página se muestra una vista detallada de las órdenes, incluyendo campos como:

Order_ID
Product_SKU
Order_Quantity
Sales_Amount
Cost_of_Goods_Sold
Order_Date

También se incluyen visualizaciones como un scatter plot para comparar ventas contra costos.

Lectura de negocio:

Esta página permite explorar el detalle operativo de las órdenes y observar la relación entre ventas y costos. El scatter plot ayuda a identificar si los costos aumentan conforme aumentan las ventas y permite detectar posibles valores atípicos.

Cómo explicarla:

Esta página funciona como una exploración inicial. Primero reviso los registros de órdenes y después comparo Sales Amount contra Cost of Goods Sold para entender si existe una relación entre ingreso y costo. También agregué filtros por fecha y producto para analizar periodos específicos.

Página 2: Product Comparison
<img width="517" height="358" alt="image" src="https://github.com/user-attachments/assets/19a8263c-dc03-48be-9ec2-66aa7f3117f7" />


En esta página se comparan productos por ventas, especialmente filtrando por atributos como género, canal o categoría.

Visuales principales:

Bar chart de Sales Amount por Product Name
Slicers de Product Gender y Retailer Channel

Lectura de negocio:

La página permite identificar qué productos concentran más ventas y cómo cambia esa lectura al filtrar por género o canal. También permite destacar productos con mejor o peor desempeño.

Cómo explicarla:

Aquí el objetivo es comparar productos. Usé barras horizontales porque los nombres de productos son largos y porque este visual facilita ordenar de mayor a menor. Además, los slicers permiten que el usuario analice segmentos específicos sin saturar la página.

Página 3: Retailer Breakdown
<img width="538" height="352" alt="image" src="https://github.com/user-attachments/assets/5cfefff3-a22d-4376-a28e-2e34ea330a96" />


En esta página se analiza la cantidad de órdenes por canal y categoría.

Visual principal:

Stacked bar chart: Order Quantity by Retailer Channel and Product Category

Lectura de negocio:

Esta página ayuda a entender qué canales generan más órdenes y qué categorías dominan dentro de cada canal. Por ejemplo, se pueden comparar canales como Franchise, Local Store, Supermarket y Small Chain Store.

Cómo explicarla:

Esta página responde cómo se distribuyen las órdenes entre canales. Elegí una barra apilada porque permite ver el total de órdenes por canal y, al mismo tiempo, la composición por categoría.

Página 4: Small Multiples
<img width="603" height="357" alt="image" src="https://github.com/user-attachments/assets/42a05090-ffc7-49b1-ba01-589affa212ed" />


En esta página se analiza la cantidad de órdenes por género y color de producto.

Visual principal:

Small multiples: Order Quantity by Product Gender and Product Color

Lectura de negocio:

Esta página permite comparar patrones de compra entre hombres y mujeres para distintos colores. Es útil para detectar colores donde un género domina claramente o donde la demanda está más equilibrada.

Cómo explicarla:

Usé small multiples porque quería comparar varios grupos de color sin crear muchas gráficas separadas. Cada mini gráfico mantiene la misma estructura, lo que facilita comparar patrones visualmente.

Página 5: Revenue and Profit
<img width="627" height="352" alt="image" src="https://github.com/user-attachments/assets/6066fab0-92c8-4d1e-b578-e4d584917a42" />


En esta página se analiza el desempeño financiero en el tiempo.

Visuales principales:

Line chart: Revenue, COGS and Profit by Month and Year
Combo chart: Gross Profit and Average Profit Margin over time
Tornado chart: Revenue vs Cost by category

Lectura de negocio:

Esta página muestra si las ventas, costos y utilidad se mueven en la misma dirección. También permite analizar si una categoría genera alto ingreso pero también alto costo.

Cómo explicarla:

Esta página está enfocada en rentabilidad. No solo muestra cuánto se vendió, sino también cuánto costó y qué utilidad quedó. El gráfico combinado permite ver Profit junto con Profit Margin, lo cual ayuda a distinguir entre ganar más dinero total y ser más eficiente.

Página 6: Shares / Gauge / Cards
<img width="612" height="348" alt="image" src="https://github.com/user-attachments/assets/ddd6db22-075a-4141-a3ea-09f72d4ab58e" />


En esta página se trabaja con participación, márgenes y metas.

Visuales principales:

Treemap por Retailer Channel
Pie chart por Product Size
Gauge de Avg Profit Margin vs Target Profit Margin
Cards de órdenes arriba y abajo del margen objetivo

Lectura de negocio:

La página permite ver la distribución de ventas u órdenes por canal, el peso de las tallas y el cumplimiento del margen objetivo. Las tarjetas resumen cuántas órdenes están arriba o abajo del margen esperado.

Cómo explicarla:

Esta página combina participación y cumplimiento de metas. El treemap ayuda a ver qué canales ocupan mayor proporción. El gauge resume si el margen promedio se acerca al objetivo de 70%, y las tarjetas muestran cuántas órdenes superan o no ese margen.

Página 7: KPIs
<img width="602" height="308" alt="image" src="https://github.com/user-attachments/assets/45f8419a-44b3-4fc3-b9b0-fe9196b0b852" />

En esta página se comparan indicadores contra metas.

Visuales principales:

KPI de Total Orders vs Target Orders
KPI de Total Returns vs Target Returns

Lectura de negocio:

Esta página permite monitorear rápidamente si las órdenes y devoluciones están dentro de los objetivos esperados. En devoluciones, la interpretación cambia porque menor es mejor.

Cómo explicarla:

Esta página está pensada para seguimiento ejecutivo. Los KPIs permiten ver si el negocio cumple sus objetivos. Para órdenes, más suele ser mejor; para devoluciones, configuré la lógica considerando que menos devoluciones es mejor.

## 8. Checklist para un próximo proyecto propio
Antes de construir
 - Definí la audiencia.
 - Definí la pregunta principal del reporte.
 - Escribí las preguntas de negocio.
 - Identifiqué las métricas principales.
 - Separé el análisis en páginas.
Durante la construcción
 - Cada página cuenta una sola historia.
 - No hay visuales innecesarios.
 - Los filtros son útiles y no estorban.
 - Los títulos son claros.
 - Los colores tienen intención.
 - Las métricas tienen formato correcto.
 - Los elementos están alineados.
 - Hay suficiente espacio en blanco.
Antes de terminar
 - El usuario puede entender la página en menos de 10 segundos.
 - Las gráficas responden preguntas reales.
 - Las medidas DAX tienen nombres claros.
 - No hay nombres técnicos confusos.
 - Puedo explicar cada visualización.
 - Puedo justificar por qué elegí cada gráfica.

## 9. Para elegir visualizaciones

Número clave → Tarjeta
Tiempo → Línea o combo chart
Categorías → Barras
Composición → Treemap / stacked bar
Relación entre variables → Scatter plot
Meta → Gauge o KPI
Detalle → Tabla o matriz
Muchos grupos comparables → Small multiples
10. Conclusión personal

Este curso me ayudó a entender que Power BI no se trata únicamente de saber usar visualizaciones, sino de aprender a estructurar información para responder preguntas de negocio.

La parte más importante no es elegir una gráfica “bonita”, sino entender qué necesita ver el usuario, qué decisión quiere tomar y cuál es la forma más clara de mostrar la información.

Para mi siguiente proyecto, quiero aplicar esta lógica desde el inicio:

Definir la audiencia.
Escribir las preguntas de negocio.
Elegir métricas relevantes.
Separar el análisis por páginas.
Usar visualizaciones que respondan preguntas concretas.
Reducir ruido visual.
Explicar cada página como una historia de negocio.

El objetivo final es construir reportes más claros, más útiles y más fáciles de defender en un contexto profesional.
