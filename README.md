# Andrés Felipe López Arango PruebaTecnica_2025-03-14 

# Implementación de un Data Warehouse financiero en Azure

## Introducción
Implementar un proceso de integración y centralización de los datos transaccionales diarios de los usuarios de un banco en un entorno de Data Warehouse (DW), con el propósito de facilitar el análisis de negocio y la toma de decisiones estratégicas. Para ello, se utilizaron herramientas y servicios en el entorno de Azure Synapse Analytics, aprovechando un Data Lake para la ingesta y almacenamiento de los datos, y un proceso ETL para la transformación y carga de la información en un modelo optimizado para análisis.

## Arquitectura
Para la integración y centralización de los datos transaccionales, se emplearon diversos servicios de Azure, cada uno seleccionado estratégicamente por sus capacidades y ventajas específicas:
- Azure Data Lake Storage Gen2 (ADLS2): Se utilizó como repositorio principal para la ingesta y almacenamiento de los archivos de origen debido a su capacidad de gestionar datos estructurados, semiestructurados y no estructurados. Su arquitectura escalable y su integración nativa con Synapse permiten un acceso eficiente a los datos transaccionales, facilitando su procesamiento posterior.
- Azure Synapse Analytics: Se encargó de la gestión del Data Warehouse y la ejecución del proceso ETL. Synapse fue seleccionado por su capacidad de escalar horizontalmente, ofrecer un entorno unificado para análisis de datos, y optimizar consultas complejas a través de su motor distribuido, garantizando un alto rendimiento para la generación de reportes y análisis de negocio.
- Pipelines en Synapse: Se implementó un Pipeline para orquestar el flujo de trabajo de forma automatizada, asegurando la reproducibilidad del proceso. Aunque no se programó un Trigger en este ejercicio, se recomienda su configuración para cargas diarias, aplicando un enfoque de carga incremental mediante la identificación de nuevas transacciones a partir de un delta temporal.

A continuación se muestra el diagrama de la arquitectura. 

![Diagrama de Arquitectura](Arquitectura.jpg)

## Ingesta de datos
Para la ingestación de los datos, inicilamente se obtiene un dataset con más de 1millon de filas, para realizar el ejercicio
- Origen: Se almacena los csv en el dataleke en la carpeta RAW, adicionalmente se realiza un proceso inicial para la estructuracion del archivo transacciones.csv y convertilo en .parquet, debido a su peso, facilitando mayor la extracción de los datos posteriormente.
- Destino: Se utilizan la estrategia de tablas externas en synapse, debido a que la utlizacion del motor de polybase permite la extracción y la manipulación de los datos con un rendimiento optimo, por lo que para gran cantidad de datos. Posteriormente transformaciones adecuadas e ingestación de datos en el DW, aplicando la nueva estrcutura que es el modelo estrella.

A continuación se muestra los diagramas de los datos. 

![Datos Transaccionales](Transaccional.jpg)

!Modelo Estrella](ModeloEstrella.jpg)
