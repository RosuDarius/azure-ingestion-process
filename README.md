# Azure Ingestion Process

This project demonstrates a full data ingestion process using **Azure Data Factory** to download, decompress, and store files in **Azure Data Lake Storage**. The data is sourced from **[Rebrickable's dataset downloads](https://rebrickable.com/downloads/)**, which provides LEGO-related datasets in `.csv.gz` (compressed CSV) format. The files are fetched from the external source, processed (decompressed), and saved in a dynamically generated folder structure in **Azure Data Lake**.

## Overview

This project covers the following steps:

1. **External Data Source (Rebrickable)**: Download compressed files (e.g., `.csv.gz`) from Rebrickable's dataset downloads (e.g., `colors.csv.gz`).
2. **Decompression**: Unzip the files from `.gz` to `.csv`.
3. **Dynamic Path Creation**: Store the files in a folder structure dynamically generated from the file name and the ingestion date.
4. **Azure Data Lake Storage**: Store the files in Azure Data Lake for further processing or analysis.

### Data Update Frequency

The data is updated every day at **12:30 PM UTC+2**. You can create triggers in Azure Data Factory to ingest the new data automatically at this specified time.

### Security and Access Control

- **Microsoft Entra ID** is used for identity management.
- A group was created in Microsoft Entra ID, and Azure Data Factory was added to this group with **Storage Blob Contributor** permissions to allow access to Azure Blob Storage.

## Getting Started

### Prerequisites

- Azure Subscription
- Azure Data Factory
- Azure Data Lake Storage

### Steps to Set Up

1. **Create an Azure Data Factory** instance.
2. **Create a linked service** for HTTP to connect to the Rebrickable download URL.
3. **Create a dataset** to specify the file path and format.
4. **Create a pipeline** that includes the following activities:
   - **Copy Activity**: To copy the file from Rebrickable to Azure Blob Storage.
5. **Set up a sink** to store the decompressed `.csv` file in Azure Data Lake Storage.

## Folder Structure

The output files are stored in the following format:
rebrickable/lego/{fileNameWithoutExtension}/{year}/{month}/{day}/
