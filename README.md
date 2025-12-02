# End-to-End Data Engineering Pipeline (CRM Dataset - Mavic Analytics)

This project implements a complete end-to-end **data engineering pipeline** using a CRM dataset provided by **Mavic Analytics**. The pipeline follows a modern data engineering architecture, incorporating on-premise extraction, Azure data services, transformation with Databricks, metadata-driven ingestion, and visualization with Power BI.

---

## 1. On-Premise Data Extraction

The CRM dataset was first extracted **on-premise** and placed into a local folder. This served as the initial source of truth before ingestion into the cloud.

---

## 2. Ingestion Using Azure Data Factory (ADF)

Azure Data Factory was used to **ingest and copy the raw dataset** into Azure Storage.

### Metadata-Driven Ingestion

* A **JSON metadata file** was created to store important information about the incoming CRM file.
* ADF pipelines used this metadata to dynamically copy and ingest the file.
* This metadata-driven pattern ensures automation, flexibility, and reusability.

### ADF Components Used

* Copy Activity
* Linked Services
* Datasets referencing metadata
* Integration Runtime for connectivity

---

## 3. Authentication & Secrets (Service Principal + Key Vault)

* A **Service Principal** was created to authenticate across Azure services.
* **Azure Key Vault** stored sensitive credentials such as client secrets.
* A **secret scope** was created inside **Azure Databricks** to securely access these secrets during transformations.

This ensured the pipeline adhered to best practices in security and secret management.

---

## 4. Data Transformation in Azure Databricks

Using Azure Databricks, the raw ingested CRM data went through necessary cleaning and transformation steps.

### Transformation Highlights

* Standardization and cleaning of columns
* Handling missing or incorrect entries
* Data type corrections
* Business-rule-based transformations

### Storage

* **Raw data** was stored in the **raw container**.
* **Transformed data** was written as **Parquet files** into the **transformed container**, optimizing storage and analytical performance.

---

## 5. Synapse Analytics Integration

Azure Synapse Analytics was connected to the transformed container.

### Work Done in Synapse

* External tables and **views** were created to query the cleaned data.
* These views serve as a semantic layer for downstream analytics tools.

---

## 6. Power BI Visualisation

Power BI was connected to Synapse (via views) to create interactive dashboards.

### KPIs Visualised

* Customer activity trends
* Sales metrics
* CRM engagement analytics
* Additional business insights

---

## 7. Monitoring with Logic Apps & Azure Monitoring

To keep the pipeline reliable, both **Azure Logic Apps** and **Azure Monitoring** were used to track pipeline activity.

### How Monitoring Was Done

* **Azure Monitoring** was used to check pipeline run history, failures, performance, and logs.
* **Logic Apps** sent notifications (email or Teams) whenever an ADF pipeline failed or completed.
* This setup ensured quick visibility and helped maintain data freshness and pipeline health.
