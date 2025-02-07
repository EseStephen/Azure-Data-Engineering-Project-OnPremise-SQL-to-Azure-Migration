# Azure-Data-Engineering-Project-OnPremise-SQL-to-Azure-Migration
This project demonstrates how to migrate an on-premise SQL Server database to Azure using Azure Data Factory, Datalake, Databricks, Synapse Analytics and Power BI<br>
The primary components used in this project are:<br>
Azure Data Factory (ADF) – Used for data ingestion and orchestration.<br>
Azure Data Lake Gen 2 – Cloud storage for raw and processed data.<br>
Azure Databricks – For data transformation and analytics.<br>
Azure Synapse Analytics – Used for querying and analytics.<br>
Azure Key Vault – Manages secrets and credentials.<br>
Azure Integration Runtime – Facilitates connectivity between on-premise and cloud environments.

Project Resources<br>
A resource group is created in Azure, containing:<br>
Azure Data Factory<br>
Azure Databricks<br>
Azure Key Vault<br>
Azure Storage Account (Data Lake Gen 2)<br>
Azure Synapse Workspace<br>

Data Source<br>
The data source is an on-premise SQL Server database managed in SQL Server Management Studio (SSMS). The database contains multiple tables, but only those with the SalesLT schema are migrated.

Linked Service Configuration
A Linked Service is configured in Azure Data Factory to establish a connection between ADF and the on-premise SQL Server, Azure Databricks for the notebooks and Azure Storage Account (Data Lake Gen 2).

# Ingestion Pipeline in Azure Data Factory<br>
⚙️ Architecture & Components<br>
🗄️ Source: On-Premises SQL Server<br>
Contains multiple tables under the SalesID schema.<br>
📂 Destination: Azure Data Lake Storage (ADLS)<br>
Stores each table as a separate file (CSV or Parquet).<br>

🔄 Pipeline Structure:<br>
Step	Activity	Purpose<br>
1️⃣	Lookup Activity	Fetches all table names from SQL Server.<br>
2️⃣	ForEach Activity	Loops through each table name.<br>
3️⃣	Copy Data Activity	Copies data from SQL Server to Azure Data Lake.<br>

# Data Transformation with Databricks<br>
After loading the tables to the Bronze Layer, Azure Databricks is used for transformation.<br>
Steps:<br>
Compute & Notebook Setup<br>
A Databricks compute instance is created.<br>
Notebooks are created to mount the Bronze, Silver, and Gold containers.<br>

# Bronze to Silver Transformation<br>
Minimal transformations are applied.<br>
Date columns are modified from DateTime to Date.<br>
Data is written to the Silver Layer in Delta format.<br>

# Silver to Gold Transformation<br>
Column names are changed from CamelCase to SnakeCase.<br>
Transformed data is stored in the Gold Layer.<br>
Integration with Data Factory<br>
Databricks notebooks are included in the ADF pipeline.<br>
An access token is stored in Azure Key Vault.<br>
A linked service for Databricks is created in ADF.<br>
Notebooks are executed as part of the ADF pipeline.

# Data Load to Azure Synapse<br>
Connection to Data Lake<br>
Azure Synapse connects to the Gold container in Data Lake Gen 2.<br>
A gold Database is created to store views serverlessly.<br>
A stored procedure is created to generate views for all tables in the Gold Layer.<br>

# Pipeline for View Creation<br>
A linked service is created to connect Synapse to the Gold Database.<br>
A pipeline is configured to execute the stored procedure for every folder in the Gold Layer.<br>

# Power BI Integration<br>
Power BI is connected to Azure Synapse.<br>
Views from the Gold Database are imported into Power BI.<br>
A simple report is created using the processed data.<br>

# Security & Access Control<br>
Azure Key Vault stores database credentials securely.<br>
Managed Identity is used for secure access across Azure resources.<br>
Role-Based Access Control (RBAC) ensures appropriate permissions.<br>

# Conclusion
This project demonstrates an end-to-end data engineering workflow in Azure, covering data ingestion, storage, transformation, and analytics using industry best practices. The implementation ensures efficient data movement, transformation, and reporting within a cloud-based architecture.










