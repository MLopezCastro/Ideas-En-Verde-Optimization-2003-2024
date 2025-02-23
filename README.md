# Ideas-En-Verde-Optimization-2003-2024
Data analysis and operational sustainability project for Ideas en Verde (2003-2024). This project focuses on optimizing costs and improving efficiency for an indoor gardening business.

# Ideas en Verde Optimization (2003-2024)

This repository contains the data analysis and operational sustainability project for **Ideas en Verde**, a company specializing in indoor gardening for businesses.

## 📊 Objectives
- Analyze historical data (2003-2024) to identify trends and patterns.
- Optimize costs and improve operational efficiency.
- Enhance sustainability through in-house production and plant recovery.

## 🔄 Workflow
1. Consolidate data from multiple Excel files into a SQL Server relational database.
2. Perform exploratory data analysis using Python (pandas, matplotlib).
3. Design interactive dashboards in Power BI to visualize key performance indicators.

## 🛠️ Tools Used
- **Python**: pandas, matplotlib
- **SQL Server**: Database modeling and queries
- **Power BI**: Advanced visualizations and dashboards

## 🌱 Key Metrics
- **REAL/SERV**: Cost of purchased plants to maintain client stocks.
- **VALOR/SERV**: Combined cost of purchased plants and the value of recovered or in-house produced plants.

## 🚀 Results
- Significant reduction in plant replacement rates.
- Identification of new growth opportunities in under-served regions.
- Improved decision-making through dynamic, data-driven dashboards.

-------------------------------------

README - Integración de Datos de 2003-2024 y Análisis en Power BI

📌 Descripción General

Este documento detalla el proceso completo de integración y análisis de datos históricos de reposiciones por cliente desde 2003 hasta 2024. Se explica la transformación de datos desde un archivo CSV inicial hasta su consolidación en SQL Server, su optimización y la integración con Power BI para el análisis visual. También se documentan los problemas encontrados y las soluciones aplicadas.

📂 1. Origen de los Datos

Los datos originales provienen de un archivo CSV con registros de 2003 a 2023, con columnas para cada cliente y sus métricas de costos y servicios. Se recibió un archivo llamado:

tabla_larga_corregida_manual_2024.csv (Incluyendo datos de 2024 y nuevos clientes)

El objetivo era integrar estos datos en una base SQL Server, transformarlos en un formato adecuado para análisis y visualización en Power BI.

🔄 2. Transformación de Datos en SQL Server

2.1. Importación del CSV a SQL Server

Se importó tabla_larga_corregida_manual_2024.csv en SQL Server usando SSMS.

Se configuró Date como DATETIME y las demás columnas como FLOAT, asegurando que los valores nulos se mantuvieran correctamente.

Se creó la tabla:

CREATE TABLE tabla_larga_corregida_manual_2024 (
    Date DATETIME,
    REAL_1 FLOAT,
    REAL_1_SERV_1 FLOAT,
    VALOR_1 FLOAT,
    VALOR_1_SERV_1 FLOAT,
    ... -- (hasta el cliente 68)
);

2.2. Creación de una Copia de Resguardo

Antes de realizar transformaciones, se hizo un backup de la tabla:

SELECT * INTO tabla_larga_cliente_2024_backup FROM tabla_larga_corregida_manual_2024;

2.3. Transformación a Formato "Tabla Larga"

Dado que la tabla importada estaba en formato ancho (cada cliente en una columna), se transformó a formato largo:

SELECT Date,
       Métrica = UNPIVOTED.ColumnName,
       Valor = UNPIVOTED.Value,
       Cliente = 'Cliente ' + CAST(SUBSTRING(UNPIVOTED.ColumnName, CHARINDEX('_', UNPIVOTED.ColumnName) + 1, LEN(UNPIVOTED.ColumnName)) AS VARCHAR)
INTO tabla_larga_cliente_2024
FROM tabla_larga_corregida_manual_2024
UNPIVOT (
    Value FOR ColumnName IN ([REAL_1], [REAL_1_SERV_1], [VALOR_1], [VALOR_1_SERV_1], ... [REAL_68], [VALOR_68_SERV_68])
) AS UNPIVOTED;

⚙️ 3. Ajustes en la Tabla para Power BI

3.1. Eliminación de Columnas No Necesarias

Dado que en el Proyecto 1 solo se usaban REAL_X/SERV_X y VALOR_X/SERV_X, se eliminaron columnas sobrantes:

ALTER TABLE tabla_larga_cliente_2024
DROP COLUMN REAL_1, VALOR_1, REAL_2, VALOR_2, ...;

3.2. Corrección del Formato de Métricas

Se ajustaron los nombres de las métricas para coincidir con Proyecto 1, reemplazando "_" por "/":

UPDATE tabla_larga_cliente_2024
SET Métrica = REPLACE(Métrica, '_', '/');

3.3. Creación de la Columna "NumericPart"

Se extrajo el número de cliente en una nueva columna:

ALTER TABLE tabla_larga_cliente_2024
ADD NumericPart INT;

UPDATE tabla_larga_cliente_2024
SET NumericPart = CAST(SUBSTRING(Cliente, 9, LEN(Cliente)) AS INT);

📊 4. Integración en Power BI

4.1. Conexión de Power BI a SQL Server

Se configuró la conexión de Power BI con la tabla tabla_larga_cliente_2024:

Get Data → SQL Server

Ingresar el servidor y base de datos

Seleccionar la tabla tabla_larga_cliente_2024

Cargar los datos en Power Query

4.2. Ajustes en Power Query

Se eliminaron pasos de "Changed Type" para evitar conversiones erróneas.

Se aplicaron filtros para seleccionar solo las métricas REAL_X/SERV_X y VALOR_X/SERV_X.

Se verificó la correcta representación de valores nulos.

Se creó una relación con otras tablas de métricas.

4.3. Creación del Gráfico en Power BI

Eje X: Date

Valores: REAL_X/SERV_X y VALOR_X/SERV_X

Leyenda: Cliente

Se verificó que los datos fueran consistentes con el Proyecto 1.

🛠️ 5. Problemas y Soluciones

Problema

Solución

Se eliminaron valores nulos en SQL sin querer

Se revisó la estructura y se preservaron los valores originales

Formato incorrecto en los nombres de métricas

Se corrigió con UPDATE tabla SET Métrica = REPLACE(Métrica, '_', '/')

En Power BI los valores se veían como ceros

Se eliminó la transformación de tipo de datos en Power Query

Exceso de decimales en Power BI

Se ajustó el tipo de dato en SQL para mantener precisión adecuada

📌 6. Conclusión y Próximos Pasos

Este documento detalla el flujo completo desde la integración de nuevos datos hasta la visualización en Power BI. Se resolvieron errores en nombres de métricas, problemas de formato y se logró una integración 100% alineada con Proyecto 1.

Próximos pasos:

Optimización de Power BI para que la carga de datos sea más eficiente.

Automatización de la carga de datos en SQL Server con un pipeline de actualización.

Exploración de modelos de predicción para anticipar tendencias en reposiciones.

📂 Referencias

Base de Datos: SQL Server (SSMS)

Visualización: Power BI

Fuente de Datos: tabla_larga_corregida_manual_2024.csv

📌 Última actualización: 2025-02-23



