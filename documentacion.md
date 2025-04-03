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
                - *Education* ¿level?: categórica ordinal, es object       # Nivel educativo alcanzado -----> ✅ education_level
                                                                            por el cliente (ej. Bachelor para licenciatura, 
                                                                            College para estudios universitarios o técnicos, etc.)
                - *Salary*: 12499 de 16737, hay datos nulos, es float, ¿$? ¿pasar ',' a '.''         
                                                    # Ingreso anual estimado del cliente ----------> ✅ annual_salary
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
    loyalty_number (tipo int64 / object) 🔗 Clave primaria. Asegurar que está presente.
    country
    province
    city
    postal_code
    gender
    education_level
    annual_salary
    marital_status
    loyalty_card
    clv
    enrollment_type
    enrollment_year
    enrollment_month
    cancellation_year
    cancellation_month