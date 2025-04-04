

## Análisis de Comportamiento de Clientes en Aerolínea 🛫


Este proyecto analiza el comportamiento de clientes de una aerolínea mediante la exploración de dos conjuntos de datos clave:

- Customer Loyalty History: Información demográfica y de fidelización (educación, salario, provincia, tarjeta de lealtad, etc.).

- Customer Flight Activity: Registros de vuelos (distancia, puntos acumulados, reservas mensuales, etc.).

                     **Nota: Aunque la presente descripción es en castellano cabe mencionar que el proyecto posee contenido en inglés debido a que los datos proceden de una aerolínea canadiense. Sin embargo solo observará que el contenido en inglés sólo ocupa a las variables de estudio y encontrará una traducción a las mismas en el mismo documento.


El objetivo es descubrir patrones ocultos, responder preguntas críticas de negocio y optimizar estrategias de fidelización.


Fase 1: EDA (Análisis Exploratorio y Limpieza)

        - Limpieza de datos: Gestión de valores nulos, corrección de formatos y eliminación de duplicados.

        - Análisis por variable: Distribución de salarios, niveles educativos, tipos de tarjetas de fidelidad y actividad geográfica.

        - Integración de DataFrames: Unión de tablas mediante la identificación del cliente para cruzar datos demográficos con actividad de vuelo.


Fase 2: Visualizaciones y Hallazgos Clave

  🔎  Preguntas Respondidas
  
        - Relación distancia vs. puntos acumulados:

            Gráfico de dispersión y líneas para detectar si vuelos más largos generan más fidelización.

        - Distribución geográfica de clientes:

            Gráfico de barras por provincia/estado.

        - Salario promedio por nivel educativo:

            Comparación con gráficos de barras agrupadas.

        - Proporción de tarjetas de fidelidad:

            Gráfico de pastel 

        - Distribución por estado civil y género:
        
            Barras apiladas para analizar diferencias demográficas.


👍 *¿Por qué este proyecto es relevante?*  

            Impacto en negocio: Los insights ayudan a:

                    - Optimizar campañas de marketing dirigidas (ej: ofertas para clientes en provincias clave).

                    - Diseñar programas de fidelización personalizados (ej: beneficios para viajeros frecuentes).

                    - Mejorar la asignación de recursos (ej: rutas con mayor demanda).

    Técnicas aplicadas:

         - Python (pandas, matplotlib, seaborn)
                    
         - Storytelling con datos para comunicar resultados.