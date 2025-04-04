## ✈️ Análisis de Clientes y Vuelos de la Aerolínea  

## Objetivo  
En este análisis exploraremos los datos de clientes inscritos en una membresía de aerolínea y sus vuelos.  Realizaremos limpieza, visualización y evaluación de los datos para obtener insights relevantes.  

  -  Preparación de Datos: Filtra el conjunto de datos para incluir únicamente las columnas relevantes:'Flights Booked' y 'Education'.
  -  Análisis Descriptivo: Agrupa los datos por nivel educativo y calcula estadísticas descriptivas
        básicas (como el promedio, la desviación estándar) del número de vuelos reservados para cada
        grupo.
  -  Prueba Estadística: Realiza una prueba de hipótesis para determinar si existe una diferencia
        significativa en el número de vuelos reservados entre los diferentes niveles educativos.



Tras importar los archivos .csv y abrirlos podemos obtener información de las variables a través del método .shape y .info() aplicado en cada dataset.
Queremos encontrar problemas en los datos: valores nulos, anormales, falta de datos, ...

*Parece que tenemos más filas en la segunda data en comparación con los clientes. Probablemente cada cliente se identificará en varias filas del dataset de la información de vuelos.*

df_loyalty: Tenemos en df_loyalty (información de clientes): 16737 filas y 15 columnas
            Datos a destacar: 
            *  Las columnas necesitan ponerse en minúsculas, sin espacios y con '_'
         *****  - *Loyalty Number*: no aparece nombrada como columna ----------> ✅ loyalty_number 
                     Identificador único del cliente dentro del programa de lealtad.
                    Este número permite correlacionar la información de este archivo con el archivo de actividad de vuelos.
                - *Country*: es object ----------> ✅ country
                - *Province*: es object:         # Provincia o estado de residencia del cliente ----------> ✅ province
                                            (aplicable a países con divisiones provinciales
                                            o estatales, como Canadá)
                - *City*: es object ----------> ✅ city
                - *Postal*: Code es object ¿dejar? ----------> ✅ postal_code
                - *Gender*: ¿hacer .map()?, es object        # Male: masculino y Female: femenino ----------> ✅ gender
                - *Education* ¿level?: categórica ordinal, es object       # Nivel educativo alcanzado -----> ✅ education                                               por el                                                              (ej. Bachelor para licenciatura, College para estudios universitarios o técnicos, etc.)
                - *Salary*: 12499 de 16737, hay datos nulos, es float, ¿$? ¿pasar ',' a '.''         
                                                    # Ingreso anual estimado del cliente ----------> ✅ salary
                - *Marital Status*: object, revisar .unique()   ----------> ✅ marital_status  
                                                    # Estado civil del cliente (ej. Single para soltero, 
                                                    Married para casado, Divorced para divorciado, etc.)
                - *Loyalty Card*: ¿qué es? inspeccionar, es object  ----------> ✅ loyalty_card
                                                    # Tipo de tarjeta de lealtad que posee el cliente. 
                                                    Esto podría indicar distintos niveles o categorías dentro del programa de lealtad
                - *CLV*: ¿qué es? inspeccionar, es float    ----------> ✅ clv   
                                                    # 'Customer Lifetime Value', Valor total estimado que el cliente aporta a
                                                    la empresa durante toda la relación que mantiene con ella
                - *Enrollment Type*: ¿qué es? inspeccionar, es object       ----------> ✅ enrollment_type
                                                    # Tipo de inscripción del cliente en el programa de lealtad (ej. Standard)
                - *Enrollment Year*: ¿qué es? inspeccionar, es int    ----------> ✅ enrollment_year      
                                                    #   Año en que el cliente se inscribió en el programa de lealtad.
                - *Enrollment Month*: ¿qué es? inspeccionar, es int   ----------> ✅ enrollment_month
                                                    #   Mes en que el cliente se inscribió en el programa de lealtad
                - *Cancellation Year*: sólo tiene 2067 valores, es float    ----------> ✅ cancellation_year
                                                    #   Año en que el cliente canceló su membresía en el programa de lealtad, si aplica
                - *Cancellation Month*: sólo tiene 2067 valores, es float   ----------> ✅ cancellation_month
                                                    #   Mes en que el cliente canceló su membresía en el programa de lealtad, si aplica.


df_flight:  Tenemos en df_flight (información de vuelos de clientes): 405624 filas y 9 columnas.
            Datos a destacar:
             *  Las columnas necesitan ponerse en minúsculas, sin espacios y con '_'
        *****   - *Loyalty Number*: no aparece nombrada como columna ----------> ✅ loyalty_number 
                        Este atributo representa un identificador único para cada cliente dentro del
                        programa de lealtad de la aerolínea. Cada número de lealtad corresponde a un cliente específico.                  
                - *Year*: es int     ----------> ✅ year     # Año en el cual se registraron las actividades de vuelo para el cliente
                - *Month*: es int    ----------> ✅ month    # Mes del año (de 1 a 12) en el cual ocurrieron las actividades de vuelo.
                - *Flights Booked*: es int   ----------> ✅ flights_booked         # Número total de vuelos reservados por el cliente
                                                                                     en ese mes específico
                - *Flights with Companions*: es int    ----------> ✅ flight_with_companions
                                                            # Número de vuelos reservados - el cliente viajó con acompañantes
                - *Total Flights*: es int           ----------> ✅ total_flights 
                            # Número total de vuelos que el cliente ha realizado, puede incluir vuelos reservados en meses anteriores
                - *Distance*: es int          ----------> ✅ distance
                                            # Distancia total (millas o kilómetros) que el cliente ha volado durante el mes
                - *Points Accumulated*: es float ----------> ✅ points_accumulated
                                                # Puntos acumulados por el cliente en el programa de lealtad durante el mes,
                                                    con base en la distancia volada u otros factores.
                - *Points Redeemed*: es int      ----------> ✅ points_redeemed
                                                # Puntos que el cliente ha redimido en el mes, posiblemente para obtener
                                                beneficios como vuelos gratis, mejoras, etc
                - *Dollar Cost Points Redeemed*: es int     ----------> ✅ dollar_cost_points_redeemed
                                                # Valor en dólares de los puntos que el cliente ha redimido durante el mes


## 1. Cambios a realizar
    ## df_loyalty
    - loyalty_number (tipo int) 🔗 Clave primaria. Asegurar que está presente (no index_col = 0)
    - country (tipo object) ⚙️ Estandarizar nombres de países.
    - province (tipo object) ⚙️ Mantener si es útil para análisis regional.
    - city (tipo object) ⚙️ Mantener si es útil. Se puede agrupar por ciudad para análisis.
    - postal_code (tipo object) ⚙️ Depende del análisis. Puede eliminarse si no se usa.
    - gender  (tipo object) ⚙️ Usar .map() para convertirlo en categoría (M/F).
    - education (tipo object) ⚙️ Convertir a variable categórica ordinal (High School < College < Bachelor < Master < PhD).
    - salary (tipo float) ⚙️ Manejo de nulos: Imputación con la mediana. Convertir ',' en '.' si es necesario.
    - marital_status (tipo object) ⚙️ Revisar .unique() para estandarizar categorías.
    - loyalty_card (tipo object) ⚙️ Inspeccionar si afecta el análisis. Si tiene niveles, convertir a ordinal (Bronze < Silver < Gold).
    - clv (tipo float) ⚙️ Importante para segmentación (Clientes de alto valor vs. bajo valor). Revisar .unique() para estandarizar 
    - enrollment_type (tipo object) ⚙️ Tipo de inscripción al programa de lealtad. Revisar si tiene impacto en la retención de clientes.
    - enrollment_year (tipo int) ⚙️ Útil para analizar fidelización (Clientes antiguos vs. nuevos).
    - enrollment_month (tipo int) ⚙️ Combinable con enrollment_year para ver tendencias.
    - cancellation_year (tipo float) ⚙️ Solo 2067 valores. Revisar si impacta el análisis. Puede tratarse como categórica (canceló/no canceló).
    - cancellation_month (tipo float) Puede combinarse con cancellation_year para ver patrones de cancelación.

    ## df_flight
    - loyalty_number (tipo int / object) 🔗 Clave primaria. Debe coincidir con df_loyalty para hacer **merge()**.
    - year (tipo int) Año del vuelo registrado. Puede usarse para analizar tendencias anuales.
    - month (tipo int) Mes en que ocurrió el vuelo. Combinable con year para ver estacionalidad.
    - flights_booked (tipo int) Total de vuelos reservados en el mes.  Importante para **analizar patrones de compra.**
    - flights_with_companions (tipo int) Puede indicar clientes que viajan en grupo.
    - total_flights (tipo int) Clave para segmentar clientes frecuentes.
    - distance (tipo int **pasar a float?**) Distancia total volada en el mes. Convertir a unidades consistentes (millas o km).
    - **points_accumulated** (tipo  float) Revisar relación con distancia volada.
    - **points_redeemed** (tipo int) Puede indicar clientes más activos en el programa por los puntos canjeados.
    - dollar_cost_points_redeemed (tipo int) Útil para analizar el valor real del programa de lealtad.

### 1.1 Limpieza 
- loyalty_number: Asegurarse de que sea único y esté presente en ambos datasets.

    **df_loyalty:** 
    Análisis exploratorio
    - "Salary" tiene 16737 filas y 12499 valores, hay datos nulos, es float ✅
    - Comparar year y month para ver cual eliminar
    - Analizar patrones de compra según flights_booked (mediana ... hacer gráfica)

    Limpieza
    - Cambiar distance de int a float
    - Renombrar columnas
    - Gestión de valores nulos en annual_salary, cancellation_year y cancellation_month

    Análisis estadístico
    - ¿Afecta la distancia de los vuelos que se recorren a los puntos?
    - ¿En qué año se han registrado más vuelos o más reservas?
    - ¿Los clientes que viajan en grupo tienen más puntos acumulados o canjeados? Hipótesis


**df_flight:** 
Análisis exploratorio
- Comparar year y month para ver cual eliminar
- Analizar patrones de compra según flights_booked (mediana ... hacer gráfica)

Limpieza
- Cambiar distance de int a float
- Renombrar columnas
- Gestión de valores nulos en annual_salary, cancellation_year y cancellation_month

Análisis estadístico
- ¿Afecta la distancia de los vuelos que se recorren a los puntos?
- ¿En qué año se han registrado más vuelos o más reservas?
- ¿Los clientes que viajan en grupo tienen más puntos acumulados o canjeados? Hipótesis



Al finalizar la limpieza de los datos, se guardarán en un nuevo archivo .csv para su posterior análisis.




Notas de tratamiento de datos:
- Hemos cambiado los nombres de las columnas para que sean más descriptivos y fáciles de entender. Por ejemplo, `loyalty_number` se convertió en `loyalty_id`, `Enrollment Month` se convertió en `enrollment_month`, etc.

**df_loyalty:** 

Análisis exploratorio

*Valores numéricos, int y float*:
- Int:
    - loyalty_id ✅ 
    - salary ✅
    - clv ✅ - valores únicos, estandarizar, es el valor que el cliente ha generado para la empresa, ¿es un valor monetario? ¿es un porcentaje?  
    - enrollment_year ✅ - analizar fidelización, clientes antiguos vs nuevos 
    - enrollment_month ✅ - combinar con enrollment_year para ver patrón de compra, enrollment = inscripción
    - cancellation_year ❌  solo tiene 2067 valores, ¿ % ? ¿eliminar? ¿categorizar?
    - cancellation_month ❌  ver patrones de cancelación ¿combinar con cancellation_year? ¿ % ? ¿eliminar? 

*Valores categóricos*:
- Nominales: object 
    - country - ¿estandarizar? ❌
    - province ✅ - ¿útil? 
    - city  ✅ - # Hacer groupby para ver si hay provincias con más de una ciudad 
           df.groupby(['province', 'city']).size()
    - postal_code  ✅ - ¿eliminar? ¿pasar a int?
    - gender ✅ - ¿convertir con map?
    - marital_status ✅ - ver valores únicos

- Ordinales: Object
    - education ✅ - es un level, ¿convertir con map?
    - loyalty_card ✅ - inspeccionar valores únicos ¿orden?
    - enrollment_type ✅ - tipo de membresía, ¿convertir con map? 
Limpieza
- Gestión de valores nulos en _salary, cancellation_year y cancellation_month


**df_flights:**

Análisis exploratorio

*Valores numéricos, int y float*:
- loyalty_id - ✅
- year - ✅   analizar registros de vuelos anuales
- month - ✅  es de cada vuelo, comparar year y month para ver cual eliminar, estadística de vuelos por mes, ¿hay meses con más vuelos? ¿hay meses con más cancelaciones?
- flights_booked - ✅ vuelos reservados en el mes, analizar patrones de compra con estadística
- flights_with_companions - ✅  ¿se acumulan más puntos? ¿se cancelan más vuelos?
- total_flights - ✅ vuelos totales por cliente
- distance -  ✅  es int ¿pasar a float? si dist., volada en el mes, convertir a millas o km
- points_accumulated - ✅  float, ¿pasar a int? no, relacionar con loyalty_id, ¿se acumulan más puntos viajando solo o en grupo?
- points_redeemed -✅ int, puntos canjeados, actividad de clientes
- dollar_cost_points_redeemed ✅  - int, ¿pasar a float? si, ¿$ quitar? relacionado con points_redeemed, valor en dólares de puntos ya canjeados durante el mes

Limpieza
- Cambiar distance de int a float 1 decimal
- Cambiar dollar_cost_points_redeemed a float 1 decimal

Unión de los datasets
- Unir los datasets por loyalty_id, asegurando que los datos estén alineados correctamente y que no haya duplicados o pérdidas de información.
- Verificar que la unión se haya realizado correctamente y que los datos estén completos y listos para el análisis posterior.

Análisis estadísticos
- ¿Afecta la distancia de los vuelos que se recorren a los puntos?
- ¿Hay meses con más vuelos? ¿hay meses con más cancelaciones?
- ¿En qué año se han registrado más vuelos o más reservas?
- Patrones de compra de clientes
- ¿Los clientes que viajan en grupo tienen más puntos acumulados o canjeados? 


**Métodos interesantes**

df_unido.drop(columns=["supermarket"], inplace=True)
df_unido.head()
df_unido.info()
df_unido.shape

isin(): seleccionar filas que contienen valores específicos en una columna. Un valor 
o lista de valores 
df[‘columna’].isin(valores) 
1. Crear filtro: filtro = [‘valor1’, ‘valor2’] 
2. Aplicar filtro df_nuevo = df[df[‘columna’].isin(filtro)] 
3. df_nuevo es igual pero con las filas que contienen los valores del filtro

between(): filtrar por un rango 
nuevo_df = df[df[‘columna’].between(inicio, fin, inclusive=both/left/right/neither)] 
• both: incluye los valores de inicio y fin 
• left: incluye inicio pero no fin 
• right: incluye fin pero no inicio 
• neither: no incluye ni inicio ni fin 

str.contains(): filtrar por palabras. Devuelve un booleano. 
df[‘columna’].str.contains(pat, case=True, na=nan, regex=True) 
• pat: patrón de texto a buscar 
• case: (op) True distingue mayúsculas y minúsculas 
• na=nan: (op) 
• regex: (op) True se interpreta como regex 

.reset_index(): nuevo DataFrame del resultado con índice en 0 
df.groupby(columna)[columna_operacion].operacion(numeric_only=True):  aplica 
la operación a todas columnas numéricas 
variable_agrupacion.ngroups: grupos formados después de la agrupación

 
.replace(): reemplaza valores en un DataFrame o Serie por otros especificados 
Sintaxis: 
df[‘col’] = df[‘col’].replace(valor a reemplazar, nuevo valor) 
Se utiliza para reemplazar un valor concreto de esa columna, no todos 

## Análisis en Visualizaciones

1. ¿Cómo se distribuye la cantidad de vuelos reservados por mes durante el año? 

Relación de variables flights_booked con points_accumulated: 


2. ¿Existe una relación entre la distancia de los vuelos y los puntos acumulados por los cliente?

Relación de variables province con loyalty_id

3. ¿Cuál es la distribución de los clientes por provincia o estado?

Relación de variables loyalty_id y province

4. . ¿Cómo se compara el salario promedio entre los diferentes niveles educativos de los clientes?

Relación de variables salary y education_level

5. ¿Cuál es la proporción de clientes con diferentes tipos de tarjetas de fidelidad?

Relación de variables loyalty_card y loyalty_id

6. ¿Cómo se distribuyen los clientes según su estado civil y género?

Relación de variables marital_status y gender