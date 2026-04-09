# 📊 AWS Data Engineering: Pipeline de Extracción y Consulta (Glue & Athena)

Este laboratorio documenta mi proceso de creación de un entorno de analítica moderna. Implementé un flujo de datos que va desde el almacenamiento de archivos crudos hasta la ejecución de consultas de inteligencia de negocios mediante SQL.



## 🏗️ 1. Fase de Almacenamiento: S3 Data Lake
Cargué los datos de origen en un bucket de **Amazon S3** llamado `bucket-dianalab-analitica`. Organizé la información en carpetas separadas para asegurar un rastreo eficiente por parte del Crawler. 

> **Evidencias de S3:**
> ![Estructura del Bucket](./img/S3_Bucket_Root.png)
> ![Archivo de Productos](./img/S3_Products_File.png)
> ![Archivo de Ventas](./img/S3_Sales_File.png)

---

## 🤖 2. Fase de Catalogación: AWS Glue
Utilicé **AWS Glue** para automatizar el descubrimiento de la estructura de los datos.

### 2.1. Configuración del Crawler
Configuré un **Crawler** llamado `crawler diana` con la descripción: *"Identificar la estructura de fuente de datos del Bucket de origen"*. Definí el S3 path y configuré el rastreo de todas las subcarpetas.

> **Evidencias del Crawler:**
> ![Mapeo de Datos](./img/Glue_Crawler_Config.png)
> ![Configuración Crawler](./img/Glue_Data_source.png)
> ![Configuración de Salida](./img/Glue_Output_DB.png)
> ![Resumen de Configuración](./img/Glue_Review.png)
> ![Crawler Listo](./img/Glue_Crawler_Ready.png)

### 2.2. Data Catalog y Metadatos
Tras la ejecución, el catálogo de datos de Glue se alimentó con dos tablas: `products` y `sales`. El Crawler identificó automáticamente los tipos de datos para cada columna. 

> **Evidencias del Catálogo:**
> ![Tablas en Glue](./img/Glue_Tables_Created.png)
> ![Esquema de Productos](./img/Glue_Schema_Products.png)
> ![Esquema de Ventas](./img/Glue_Schema_Sales.png)

---

## 🔍 3.  Análisis con Amazon Athena
Con los datos catalogados, utilicé **Amazon Athena** como motor de consultas SQL sobre S3. 

1. **Configuración:** Definí el bucket de S3 para depositar los resultados de las consultas.
2. **Validación:** Realicé un `Preview Table` para confirmar la integridad de los datos cargados. 
3. **Análisis Avanzado:** Ejecuté un `JOIN` entre ambas tablas para obtener métricas de ingresos por nombre de producto.

> **Evidencias de Consulta:**
> ![Configuración de Query](./img/Athena_Settings.png)
> ![Previsualización de Datos](./img/Athena_Preview.png)
> ![Análisis de Ingresos Totales](./img/Athena_Complex_Query.png)

---
## 📝 Conclusiones 

* **Arquitectura Serverless:** Aprendí que es posible procesar y analizar grandes volúmenes de datos pagando únicamente por las consultas realizadas, eliminando costos de mantenimiento de servidores.
* **Automatización de Esquemas:** AWS Glue me permitió ahorrar tiempo crítico al inferir automáticamente la estructura de los archivos CSV, gestionando los metadatos de forma centralizada.
* **SQL sobre Archivos Planos:** Con Amazon Athena logré aplicar mis conocimientos de SQL directamente sobre S3, permitiendo realizar uniones y agrupaciones complejas entre tablas de manera ágil.
* **Escalabilidad:** Esta solución es ideal para un Data Lake, ya que permite que los datos crezcan en S3 mientras el catálogo de Glue se mantiene actualizado para análisis inmediatos.
