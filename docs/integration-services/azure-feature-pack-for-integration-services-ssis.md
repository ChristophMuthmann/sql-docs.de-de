---
title: "Azure FeaturePack für Integrationsservices (SSIS) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 08/22/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.SSIS.AZURE.F1
- SQL14.SSIS.AZURE.F1
ms.assetid: 31de555f-ae62-4f2f-a6a6-77fea1fa8189
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 4941d8eb846e9d47b008447fe0e346d43de5d87f
ms.openlocfilehash: d4204ba56e515025bed3ae3bf8e7a77d6da471be
ms.contentlocale: de-de
ms.lasthandoff: 08/30/2017

---
# <a name="azure-feature-pack-for-integration-services-ssis"></a>Azure Feature Pack für Integration Services (SSIS)
SQL Server Integration Services (SSIS) Feature Pack für Azure ist eine Erweiterung, die die aufgeführten Komponenten auf dieser Seite für die SSIS zur Verbindung mit Azure-Dienste, Daten zwischen Azure und lokalen Datenquellen und Verarbeitung von Daten in Azure gespeicherten bereitstellt.

[![Herunterladen von SSIS-Feature Pack für Azure](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/download/details.aspx?id=54798) **herunterladen**

- Für SQLServer 2017 - [Microsoft SQL Server 2017 Integration Services FeaturePack für Azure](https://www.microsoft.com/download/details.aspx?id=54798)
- Für SQLServer 2016 - [Microsoft SQL Server 2016 Integration Services FeaturePack für Azure](https://www.microsoft.com/download/details.aspx?id=49492)
- Für SQLServer 2014 - [Microsoft SQL Server 2014 Integration Services FeaturePack für Azure](https://www.microsoft.com/en-us/download/details.aspx?id=47366)
- Für SQLServer 2012 - [Microsoft SQL Server 2012 Integration Services FeaturePack für Azure](https://www.microsoft.com/en-us/download/details.aspx?id=47367)

## <a name="components-in-the-feature-pack"></a>Komponenten im Feature Pack
-   Verbindungs-Manager

    -   [Azure Storage-Verbindungs-Manager](../integration-services/connection-manager/azure-storage-connection-manager.md)

    -   [Azure-Abonnementverbindungs-Manager](../integration-services/connection-manager/azure-subscription-connection-manager.md)
    
    -   [Azure Data Lake Store Connection Manager (Azure Data Lake Store-Verbindungs-Manager)](../integration-services/connection-manager/azure-data-lake-store-connection-manager.md)
    
    -   [Azure Resource Manager-Verbindungs-Manager](../integration-services/connection-manager/azure-resource-manager-connection-manager.md)
    
    -   [Azure HDInsight-Verbindungs-Manager](../integration-services/connection-manager/azure-hdinsight-connection-manager.md)

-   Aufgaben

    -   [Azure-Blob-Uploadtask](../integration-services/control-flow/azure-blob-upload-task.md)

    -   [Azure Blob-Download-Task](../integration-services/control-flow/azure-blob-download-task.md)

    -   [Azure HDInsight Hive-Task](../integration-services/control-flow/azure-hdinsight-hive-task.md)

    -   [Azure HDInsight Pig-Task](../integration-services/control-flow/azure-hdinsight-pig-task.md)

    -   [Azure HDInsight Create Cluster-Task](../integration-services/control-flow/azure-hdinsight-create-cluster-task.md)

    -   [Azure HDInsight-Delete Cluster-Task](../integration-services/control-flow/azure-hdinsight-delete-cluster-task.md)
    
    -   [Azure SQL DW-Uploadtask](../integration-services/control-flow/azure-sql-dw-upload-task.md)

    -   [Azure Data Lake-Speicher-Dateisystemtask](../integration-services/control-flow/azure-data-lake-store-file-system-task.md)

-   Datenflusskomponenten

    -   [Azure-Blob-Quelle](../integration-services/data-flow/azure-blob-source.md)

    -   [Azure-BLOB-Ziel](../integration-services/data-flow/azure-blob-destination.md)
    
    -   [Azure Data Lake Store Source](../integration-services/data-flow/azure-data-lake-store-source.md)
    
    -   [Azure Data Lake Store Destination](../integration-services/data-flow/azure-data-lake-store-destination.md)

-   Azure-Blob & ADLS-File-Enumerator. Finden Sie unter [ForEach-Schleifencontainer](http://msdn.microsoft.com/library/95a19dde-61ca-4d9b-aa3d-131fa4264296)

## <a name="download-the-feature-pack"></a>Download des Feature Packs
 Herunterladen von SQL Server Integration Services (SSIS) Feature Pack für Azure.
 
- [SSIS-Feature Pack für Azure](http://go.microsoft.com/fwlink/?LinkID=626967) für SQLServer 2016
- [SSIS-Feature Pack für Azure](https://www.microsoft.com/en-us/download/details.aspx?id=54798) für[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]

## <a name="prerequisites"></a>Erforderliche Komponenten
 Sie müssen die folgenden erforderlichen Komponenten installieren, bevor Sie dieses Feature Pack installieren.

-   SQL Server Integration Services
-   .NET Framework 4.5

## <a name="scenario-processing-big-data"></a>Szenario: Verarbeitung großer Datenmengen
 Verwenden Sie den Azure Connector zum Ausführen der folgenden Big Data-Verarbeitungsaufgaben:

1.  Verwenden Sie den Azure Blob Upload-Task zum Hochladen von Eingabedaten in den Azure BLOB-Speicher.

2.  Verwenden Sie den Azure HDInsight Create Cluster-Task zum Erstellen eines Azure HDInsight-Clusters. Dieser Schritt ist optional, wenn Sie einen eigenen Cluster verwenden möchten.

3.  Verwenden Sie den Azure HDInsight Hive-Task oder Azure HDInsight Pig-Task zum Aufrufen eines Pig- oder Hive-Auftrags auf dem Azure HDInsight-Cluster.

4.  Verwenden Sie den Azure HDInsight Delete Cluster-Task zum Löschen des HDInsight-Clusters nach der Verwendung, wenn Sie in Schritt 2 einen HDInsight-Bedarfscluster erstellt haben.

5.  Verwenden Sie den Azure HDInsight Blob Download-Task zum Herunterladen der Pig/Hive-Ausgabedaten vom Azure BLOB-Speicher.

![SSIS-AzureConnector-BigDataScenario](../integration-services/media/ssis-azureconnector-bigdatascenario.png)
 
## <a name="scenario-managing-data-in-the-cloud"></a>Szenario: Verwalten von Daten in der Cloud
 Verwenden Sie das Azure BLOB-Ziel in einem SSIS-Paket, um Ausgabedaten in einen Azure BLOB-Speicher zu schreiben, oder verwenden Sie die Azure Blob-Quelle zum Lesen von Daten aus einem Azure BLOB-Speicher.

![SSIS-AzureConnector-CloudArchive-1](../integration-services/media/ssis-azureconnector-cloudarchive-1.png)
 
 ![SSIS-AzureConnector-CloudArchive-2](../integration-services/media/ssis-azureconnector-cloudarchive-2.png)

 Verwenden Sie den Foreach-Schleifencontainer mit dem Azure Blob-Enumerator, um Daten in mehreren BLOB-Dateien zu verarbeiten.

![SSIS-AzureConnector-CloudArchive-3](../integration-services/media/ssis-azureconnector-cloudarchive-3.png)
  

