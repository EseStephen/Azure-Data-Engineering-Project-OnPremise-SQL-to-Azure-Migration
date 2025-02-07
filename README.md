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



