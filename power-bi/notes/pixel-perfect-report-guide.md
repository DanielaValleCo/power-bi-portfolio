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
