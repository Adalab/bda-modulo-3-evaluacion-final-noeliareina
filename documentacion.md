## ✈️ Análisis de Clientes y Vuelos de la Aerolínea  

## Objetivo  
En este análisis exploraremos los datos de clientes inscritos en una membresía de aerolínea y sus vuelos.  Realizaremos limpieza, visualización y evaluación de los datos para obtener insights relevantes.  

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
                - *Education* ¿level?: categórica ordinal, es object       # Nivel educativo alcanzado -----> ✅ education                                               por el                                                              (ej. Bachelor para licenciatura, 
                                                                            College para estudios universitarios o técnicos, etc.)
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
    - loyalty_number (tipo int / object) 🔗 Clave primaria. Asegurar que está presente.
    - country (tipo object) ⚙️ Estandarizar nombres de países.
    - province (tipo object) ⚙️ Mantener si es útil para análisis regional.
    - city (tipo object) ⚙️ Mantener si es útil. Se puede agrupar por ciudad para análisis.
    - postal_code (tipo object) ⚙️ Depende del análisis. Puede eliminarse si no se usa.
    - gender  (tipo object) ⚙️ Usar .map() para convertirlo en categoría (M/F).
    - education (tipo object) ⚙️ Convertir a variable categórica  ordinal (High School < College < Bachelor < Master < PhD).
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

