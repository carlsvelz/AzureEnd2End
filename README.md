# Azure Data Platform End2End (V2)

En este taller aprenderá sobre los conceptos principales relacionados con la analítica avanzada y el procesamiento de Big Data y cómo se puede utilizar Azure Data Services para implementar una arquitectura de almacenamiento de datos moderna. Así mismo Aprenderá qué servicios de Azure puede aprovechar para establecer una plataforma de datos sólida para ingerir, procesar y visualizar rápidamente datos de una gran variedad de fuentes de datos. Se ha demostrado que la arquitectura de referencia que creará como parte de este ejercicio le brinda la flexibilidad y escalabilidad para crecer y manejar grandes volúmenes de datos y mantener un nivel óptimo de rendimiento.

En los ejercicios de este laboratorio, creará canalizaciones de datos utilizando datos relacionados con la ciudad de Nueva York. El taller fue diseñado para implementar progresivamente una arquitectura de plataforma de datos moderna extendida a partir de una canalización de datos relacionales tradicional. Luego presentamos escenarios de big data con archivos de datos grandes y computación distribuida. Agregamos datos no estructurados e inteligencia artificial a la mezcla y terminamos con análisis de transmisión en tiempo real. Habrá hecho todo eso al final del taller.

## Workshop Agenda Propuesta
El taller se puede completar a su propio ritmo dependiendo de su experiencia previa con las herramientas de Azure DP. Las diapositivas de apoyo están disponibles para cada formato.

### **1-Día Formato**

#### Slides: [Azure Data Platform End2End - 1 Day](Slides/Azure%20Data%20Platform%20End2End%20-%201Day.pptx)

Actividad | Duración
-------- | ---------
Resumen del taller | 15 minutos
Conceptos de la plataforma de datos moderna: Parte I | 15 minutos
**Almacenamiento de datos moderno** |
Lab 1: Carga de datos en Azure Synapse Analytics mediante Azure Data Factory Pipelines    | 45 minutos
Conceptos de la plataforma de datos moderna: Parte II | 15 minutos
Lab 2: Transformar macrodatos utilizando Azure Data Factory & Mapping Data Flows    | 60 minutos
**Advanced Analytics** |
Conceptos de la plataforma de datos moderna: Parte III | 15 minutes
Lab 3:  Explore Big Data con Azure Databricks    | 45 minutes
Conceptos de la plataforma de datos moderna: Parte IV | 15 minutes
Lab 4: Agregue IA a su Pipeline de Big Data con Cognitive Services    | 75 minutes
**Real-time Analytics** |
Conceptos de la plataforma de datos moderna: Parte V | 15 minutes
Lab 5: Ingesta y analiza datos en tiempo real con Event Hubs y Stream Analytics   | 45 minutes

**IMPORTANT**:

* La arquitectura de referencia propuesta en este taller tiene como objetivo explicar lo suficiente del papel de cada uno de los servicios de datos de Azure incluidos en la arquitectura general de la plataforma de datos moderna. Este taller no reemplaza la necesidad de capacitación en profundidad sobre cada servicio de Azure cubierto.

* Los servicios cubiertos en este curso son solo un subconjunto de una familia mucho más grande de servicios de Azure. Se pueden lograr resultados similares aprovechando otros servicios y / o características que no se cubren en este taller. Los requisitos comerciales específicos pueden requerir el uso de diferentes servicios o características que no se incluyen en este taller.

* Algunos conceptos presentados en este curso pueden ser bastante complejos y es posible que deba buscar más información de diferentes fuentes para complementar su comprensión de los servicios de Azure cubiertos.

![](./Media/ModernDataPlatformReferenceArchitecture.jpg)

### Azure Synapse Analytics

Microsoft anunció recientemente Azure Synapse Analytics como la evolución de Azure SQL Data Warehouse, que combina big data, almacenamiento de datos e integración de datos en un solo servicio para análisis de extremo a extremo a escala de la nube. Esta arquitectura de referencia y el contenido del taller se actualizarán a medida que las características anunciadas en la hoja de ruta estén disponibles públicamente. Para obtener más información, visite: https://azure.microsoft.com/en-au/services/synapse-analytics/

![](./Media/AzureSynapse.png)

## Estructura del documento
Este documento contiene instrucciones detalladas paso a paso sobre cómo implementar una arquitectura de plataforma de datos moderna mediante Azure Data Services. Se recomienda que lea atentamente la descripción detallada contenida en este documento para tener una experiencia exitosa con todos los servicios de Azure. 

Verá la etiqueta IMPORTANTE siempre que haya un paso crítico en el laboratorio. Preste mucha atención a las instrucciones dadas.

También verá la etiqueta IMPORTANTE al comienzo de cada sección de laboratorio. Como algunas instrucciones deben ejecutarse en su computadora host, mientras que otras deben ejecutarse en una conexión de escritorio remoto (RDP), esta etiqueta IMPORTANTE indica dónde debe ejecutar la sección de laboratorio. Vea el ejemplo a continuación:

**IMPORTANTE**|
-------------|
**Ejecute estos pasos en su computadora host**|

## Referencias de fuentes de datos
Los datos de la ciudad de Nueva York utilizados en este laboratorio se obtuvieron del sitio web de datos abiertos de la ciudad de Nueva York: https://opendata.cityofnewyork.us/. Se utilizaron los siguientes conjuntos de datos
    <br>- NYPD Motor Vehicle Collisions: https://data.cityofnewyork.us/Public-Safety/NYPD-Motor-Vehicle-Collisions/h9gi-nx95
    <br>- TLC Yellow Taxi Trip Data: https://www1.nyc.gov/site/tlc/about/tlc-trip-record-data.page

## Implementación y requisitos previos del laboratorio
Se deben completar los siguientes requisitos previos antes de comenzar con estos labs:

* You must be connected to the internet;

* Use either Edge or Chrome when executing the labs. Internet Explorer may have issues when rendering the UI for specific Azure services.

* You must have a Pay-As-You-Go Azure account with administrator- or contributor-level access to your subscription. If you don’t have an account, you can sign up for an account following the instructions here: https://azure.microsoft.com/en-au/pricing/purchase-options/pay-as-you-go/.

    <br>**IMPORTANT**: Azure free subscriptions have quota restrictions that prevent the workshop resources from being deployed successfully. Please use a Pay-As-You-Go subscription instead.

    <br>**IMPORTANT**: When you deploy the lab resources in your own subscription you are responsible for the charges related to the use of the services provisioned. For more information about the list of services and tips on how to save money when executing these labs, please visit the Cost Management section of the [Lab 0: Deploy Azure Data Platform End2End to your subscription](./Deploy/Deploy.md) page.

* Labs 1 to 4 require you to open a Remote Desktop Connection (RDP) to Azure Virtual Machines. If you are using a Mac, please ensure you have the latest version of the Microsoft Remote Desktop software installed: https://apps.apple.com/us/app/microsoft-remote-desktop-10/id1295203466?mt=12

* Lab 5 requires you to have a Power BI Pro account. If you don’t have an account you can sign up for a 60-day trial for free here: https://powerbi.microsoft.com/en-us/power-bi-pro/
  
## Lab Guide

Throughout a series of 5 labs you will progressively implement a modern data platform architecture using datasets from New York City. 

You will start ingesting relational data about motorvehicle collisions in Manhattan hosted in an Azure SQL Database into your Azure Synapse Analytics data warehouse. Then we will introduce the concepts of data lake and  big data challenges and you will put these into practice by ingesting and processing over 50 million yellow taxi ride records stored as large data files stored in your data lake.

You will then use Databricks and the power of Spark clusters to explore big data files. Then you will incorporate AI into your data pipeline by invoking the Cognitive Services Computer Vision API to automatically generate metadata for New York City street photographs and store the metadata in a Cosmos DB database. Finally, you will use a LogicApp to simulate high-frequency stock purchase transactions as a source of streaming events that you will capture, store and process in real time with Event Hubs, Stream Analytics and Power BI.

By the end of the workshop you will have implemented the lab architecture referenced below:

![](./Media/LabArchitecture.jpg)

### [Lab 0: Deploy Azure Data Platform End2End to your subscription](./Deploy/Deploy.md)

**IMPORTANT**: You should skip this Lab if you are executing the labs through subscriptions provided by CloudLabs. All Azure services will be deployed as you activate your registration.

In this section you will automatically provision all Azure resources required to complete labs 1 though to 5. We will use a pre-defined ARM template with the definition of all Azure services used to ingest, store, process and visualise data. 

The estimated time to complete this lab is: **30 minutes**.

**IMPORTANT**|
-------------|
**In order to avoid potential delays caused by issues found during the ARM template deployment it is recommended you execute Lab 0 prior to Day 1.**|

### [Lab 1: Load Data into Azure Synapse Analytics using Azure Data Factory Pipelines](./Lab/Lab1/Lab1.md)

In this lab, the dataset you will use contains data about motor vehicle collisions that happened in New Your City from 2012 to 2019 stored in a relational database. You will configure the Azure environment to allow relational data to be transferred from an Azure SQL Database to an Azure Synapse Analytics data warehouse using Azure Data Factory also staging to Azure Data Lake storage. You will use Power BI to visualise collision data loaded from your Azure Synapse data warehouse.

The estimated time to complete this lab is: **45 minutes**.

Step     | Description
-------- | -----
![1](./Media/Black1.png) | Build an Azure Data Factory Pipeline to copy data from an Azure SQL Database table
![2](./Media/Black2.png) | Use Azure Data Lake Storage Gen2 as a staging area for Polybase
![3](./Media/Black3.png) | Load data to an Azure Synapse Analytics table using Polybase
![4](./Media/Black4.png) | Visualize data from Azure Synapse Analytics using Power BI

![](./Lab/Lab1/Media/Lab1-Image51.png)

### [Lab 2: Transform Big Data using Azure Data Factory Mapping Data Flows](./Lab/Lab2/Lab2.md)
In this lab the dataset you will use contains detailed New York City Yellow Taxi rides for the first half of 2019. You will use Azure Data Factory to download large data files to your data lake. You will generate a daily aggregated summary of all rides from data lake using Mapping Data Flows and save the resulting dataset in your Azure Synapse Analytics. You will use Power BI to visualise summarised taxi ride data.

The estimated time to complete this lab is: **60 minutes**.

 
Step     | Description
-------- | -----
![](./Media/Green1.png) | Build an Azure Data Factory Pipeline to copy big data files from shared Azure Storage
![](./Media/Green2.png) | Ingest data files into your data lake
![](./Media/Green3.png) | Use Mapping Data Flows to generate a aggregated daily summary and save the resulting dataset into your Azure Synapse Analytics data warehouse.
![](./Media/Green4.png) | Visualize data from your Azure Synapse Analytics using Power BI

![](./Lab/Lab2/Media/Lab2-Image40.png)

### [Lab 3: Explore Big Data using Azure Databricks](./Lab/Lab3/Lab3.md)
In this lab you will use Azure Databricks to explore the New York Taxi data files you saved in your data lake in Lab 2. Using a Databricks notebook you will connect to the data lake and query taxi ride details for data cleasning and to apply standard column definitions for the resulting dataset. At the completion,  The resulting dataset should be saved in a Spark table using Parquet files sitting in the NYCTaxiData-Curated container in your SynapseDataLake storage account.

The estimated time to complete this lab is: **45 minutes**.

Step     | Description
-------- | -----
![](./Media/Red1.png) |Build an Azure Databricks notebook to explore the data files you saved in your data lake in the previous exercise. You will use Python and SQL commands to open a connection to your data lake and query data from data files.
![](./Media/Red2.png) |Integrate datasets from Azure Synapse Analytics data warehouse to your big data processing pipeline. Databricks becomes the bridge between your relational and non-relational data stores.

![](./Lab/Lab3/Media/Lab3-Image14.png)

### [Lab 4: Add AI to your Big Data Pipeline with Cognitive Services](./Lab/Lab4/Lab4.md)
In this lab you will use Azure Data Factory to download New York City images to your data lake. Then, as part of the same pipeline, you are going to use an Azure Databricks notebook to invoke Computer Vision Cognitive Service to generate metadata documents and save them in back in your data lake. The Azure Data Factory pipeline then finishes by saving all metadata information in a Cosmos DB collection. You will use Power BI to visualise NYC images and their AI-generated metadata.

The estimated time to complete this lab is: **75 minutes**.

Step     | Description
-------- | -----
![](./Media/Blue1.png) | Build an Azure Data Factory Pipeline to copy image files from shared Azure Storage
![](./Media/Blue2.png) | Save image files to your data lake
![](./Media/Blue3.png) | For each image in your data lake, invoke an Azure Databricks notebook that will take the image URL as parameter
![](./Media/Blue4.png) | For each image call the Azure Computer Vision Cognitive service to generate image metadata. Metadata files are saved back in your data lake
![](./Media/Blue5.png) | Copy metadata JSON documents into your Cosmos DB database
![](./Media/Blue6.png) | Visualize images and associated metadata using Power BI

![](./Lab/Lab4/Media/Lab4-Image70.png)

### [Lab 5: Ingest and Analyse real-time data with Event Hubs and Stream Analytics](./Lab/Lab5/Lab5.md)
In this lab you will use an Azure Logic App to simulate a NYSE stream of stock purchase transactions. The logic app will then send the messages to Event Hubs. You will then use Stream Analytics to receive and process the stream and perform aggregations to calculate the number of transactions and amount traded in the last 10 seconds. Stream Analytics will send the results to a real-time dataset in Power BI.

The estimated time to complete this lab is: **45 minutes**.

Step     | Description
-------- | -----
![](./Media/Orange1.png) | Review the Azure Logic App logic that simmulates the NYSE transaction stream sent to EventHubs
![](./Media/Orange2.png) | Save simulated NYSE stock transaction messages into your data lake for future analysis (cold path)
![](./Media/Orange3.png) | Send stream of NYSE stock transaction messages to Stream Analytics for real-time analytics (hot path)
![](./Media/Orange4.png) | Incorporate Stock Company reference data into your stream processing logic
![](./Media/Orange5.png) | Visualize real-time data generated by Stream Analytics with Power BI

![](./Lab/Lab5/Media/Lab5-Image66.png)
