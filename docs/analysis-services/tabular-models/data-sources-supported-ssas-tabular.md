---
title: In tabellarischen 1200-Modelle von SQL Server Analysis Services unterstützte Datenquellen | Microsoft Docs
ms.custom: ''
ms.date: 03/28/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d6c2b1b3-91fc-4175-af25-509946dc7f24
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 1afd2be21af505d0d027567abe1c7d46c956525d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="data-sources-supported-in-sql-server-analysis-services-tabular-1200-models"></a>Datenquellen unterstützt in SQL Server Analysis Services tabular 1200-Modelle
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  
Dieser Artikel beschreibt die Typen von Datenquellen, die mit SQL Server Analysis Services-Tabellenmodelle die 1200 und niedrigeren Kompatibilitätsgrad verwendet werden können. 

Bei den Kompatibilitätsgraden 1400 Modellen finden Sie unter [in SQL Server Analysis Services Tabellenmodelle 1400 unterstützte Datenquellen](data-sources-supported-ssas-tabular-1400.md).

Azure Analysis Services, finden Sie unter [in Azure Analysis Services unterstützte Datenquellen](https://docs.microsoft.com/azure/analysis-services/analysis-services-datasource).
  
##  <a name="bkmk_supported_ds"></a> Unterstützte Datenquellen für tabellarische Modelle im Arbeitsspeicher  
Bei der Installation von [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]werden die für die einzelnen Datenquellen aufgelisteten Anbieter nicht von Setup installiert. Einige Anbieter wurden möglicherweise mit anderen Anwendungen auf Ihrem Computer installiert werden. In anderen Fällen müssen Sie möglicherweise herunterladen und Installieren des Anbieters.  
  
|||||  
|-|-|-|-|  
|Quelle|Versionen|Dateityp|Anbieter|  
|Access-Datenbanken|Microsoft Access 2010 und höher|.accdb oder .mdb|ACE 14 OLE DB-Anbieter|  
|Relationale SQL Server-Datenbanken|SQLServer 2008 und höher, SQL Server Data Warehouse 2008 und höher, Azure SQL-Datenbank, Azure SQL Data Warehouse, Analytics Platform System (APS)<br /><br /> <br /><br /> Analytics Platform System (APS) wurde früher als SQL Server Parallel Data Warehouse (PDW) bezeichnet. Ursprünglich war für das Herstellen einer Verbindung mit PDW von Analysis Services ein spezieller Datenanbieter erforderlich. Dieser Anbieter wurde in SQL Server 2012 ersetzt. Ab SQL Server 2012 wird der SQL Server Native Client für Verbindungen mit PDW/APS verwendet. |(–)|OLE DB-Anbieter für SQL Server<br /><br /> SQL Server Native Client OLE DB-Anbieter<br /><br /> OLE DB-Anbieter für SQL Server Native 10.0 Client<br /><br /> .NET Framework-Datenanbieter für SQL Client|  
|Relationale Oracle-Datenbanken|Oracle 9i und höher|(–)|OLE DB-Anbieter für Oracle<br /><br /> .NET Framework-Datenanbieter für Oracle Client<br /><br /> .NET Framework-Datenanbieter für SQL Server<br /><br /> OraOLEDB<br /><br /> MSDASQL|  
|Relationale Teradata-Datenbanken|Teradata V2R6 und höher|(–)|OLE DB-Anbieter für TDOLEDB<br /><br /> .NET-Datenanbieter für Teradata|  
|Relationale Informix-Datenbanken||(–)|OLE DB-Anbieter für Informix|  
|Relationale IBM DB2-Datenbanken|8.1|(–)|DB2OLEDB|  
|Relationale Datenbanken von Sybase Adaptive Server Enterprise (ASE)|15.0.2|(–)|OLE DB-Anbieter für Sybase|  
|Andere relationale Datenbanken|(–)|(–)|OLE DB-Anbieter oder ODBC-Treiber|  
|Textdateien|(–)|.txt, .tab, .csv|ACE 14 OLE DB-Anbieter für Microsoft Access|  
|Microsoft Excel-Dateien|Excel 2010 und höher|.xlsx, xlsm, .xlsb, .xltx, .xltm|ACE 14 OLE DB-Anbieter|  
|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappe|Microsoft SQL Server 2008 und höher Analysis Services|XLSX, XLSM, XLSB, XLTX, XLTM|ASOLEDB 10.5<br /><br /> (wird nur für [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappen verwendet, die in SharePoint-Farmen veröffentlicht werden, in denen [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] installiert ist)|  
|Analysis Services-Cube|Microsoft SQL Server 2008 und höher Analysis Services|(–)|ASOLEDB 10|  
|Datenfeeds<br /><br /> (wird verwendet, um Daten aus Reporting Services-Berichten, Atom-Dienstdokumenten, Microsoft Azure Marketplace DataMarket und einem einzelnen Datenfeed zu importieren)|Atom 1.0-Format<br /><br /> Sämtliche Datenbanken oder Dokumente, die als Windows Communication Foundation (WCF) Data Service (früher ADO.NET Data Services) verfügbar gemacht werden.|`.atomsvc` für ein dienstdokument definiert, das einen oder mehrere feeds<br /><br /> ".atom" für ein Atom-Webfeeddokument|Microsoft-Datenfeedanbieter für [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]<br /><br /> .NET Framework-Datenfeedanbieter für [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]|  
|Office Database Connection-Dateien||ODC||  
  
  
##  <a name="bkmk_supported_ds_dq"></a> Unterstützte Datenquellen für DirectQuery-Modelle  
 DirectQuery ist eine Alternative zum In-Memory-Speichermodus. Abfragen werden an Back-End-Datensysteme geleitet und direkt von diesen zurückgegeben, statt dass alle Daten innerhalb des Modells (und im Arbeitsspeicher, sobald das Modell geladen wird) gespeichert werden. Da Analysis Services Abfragen in die Datenbank im einheitlichen Abfragesyntax formuliert, wird eine kleinere Teilmenge von Datenquellen für diesen Modus unterstützt.  
  
Datenquelle   |Versionen  |Anbieter
---------|---------|---------
Microsoft SQL Server    |  2008 und höher      |       OLE DB-Anbieter für SQL Server, OLE DB-Anbieter für SQL Server Native Client, .NET Framework-Datenanbieter für SQL Client  
Microsoft Azure SQL-Datenbank    |   Alle      |  OLE DB-Anbieter für SQL Server, OLE DB-Anbieter für SQL Server Native Client, .NET Framework-Datenanbieter für SQL Client            
Microsoft Azure SQL Data Warehouse     |   Alle     |  OLE DB-Anbieter für SQL Server Native Client, .NET Framework-Datenanbieter für SQL Client       
Microsoft SQL Analytics Platform System (APS)     |   Alle      |  OLE DB-Anbieter für SQL Server, OLE DB-Anbieter für SQL Server Native Client, .NET Framework-Datenanbieter für SQL Client       
Relationale Oracle-Datenbanken     |  Oracle 9i und höher       |  OLE DB-Anbieter für Oracle       
Relationale Teradata-Datenbanken    |  Teradata V2R6 und höher     | .NET-Datenanbieter für Teradata    

  
##  <a name="bkmk_tips"></a> Tipps zum Auswählen von Datenquellen  
  
Durch das Importieren von Tabellen aus relationalen Datenbanken ersparen Sie sich Schritte, da beim Import *Fremdschlüssel* beziehungen verwendet werden, um Beziehungen zwischen den Tabellen im Modell-Designer zu erstellen.  
  
Sie können auch Zeit sparen, indem Sie mehrere Tabellen importieren und dann die Tabellen löschen, die Sie nicht benötigen. Wenn Sie Tabellen einzeln importieren, müssen Sie die Beziehungen zwischen den Tabellen ggf. manuell erstellen.  
  
Spalten, die ähnliche Daten in anderen Datenquellen enthalten, bilden die Basis bei der Erstellung von Beziehungen innerhalb des Modell-Designers. Wenn Sie heterogene Datenquellen verwenden, wählen Sie Tabellen mit Spalten aus, die Tabellen in anderen Datenquellen zugeordnet werden können, die identische oder ähnliche Daten enthalten.  
  
OLE DB-Anbieter können in einigen Fällen bessere Leistung für umfangreiche Datenmengen anbieten. Bei der Auswahl zwischen unterschiedlichen Anbietern für die gleiche Datenquelle sollten Sie zuerst den OLE DB-Anbieter wählen.  

## <a name="see-also"></a>Siehe auch

[Datenquellen unterstützt in SQL Server Analysis Services-Tabellenmodelle 1400](data-sources-supported-ssas-tabular-1400.md)

[In Azure Analysis Services unterstützte Datenquellen](https://docs.microsoft.com/azure/analysis-services/analysis-services-datasource)   