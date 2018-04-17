---
title: In SQL Server Analysis Services Tabellenmodelle 1400 unterstützte Datenquellen | Microsoft Docs
ms.date: 03/26/2018
ms.prod: analysis-services
ms.suite: pro-bi
ms.topic: article
ms.assetid: ''
author: Minewiskan
ms.author: owend
manager: kfile
monikerRange: '>= sql-analysis-services-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: c32b715ac73fd69e63bad8487950ff1e4df003c9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="data-sources-supported-in-sql-server-analysis-services-tabular-1400-models"></a>Datenquellen unterstützt in SQL Server Analysis Services-Tabellenmodelle 1400

[!INCLUDE[ssas-appliesto-sql2017](../../includes/ssas-appliesto-sql2017.md)]

Dieser Artikel beschreibt die Typen von Datenquellen, die mit tabellarischen Modellen von SQL Server Analysis Services (SSAS) mit dem Kompatibilitätsgrad 1400 verwendet werden können. 

SSAS-Tabellenmodelle bei den 1200 und niedrigeren Kompatibilitätsgraden, finden Sie unter [in tabellarischen 1200-Modelle von SQL Server Analysis Services unterstützte Datenquellen](data-sources-supported-ssas-tabular.md).

Azure Analysis Services, finden Sie unter [in Azure Analysis Services unterstützte Datenquellen](https://docs.microsoft.com/azure/analysis-services/analysis-services-datasource).


## <a name="cloud-data-sources"></a>Cloud-Datenquellen

|Azure-Datenquelle  |In-memory  |DirectQuery  |
|---------|---------|---------|
|Azure SQL Database     |   ja      |    ja      |
|Azure SQL Data Warehouse     |   ja      |   ja       |
|Azure BLOB-Speicher     |   ja       |    nein      |
|Azure-Tabellenspeicher    |   ja       |    nein      |
|Azure-Cosmos-DB      |  ja        |  nein        |
|Azure Data Lake-Speicher     |   ja       |    nein      |
|Azure HDInsight HDFS     |     ja     |   nein       |
|Azure HDInsight Spark (Beta)     |   ja       |   nein       |
||||

**Anbieter**   
Arbeitsspeicherinterne und DirectQuery-Modellen Herstellen einer Verbindung mit Azure-Datenquellen verwenden .NET Framework-Datenanbieter für SQL Server.

## <a name="on-premises-data-sources"></a>Auf lokale Datenquellen

### <a name="supported-by-in-memory-and-directquery-models"></a>Von speicherinternen und DirectQuery-Modelle unterstützt werden

|Datenquelle | In-Memory-Anbieter | DirectQuery-Anbieter |
|  --- | --- | --- |
| SQL Server |SQL Server Native Client 11.0, Microsoft OLE DB-Anbieter für SQLServer, .NET Framework-Datenanbieter für SQLServer | .NET Framework-Datenanbieter für SQL Server |
| SQL Server Datawarehouse |SQL Server Native Client 11.0, Microsoft OLE DB-Anbieter für SQLServer, .NET Framework-Datenanbieter für SQLServer | .NET Framework-Datenanbieter für SQL Server |
| Oracle |Microsoft OLE DB-Anbieter von Oracle, Oracle-Datenanbieter für .NET |Oracle-Datenanbieter für .NET | |
| Teradata |OLE DB-Anbieter für Teradata von Teradata-Datenanbieter für .NET |Teradata-Datenanbieter für .NET | |
| | | |

> [!NOTE]
> Bei speicherinternen Modellen können OLE DB-Anbieter eine bessere Leistung für umfangreiche Daten bereitstellen. Bei der Auswahl zwischen unterschiedlichen Anbietern für die gleiche Datenquelle zuerst den OLE DB-Anbieter.  

### <a name="supported-by-in-memory-models-only"></a>Unterstützt von speicherinternen Modellen nur

|Datenbank  |
|---------|---------|---------|
|Access-Datenbank     | 
|SQL Server Analysis Services     | 
|IBM Informix (Beta) | 
|JSON-Dokument     | 
|Zeilen aus der Binärdatei     | 
|MySQL-Datenbank     | 
|PostgreSQL-Datenbank    | ja | nein
|SAP HANA   | ja | nein
|SAP Business Warehouse    | ja | nein
|Sybase-Datenbank     | ja | nein
|||

|File  |  
|---------|---------|
|Excel-Arbeitsmappe     |
|Ordner     | 
|JSON | 
|Text/CSV    | 
|XML-Tabelle    | 
|||

|Online-Dienste  |  
|---------|---------|
|Dynamics 365      |
|Exchange Online     |
|Saleforce-Objekte    | 
|Salesforce-Berichte     |
|SharePoint Online-Liste     |
|||

|Andere  |  
|---------|---------|
|Active Directory      | 
|Exchange     |  
|OData-Feed     | 
|ODBC-Abfrage     | 
|OLE DB  | 
|SharePoint-Liste | 
|||

## <a name="see-also"></a>Siehe auch

[Datenquellen unterstützt in SQL Server Analysis Services tabular 1200-Modelle](data-sources-supported-ssas-tabular.md)

[In Azure Analysis Services unterstützte Datenquellen](https://docs.microsoft.com/azure/analysis-services/analysis-services-datasource)   
