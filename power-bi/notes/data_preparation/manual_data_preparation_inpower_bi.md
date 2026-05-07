# Manual de preparación de datos en Power BI

> Compilación de notas del curso **Data Preparation in Power BI** y apuntes personales sobre limpieza, diagnóstico y transformación de datos con **Power Query**.

---

## Índice

1. [Objetivo del manual](#objetivo-del-manual)
2. [Idea central: por qué preparar datos](#idea-central-por-qué-preparar-datos)
3. [Qué significa tener datos limpios](#qué-significa-tener-datos-limpios)
4. [Power Query: la herramienta principal](#power-query-la-herramienta-principal)
5. [Flujo recomendado de preparación de datos](#flujo-recomendado-de-preparación-de-datos)
6. [Tipos de datos en Power Query](#tipos-de-datos-en-power-query)
7. [Transformaciones estructurales básicas](#transformaciones-estructurales-básicas)
8. [Funciones de vista previa de datos](#funciones-de-vista-previa-de-datos)
9. [Tratamiento de duplicados](#tratamiento-de-duplicados)
10. [Tratamiento de valores vacíos, nulos y faltantes](#tratamiento-de-valores-vacíos-nulos-y-faltantes)
11. [Tratamiento de valores atípicos](#tratamiento-de-valores-atípicos)
12. [Limpieza de columnas de texto](#limpieza-de-columnas-de-texto)
13. [Dividir y combinar columnas](#dividir-y-combinar-columnas)
14. [Transformaciones numéricas](#transformaciones-numéricas)
15. [Transformaciones de fechas](#transformaciones-de-fechas)
16. [Buenas prácticas generales](#buenas-prácticas-generales)
17. [Errores comunes y cómo evitarlos](#errores-comunes-y-cómo-evitarlos)
18. [Checklist final antes de cargar el modelo](#checklist-final-antes-de-cargar-el-modelo)
19. [Resumen para entrevista o portafolio](#resumen-para-entrevista-o-portafolio)

---

## Objetivo del manual

Este manual resume el proceso básico de **preparación de datos en Power BI**, especialmente usando **Power Query**. La idea es tener una guía clara para limpiar, transformar y revisar datos antes de construir visualizaciones, medidas o modelos.

La preparación de datos no consiste solo en “arreglar errores”. También implica entender la estructura del conjunto de datos, decidir qué columnas sirven para el análisis, corregir tipos de datos, detectar duplicados, revisar valores vacíos y transformar columnas para que el modelo sea más confiable.

En términos simples:

> Un buen análisis depende de buenos datos.

Si los datos de entrada están mal, el resultado también puede salir mal, aunque las gráficas se vean bonitas.

---

## Idea central: por qué preparar datos

En análisis de datos existe una frase muy importante:

> Garbage in, garbage out.

Esto significa que si entran datos sucios, incompletos o mal estructurados, el resultado del análisis también será poco confiable.

Preparar datos sirve para:

- Evitar errores en cálculos.
- Evitar conclusiones incorrectas.
- Mejorar el rendimiento del modelo.
- Facilitar la creación de medidas en DAX.
- Hacer que las columnas sean más comprensibles.
- Reducir ruido en el análisis.
- Detectar problemas antes de construir el dashboard.

Ejemplo sencillo:

Si una columna de precios está guardada como texto, Power BI puede no permitir hacer sumas, promedios o medidas correctamente. El dato se ve como número, pero internamente no está siendo tratado como número.

---

## Qué significa tener datos limpios

Un conjunto de datos limpio tiene varias características.

### 1. No tiene valores faltantes sin revisar

Los valores vacíos pueden aparecer como:

- Celdas en blanco.
- `null`.
- Errores.
- Texto como `N/A`, `Sin dato`, `Desconocido`, etc.

No siempre se eliminan. Primero se investigan.

### 2. No tiene errores tipográficos relevantes

Ejemplo:

| Valor incorrecto | Valor correcto |
|---|---|
| `Yelow` | `Yellow` |
| `United  States` | `United States` |
| `Méxcio` | `México` |

Estos errores pueden crear categorías falsas. Para Power BI, `Yellow` y `Yelow` son valores diferentes.

### 3. No tiene duplicados innecesarios

Los duplicados pueden sesgar estadísticas.

Ejemplo: si una película aparece dos veces, puede afectar conteos, promedios o rankings.

Pero no todo valor repetido es un duplicado. Por ejemplo, que varios productos tengan el mismo color no es un error. En cambio, que el mismo `ProductKey` aparezca repetido cuando debería ser único sí puede ser un problema.

### 4. Solo conserva columnas relevantes

No todas las columnas sirven para responder la pregunta del análisis.

Ejemplo: si todos los registros tienen el mismo idioma, la columna `Language` quizá no aporta información para comparar. Se puede eliminar, pero conviene documentarlo.

### 5. Trata los valores atípicos con cuidado

Un valor atípico no siempre es un error.

Ejemplo:

- Una película de 11 horas puede ser rara, pero podría existir.
- Una duración de `-50` minutos claramente no tiene sentido.

La regla es:

> No elimines un valor extremo solo porque se ve raro. Primero pregunta si puede tener sentido en el contexto.

### 6. Usa tipos de datos correctos

Cada columna debe tener el tipo adecuado.

Ejemplos:

| Columna | Tipo recomendado |
|---|---|
| Precio | Decimal fijo o número decimal |
| Fecha de orden | Fecha |
| Nombre de producto | Texto |
| Activo / Inactivo | Lógico |
| Cantidad vendida | Número entero |

### 7. Tiene nombres claros y descriptivos

Los nombres de tablas y columnas deben ser cortos, claros y entendibles.

Ejemplo:

| Malo | Mejor |
|---|---|
| `Column1` | `Product Name` |
| `Cat1` | `Category` |
| `Cat2` | `Subcategory` |
| `StdCost` | `Standard Cost` |

---

## Power Query: la herramienta principal

**Power Query** es la herramienta de Power BI que permite conectar, limpiar y transformar datos antes de cargarlos al modelo.

Power Query funciona como una receta.

Cada cambio que hacemos se guarda como un paso en el panel **Applied Steps**.

Ejemplo de pasos aplicados:

1. Source.
2. Navigation.
3. Promoted Headers.
4. Changed Type.
5. Removed Columns.
6. Replaced Values.
7. Filtered Rows.

Cada paso se ejecuta en orden. Por eso es importante revisar la secuencia: un paso mal ubicado puede afectar los pasos siguientes.

### Idea clave

> En Power Query no solo importa qué transformación haces, también importa en qué orden la haces.

---

## Flujo recomendado de preparación de datos

Un flujo práctico para limpiar datos en Power Query sería:

### Paso 1. Conectar los datos

Desde Power BI:

```text
Home > Get Data
```

Se puede conectar a:

- Excel.
- CSV.
- Web.
- SQL Server.
- Carpetas.
- Bases de datos.
- Otras fuentes.

### Paso 2. Revisar la estructura inicial

Antes de transformar, revisar:

- Si los encabezados están bien.
- Si hay filas basura al inicio.
- Si las columnas están en orden lógico.
- Si hay columnas que no sirven.
- Si los nombres son entendibles.

### Paso 3. Promover encabezados

Cuando la primera fila contiene los nombres reales de las columnas:

```text
Home > Use First Row as Headers
```

Esto convierte la primera fila en encabezados.

### Paso 4. Cambiar tipos de datos

Revisar que cada columna tenga el tipo correcto.

```text
Transform > Data Type
```

Es mejor corregir tipos de datos temprano, pero después de tener encabezados correctos.

### Paso 5. Activar vista previa de datos

Desde:

```text
View > Data Preview
```

Activar:

- Column quality.
- Column distribution.
- Column profile.

Esto ayuda a diagnosticar errores.

### Paso 6. Corregir problemas columna por columna

Revisar:

- Valores nulos.
- Errores.
- Duplicados.
- Valores raros.
- Categorías mal escritas.
- Tipos incorrectos.
- Columnas poco útiles.

### Paso 7. Documentar decisiones importantes

Si eliminas una columna, filtras filas o reemplazas valores, conviene dejar claro por qué.

Esto es especialmente importante si el proyecto va a GitHub.

---

## Tipos de datos en Power Query

Power Query maneja varios tipos de datos. Los más importantes son:

### 1. Números

Sirven para columnas que se usarán en cálculos.

Ejemplos:

- Ventas.
- Costos.
- Precios.
- Cantidades.
- Descuentos.

Tipos comunes:

- Whole Number.
- Decimal Number.
- Fixed Decimal Number.

Para moneda, suele ser recomendable usar **Fixed Decimal Number**, porque evita algunos problemas de precisión decimal.

### 2. Fecha y hora

Sirven para análisis temporal.

Ejemplos:

- Order Date.
- Ship Date.
- Birth Date.
- Transaction Date.

Tipos comunes:

- Date.
- Time.
- Date/Time.

### 3. Texto

Sirve para nombres, categorías, descripciones o identificadores que no se calculan.

Ejemplos:

- Nombre del producto.
- País.
- Ciudad.
- Categoría.
- ID cuando no se va a operar matemáticamente.

### 4. Lógico

Contiene valores tipo verdadero/falso.

Ejemplos:

- Active = true/false.
- IsReturned = true/false.
- HasDiscount = true/false.

### 5. Binario

Se usa para archivos o imágenes, generalmente codificados.

Ejemplo:

- Imágenes cargadas desde una carpeta.
- Archivos en formato binario.

---

## Transformaciones estructurales básicas

Las transformaciones estructurales cambian la organización de la tabla, no necesariamente el significado de los valores.

### Promover encabezados

Se usa cuando la primera fila contiene los nombres de columnas.

```text
Home > Use First Row as Headers
```

### Cambiar orden de columnas

Sirve para organizar la tabla de manera más lógica.

Ejemplo recomendado:

1. Columnas de identificación.
2. Columnas de texto/categorías.
3. Fechas.
4. Columnas numéricas.
5. Métricas calculadas.

### Renombrar columnas

Los nombres deben ser descriptivos.

Ejemplo:

```text
ProductAlternateKey -> Product Key
ProductAlternateNameDescription -> Product Name
```

### Eliminar columnas

Se eliminan columnas que:

- No aportan al análisis.
- Tienen un solo valor y no permiten comparar.
- Están demasiado incompletas.
- Duplican información ya existente.
- No se relacionan con la pregunta de negocio.

Importante:

> Eliminar una columna no debe ser automático. Primero hay que justificarlo.

### Eliminar filas basura

A veces los archivos de Excel tienen filas superiores sin sentido, títulos, notas o información que no pertenece a la tabla.

En ese caso se pueden eliminar filas superiores:

```text
Home > Remove Rows > Remove Top Rows
```

---

## Funciones de vista previa de datos

Las funciones de vista previa ayudan a diagnosticar el estado de las columnas antes de transformar.

Se activan en:

```text
View > Data Preview
```

Las tres principales son:

1. Column Distribution.
2. Column Quality.
3. Column Profile.

### Nota importante sobre las primeras 1000 filas

Power Query puede analizar solo las primeras 1000 filas por defecto. Si el conjunto de datos es grande, eso puede ocultar errores que aparecen después.

Para revisar todo el conjunto de datos, se puede cambiar la opción de perfilado desde la parte inferior de Power Query:

```text
Column profiling based on top 1000 rows
```

Cambiar a:

```text
Column profiling based on entire dataset
```

Esto puede tardar más, pero da una revisión más completa.

---

### Column Distribution

Muestra una pequeña distribución debajo de cada columna.

Sirve para detectar:

- Valores repetidos.
- Cantidad de valores distintos.
- Cantidad de valores únicos.
- Columnas con poca variación.
- Posibles errores de escritura.

#### Diferencia entre valores distintos y únicos

- **Distinct values**: número de valores diferentes que existen en la columna.
- **Unique values**: valores que aparecen una sola vez.

Ejemplo:

| Columna Color |
|---|
| Red |
| Red |
| Blue |
| Green |

Valores distintos: 3 (`Red`, `Blue`, `Green`)  
Valores únicos: 2 (`Blue`, `Green`) porque `Red` aparece más de una vez.

### Column Quality

Muestra la calidad de cada columna.

Sirve para detectar:

- Valores válidos.
- Valores con error.
- Valores vacíos.

Ejemplo:

```text
Valid: 89%
Error: 0%
Empty: 11%
```

Si una columna tiene muchos vacíos, se debe decidir si se rellenan, se eliminan o se dejan como `null`.

### Column Profile

Da un análisis más detallado de una columna específica.

Puede mostrar:

- Promedio.
- Mínimo.
- Máximo.
- Desviación estándar.
- Número de valores distintos.
- Número de valores únicos.
- Distribución de valores.

Es especialmente útil para detectar valores extremos.

Ejemplo:

Si una columna de duración muestra:

```text
Minimum: -50
Maximum: 660
```

Hay que investigar, porque una duración negativa no tiene sentido.

---

## Tratamiento de duplicados

Eliminar duplicados es una de las tareas más delicadas en preparación de datos.

### Cuándo eliminar duplicados

Conviene eliminar duplicados cuando cada fila debería representar una entidad única.

Ejemplos:

| Tabla | Columna que debería ser única |
|---|---|
| Productos | ProductKey |
| Clientes | CustomerKey |
| Películas | Movie Title |
| Pedidos | Order ID |

Si una película debe aparecer una sola vez y aparece repetida, eso probablemente es un duplicado real.

### Cuándo NO eliminar duplicados

No se eliminan duplicados solo porque una columna tiene valores repetidos.

Ejemplo:

| Producto | Color |
|---|---|
| Bicicleta A | Red |
| Bicicleta B | Red |
| Bicicleta C | Blue |

Que `Red` aparezca varias veces no es un error. Es normal que muchos productos tengan el mismo color.

### Cómo eliminar duplicados

Seleccionar la columna clave y usar:

```text
Right click column > Remove Duplicates
```

O:

```text
Home > Remove Rows > Remove Duplicates
```

### Buen uso temporal de Remove Duplicates

A veces se puede usar **Remove Duplicates** como paso temporal para diagnosticar valores distintos.

Ejemplo:

Si sabes que deberían existir 10 colores, pero Power Query muestra 13, puedes:

1. Duplicar mentalmente el análisis, no necesariamente la tabla.
2. Aplicar Remove Duplicates temporalmente sobre `Color`.
3. Ver los valores distintos.
4. Detectar errores como `Yelow` en lugar de `Yellow`.
5. Reemplazar los valores mal escritos.
6. Eliminar el paso temporal de Remove Duplicates.

Esto es importante porque no querías borrar filas reales, solo querías ver las categorías disponibles.

---

## Tratamiento de valores vacíos, nulos y faltantes

Esta parte es central en preparación de datos.

En Power Query, `null` representa un vacío real. No es lo mismo que un espacio en blanco escrito como texto ni que un cero.

### Diferencia entre `null`, blanco, cero y error

| Valor | Qué significa |
|---|---|
| `null` | No hay dato registrado |
| `""` | Texto vacío |
| Espacio `
` | Parece vacío, pero realmente contiene un carácter de espacio |
| `0` | Número cero; puede ser dato válido |
| `Error` | Power Query no pudo interpretar o calcular el valor |

### Regla principal

> Nunca reemplazar valores vacíos sin pensar qué significan.

Rellenar por rellenar puede crear sesgo. A veces es mejor dejar `null` porque es una forma honesta de decir: “este dato no existe o no se conoce”.

---

### ¿Cuándo dejar los valores como `null`?

Conviene dejarlos como `null` cuando:

- El dato realmente no se conoce.
- No hay una forma confiable de inferirlo.
- Reemplazarlo inventaría información.
- Power BI o DAX pueden manejarlo correctamente.
- El vacío tiene significado analítico.

Ejemplo:

Si una columna `Discount` está vacía, no necesariamente significa descuento cero. Podría significar que no se registró el dato. Antes de convertirlo en `0`, se debe revisar el contexto.

Otro ejemplo:

Si `Color` está vacío, poner el color más frecuente puede ser peligroso, porque estaríamos inventando el color del producto.

---

### ¿Cuándo reemplazar `null` por cero?

Solo tiene sentido cuando el cero representa ausencia real de cantidad.

Ejemplos donde podría tener sentido:

- `Discount Amount`: si el negocio confirma que vacío significa que no hubo descuento.
- `Quantity Returned`: si vacío significa que no hubo devoluciones.
- `Shipping Cost`: solo si se confirma que vacío significa envío gratis o costo cero.

No debe hacerse automáticamente.

Ejemplo peligroso:

```text
Precio vacío -> 0
```

Eso casi nunca es correcto, porque un precio de cero puede alterar promedios, mínimos, márgenes y medidas.

---

### ¿Cuándo reemplazar con promedio o mediana?

Puede usarse en columnas numéricas cuando:

- Hay pocos valores faltantes.
- La variable es importante para el análisis.
- El reemplazo no distorsiona demasiado los resultados.
- Se documenta la decisión.

La **mediana** suele ser más segura que el promedio cuando hay valores extremos.

Ejemplo:

Si falta el costo estándar de algunos productos y los costos tienen valores muy extremos, la mediana puede ser una mejor opción que el promedio.

---

### ¿Cuándo reemplazar con la moda?

La moda es el valor más frecuente.

Puede usarse en variables categóricas si:

- Hay pocos faltantes.
- Tiene sentido asumir la categoría más común.
- El análisis no depende fuertemente de esa categoría.

Ejemplo:

Si casi todos los productos son `Color = Black` y unos pocos están vacíos, se podría considerar reemplazar por `Black`, pero solo si el contexto lo justifica.

---

### ¿Cuándo eliminar filas con valores vacíos?

Eliminar filas puede ser válido cuando:

- Son muy pocas filas.
- La columna es esencial para el análisis.
- No se puede recuperar el valor.
- La fila incompleta no sirve para responder la pregunta.
- El modelo no admite `null`.

Ejemplo:

Si una fila no tiene `Customer ID`, `Order Date` ni `Sales Total`, probablemente no sirve para el análisis de ventas.

Pero si una fila solo tiene vacío el campo `Color`, quizá eliminar toda la fila sería demasiado agresivo.

---

### ¿Cuándo usar Fill Down?

**Fill Down** copia el valor anterior hacia abajo para rellenar vacíos.

Se usa cuando los datos vienen en formato de reporte, no en formato de tabla limpia.

Ejemplo:

| ProductKey | Category | Subcategory |
|---|---|---|
| 1 | Bikes | Mountain Bikes |
| 2 | null | null |
| 3 | null | null |
| 4 | Accessories | Helmets |
| 5 | null | null |

Después de Fill Down:

| ProductKey | Category | Subcategory |
|---|---|---|
| 1 | Bikes | Mountain Bikes |
| 2 | Bikes | Mountain Bikes |
| 3 | Bikes | Mountain Bikes |
| 4 | Accessories | Helmets |
| 5 | Accessories | Helmets |

### Por qué el orden importa en Fill Down

Fill Down depende del valor que está arriba. Por eso, si la tabla no está ordenada correctamente, puedes copiar categorías equivocadas.

Ejemplo:

Si se debe rellenar por `ProductKey`, primero se ordena `ProductKey` de forma ascendente. Así Power Query copia el valor correcto hacia las filas que pertenecen al mismo bloque.

Regla:

> Fill Down solo es seguro cuando el orden de la tabla tiene sentido.

---

### Buenas prácticas con valores vacíos

1. Detectar vacíos con **Column Quality**.
2. Filtrar para ver solo filas vacías.
3. Revisar si el vacío significa ausencia, error o dato desconocido.
4. Decidir entre dejar `null`, reemplazar, rellenar o eliminar.
5. Documentar la decisión.
6. Verificar que el porcentaje de vacíos cambió después de la transformación.

---

## Tratamiento de valores atípicos

Los valores atípicos son valores muy diferentes del resto.

Ejemplos:

- Un costo negativo.
- Una duración de película de `-50` minutos.
- Una duración de 11 horas.
- Un precio extremadamente alto.
- Un año como `202` en lugar de `2002`.

### No todos los atípicos son errores

Un valor atípico puede ser:

- Error de captura.
- Dato real pero raro.
- Caso especial importante.
- Señal de fraude.
- Evento extraordinario.

Por eso, antes de eliminarlo hay que interpretarlo.

### Opciones para tratar atípicos

#### 1. Corregir el valor

Si se sabe cuál es el valor correcto.

Ejemplo:

```text
Año 202 -> Año 2002
```

#### 2. Eliminar la fila

Si el valor no tiene sentido y no se puede corregir.

Ejemplo:

```text
Duración = -50 minutos
```

#### 3. Filtrar rangos razonables

Ejemplo:

```text
Conservar películas entre 60 y 240 minutos
```

#### 4. Aplicar piso o techo

También se conoce como **capping**.

Ejemplo:

- Si un valor es menor al mínimo aceptable, se reemplaza por el mínimo.
- Si un valor supera el máximo aceptable, se reemplaza por el máximo.

Esto reduce el efecto de los valores extremos sin eliminar registros.

---

## Limpieza de columnas de texto

Las columnas de texto son propensas a errores porque suelen venir de captura manual o de fuentes externas.

Problemas comunes:

- Errores tipográficos.
- Espacios al inicio o al final.
- Saltos de línea invisibles.
- Mayúsculas y minúsculas inconsistentes.
- Varias formas de escribir lo mismo.
- Columnas con demasiada información mezclada.

### Transformaciones de texto importantes

Se encuentran en:

```text
Transform > Text Column > Format
```

### Trim

Elimina espacios en blanco al inicio y al final.

Ejemplo:

```text
" United States " -> "United States"
```

Es recomendable aplicarlo a casi todas las columnas de texto.

### Clean

Elimina caracteres de control, como saltos de línea o retornos de carro.

Ejemplo:

```text
"United States\n" -> "United States"
```

También conviene aplicarlo a columnas de texto, sobre todo si los datos vienen de web, archivos antiguos o sistemas externos.

### Capitalize Each Word

Convierte el texto a formato de título.

Ejemplo:

```text
"new south wales" -> "New South Wales"
```

Sirve cuando la misma categoría aparece con distinta capitalización.

### Uppercase y Lowercase

Sirven para estandarizar texto.

Ejemplo:

```text
"usa", "USA", "Usa" -> "USA"
```

### Replace Values

Permite reemplazar valores mal escritos.

Ejemplo:

```text
"Yelow" -> "Yellow"
```

Buena práctica:

> Cuando haya muchos errores iguales, es mejor corregirlos en el archivo fuente si es posible.

Esto evita que Power Query reemplace valores que tal vez no debían cambiarse.

---

## Dividir y combinar columnas

Una buena estructura de datos busca que cada columna represente una sola pieza de información.

### Dividir columnas

Conviene dividir una columna cuando contiene demasiada información.

Ejemplo:

```text
Address = "Building 5, Main Street, London, UK"
```

Puede dividirse en:

- Building.
- Street.
- City.
- Country.

Esto facilita filtrar, agrupar y analizar.

En Power Query:

```text
Transform > Split Column > By Delimiter
```

### Combinar columnas

Conviene combinar columnas cuando juntas son más útiles para el análisis o presentación.

Ejemplo:

```text
First Name + Last Name -> Full Name
```

En Power Query:

```text
Transform > Merge Columns
```

Se puede elegir un delimitador, como espacio, coma o guion.

### Ejemplo de corrección de nombre

Si una columna viene como:

```text
Last Name, First Name
```

Se puede:

1. Dividir por coma.
2. Reordenar las columnas.
3. Combinar con espacio.
4. Renombrar como `Full Name`.

---

## Transformaciones numéricas

Las columnas numéricas son clave porque muchas medidas dependen de ellas.

Problemas comunes:

- Números almacenados como texto.
- Valores negativos cuando no tienen sentido.
- Valores extremos.
- Demasiados decimales.
- Unidades poco legibles.
- Valores faltantes.

### Cambiar tipo de dato numérico

Ejemplos:

| Caso | Tipo recomendado |
|---|---|
| Cantidad | Whole Number |
| Precio | Fixed Decimal Number |
| Porcentaje | Decimal Number |
| Costo | Fixed Decimal Number |

### Valor absoluto

Sirve para convertir valores negativos a positivos.

Ejemplo:

```text
-2171.2942 -> 2171.2942
```

Pero debe usarse con cuidado.

No todo número negativo es error. En finanzas, por ejemplo, un número negativo puede representar pérdida, devolución o ajuste.

### Sumar o restar valores a una columna

Puede usarse cuando una regla de negocio se aplica a todas las filas.

Ejemplo:

```text
Sales Total = Sales Total - 1
```

Esto puede representar un impuesto fijo o ajuste aplicado a cada venta.

Importante:

> Si la instrucción dice restar 1, se resta 1 porque esa es la regla definida para el ejercicio. No se asume otro valor.

### Multiplicar o dividir columnas

Sirve para cambiar unidades.

Ejemplo:

```text
Volume / 1,000,000
```

Después conviene renombrar la columna:

```text
Volume -> Volume Millions
```

Así el usuario entiende la escala.

### Redondear números

Redondear ayuda a:

- Reducir tamaño del modelo.
- Mejorar legibilidad.
- Evitar decimales innecesarios.

Ejemplo:

```text
26.3763 -> 26.38
```

### Transformaciones estadísticas

Power Query puede calcular:

- Suma.
- Promedio.
- Mínimo.
- Máximo.
- Desviación estándar.

Pero cuidado:

> Algunas transformaciones estadísticas resumen toda la tabla en un solo número. Son útiles para exploración, pero no siempre deben cargarse al modelo final.

---

## Transformaciones de fechas

Las fechas son un tipo especial de dato. No se tratan igual que una columna numérica normal.

Power Query permite extraer partes de una fecha.

Ejemplos:

- Año.
- Mes.
- Nombre del mes.
- Día.
- Nombre del día.
- Semana del mes.
- Inicio del año.
- Fin del mes.
- Edad a partir de una fecha.

### Buenas prácticas con fechas

#### Duplicar antes de transformar

Si se quiere extraer el nombre del día, conviene duplicar la columna original.

Ejemplo:

```text
Order Date -> Duplicate Column -> Day Name
```

Así no se pierde la fecha original.

#### Usar columnas derivadas para análisis

Ejemplo:

Si una empresa quiere saber qué día se envían más pedidos:

```text
Ship Date -> Name of Day
```

Si quiere saber en qué semana del mes se reciben más órdenes:

```text
Order Date -> Week of Month
```

### Importante

Una columna de fecha original debe conservarse siempre que sea posible, porque sirve para relaciones, calendarios y análisis temporal.

---

## Buenas prácticas generales

### 1. Revisar primero, transformar después

Antes de limpiar, hay que entender el problema.

No conviene eliminar columnas, filas o valores sin revisar su significado.

### 2. Conservar el archivo fuente

Power Query permite transformar sin modificar directamente el archivo original. Eso es útil porque mantiene una fuente limpia y permite repetir el proceso.

Sin embargo, si hay muchos errores de captura en el archivo original, puede ser mejor corregirlos desde la fuente.

### 3. Nombrar bien los pasos aplicados

Si el proyecto es grande, puede ser útil renombrar pasos para que se entienda qué hiciste.

Ejemplo:

```text
Replaced Value -> Corrected Yellow typo
Filtered Rows -> Removed invalid durations
```

### 4. Revisar el orden de los pasos

Un paso puede afectar los siguientes.

Ejemplo:

Si haces Fill Down antes de ordenar correctamente, puedes rellenar valores equivocados.

### 5. No eliminar columnas solo porque “se ven feas”

Primero hay que preguntar:

- ¿Sirve para el análisis?
- ¿Es identificador?
- ¿Ayuda a relacionar tablas?
- ¿Puede ser útil después?

### 6. Documentar decisiones

Para un repositorio de GitHub, es muy buena práctica escribir notas como:

```text
Se eliminó la columna Language porque todos los registros pertenecen al mismo idioma y no aporta variabilidad para el análisis.
```

O:

```text
Se conservaron valores null en la columna Color porque no existe información suficiente para inferir el color real del producto.
```

### 7. Validar después de cada transformación importante

Después de limpiar:

- Revisar Column Quality.
- Revisar Column Distribution.
- Revisar Column Profile.
- Verificar conteo de filas.
- Verificar tipos de datos.

---

## Errores comunes y cómo evitarlos

### Error 1. Reemplazar todos los null por cero

Esto puede distorsionar promedios, sumas y mínimos.

Solución:

Revisar si cero realmente significa ausencia de cantidad.

### Error 2. Eliminar duplicados en la columna equivocada

Si eliminas duplicados por `Color`, puedes borrar productos reales que comparten color.

Solución:

Eliminar duplicados solo usando una columna que debería ser única, como un ID.

### Error 3. No revisar el perfil completo del dataset

Si solo analizas las primeras 1000 filas, podrías no ver errores en filas posteriores.

Solución:

Cuando sea necesario, activar perfilado sobre todo el conjunto de datos.

### Error 4. Cambiar fechas a texto y perder la fecha original

Si conviertes `Order Date` directamente en nombre de mes, pierdes la fecha original.

Solución:

Duplicar la columna antes de extraer texto.

### Error 5. Usar Fill Down sin ordenar

Fill Down copia valores hacia abajo. Si el orden está mal, rellena incorrectamente.

Solución:

Ordenar la tabla según la clave correcta antes de aplicar Fill Down.

### Error 6. Corregir valores sin validar con el negocio

Ejemplo:

```text
-2171 -> 2171
```

Puede ser correcto si era un error de signo, pero también podría representar devolución o pérdida.

Solución:

Revisar contexto antes de aplicar valor absoluto.

---

## Checklist final antes de cargar el modelo

Antes de cerrar Power Query y aplicar los cambios, revisar:

- [ ] Los encabezados están correctos.
- [ ] Los nombres de columnas son claros.
- [ ] Las columnas innecesarias fueron eliminadas con justificación.
- [ ] Los tipos de datos son correctos.
- [ ] Las columnas numéricas no están como texto.
- [ ] Las columnas de fecha están como fecha.
- [ ] Las columnas de moneda usan tipo decimal adecuado.
- [ ] Se revisaron valores vacíos.
- [ ] Se decidió qué hacer con los `null`.
- [ ] Se revisaron duplicados.
- [ ] Se corrigieron errores tipográficos relevantes.
- [ ] Se aplicó Trim y Clean a columnas de texto cuando fue necesario.
- [ ] Se revisaron valores atípicos.
- [ ] Se documentaron filtros importantes.
- [ ] Se verificó el conteo de filas después de eliminar registros.
- [ ] Se revisó el panel de Applied Steps.
- [ ] Se eliminaron pasos temporales de diagnóstico.
- [ ] Se conservó la fecha original si se crearon columnas derivadas.
- [ ] Se renombraron columnas transformadas para indicar unidades o significado.

---

## Resumen para entrevista o portafolio

En este curso practiqué el proceso de preparación de datos en Power BI utilizando Power Query. Aprendí a diagnosticar problemas de calidad mediante Column Distribution, Column Quality y Column Profile, así como a aplicar transformaciones estructurales, de texto, numéricas y de fecha. También reforcé buenas prácticas para tratar valores nulos, duplicados, errores tipográficos y valores atípicos sin modificar los datos de forma automática o injustificada.

La idea principal del proceso es que la limpieza de datos no consiste únicamente en eliminar errores, sino en tomar decisiones razonadas según el contexto del análisis. Una buena preparación permite construir modelos más confiables, medidas más correctas y dashboards más claros.

---

## Mini resumen ejecutivo

La preparación de datos en Power BI consiste en revisar, limpiar y transformar la información antes de analizarla. Power Query permite construir una secuencia de pasos reproducibles para corregir encabezados, tipos de datos, valores vacíos, duplicados, errores de texto, valores extremos, columnas numéricas y fechas. La buena práctica más importante es no transformar datos sin entender su significado: cada eliminación, reemplazo o filtro debe tener una razón clara.

---

## Frases clave para recordar

> Dato limpio, análisis confiable.

> No todo null se rellena.

> No todo duplicado es error.

> No todo valor extremo se elimina.

> Power Query es una receta: cada paso importa.

> Primero diagnosticar, luego transformar.

> Si no sabes qué significa el vacío, no lo inventes.

---

## Posible estructura del repositorio

```text
power-bi-data-preparation-manual/
│
├── README.md
├── manual_data_preparation_power_bi.md
├── images/
│   └── power_query_preview_features.png
├── examples/
│   └── adventureworks_cleaning_notes.md
└── datasets/
    └── README.md
```

---

## Nota personal

Este manual fue elaborado como una compilación de aprendizaje sobre preparación de datos en Power BI. Su objetivo es servir como referencia práctica para futuros proyectos de análisis, especialmente cuando sea necesario limpiar datos antes de construir reportes o dashboards.
