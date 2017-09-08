---
title: "Unterstützten Datenquellen (SSAS – tabellarisch) | Microsoft Docs"
ms.custom: 
ms.date: 07/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d6c2b1b3-91fc-4175-af25-509946dc7f24
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e5457f0c2abf5f1b7cdae5ff2ae57b5298a72d82
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="data-sources-supported-ssas-tabular"></a>Data Sources Supported (SSAS Tabular)
  In diesem Thema werden die Datenquellentypen beschrieben, die mit tabellarischen Modellen verwendet werden können.  
  
##  <a name="bkmk_supported_ds"></a> Unterstützte Datenquellen für Modelle im Arbeitsspeicher  
 Sie können Daten aus den Datenquellen in der folgenden Tabelle importieren. Bei der Installation von [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]werden die für die einzelnen Datenquellen aufgelisteten Anbieter nicht von Setup installiert. Einige Anbieter wurden möglicherweise bereits mit anderen Anwendungen auf dem Computer installiert. In anderen Fällen müssen Sie den Anbieter herunterladen und installieren.  
  
|||||  
|-|-|-|-|  
|Quelle|Versionen|Dateityp|Anbieter|  
|Access-Datenbanken|Microsoft Access 2010 und höher|.accdb oder .mdb|ACE 14 OLE DB-Anbieter|  
|Relationale SQL Server-Datenbanken|SQLServer 2008 und höher, SQL Server Data Warehouse 2008 und höher, Azure SQL-Datenbank, Azure SQL Data Warehouse, Analytics Platform System (APS)<br /><br /> <br /><br /> Beachten Sie, dass das Analytics Platform System (APS) früher als SQL Server Parallel Data Warehouse (PDW) bezeichnet wurde. Ursprünglich war für das Herstellen einer Verbindung mit PDW von Analysis Services ein spezieller Datenanbieter erforderlich. Dieser Anbieter wurde in SQL Server 2012 ersetzt. Ab SQL Server 2012 wird der SQL Server Native Client für Verbindungen mit PDW/APS verwendet. |(–)|OLE DB-Anbieter für SQL Server<br /><br /> SQL Server Native Client OLE DB-Anbieter<br /><br /> OLE DB-Anbieter für SQL Server Native 10.0 Client<br /><br /> .NET Framework-Datenanbieter für SQL Client|  
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
|Datenfeeds<br /><br /> (wird verwendet, um Daten aus Reporting Services-Berichten, Atom-Dienstdokumenten, Microsoft Azure Marketplace DataMarket und einem einzelnen Datenfeed zu importieren)|Atom 1.0-Format<br /><br /> Sämtliche Datenbanken oder Dokumente, die als Windows Communication Foundation (WCF) Data Service (früher ADO.NET Data Services) verfügbar gemacht werden.|".atomsvc" für ein Dienstdokument, das einen oder mehrere Feeds definiert<br /><br /> ".atom" für ein Atom-Webfeeddokument|Microsoft-Datenfeedanbieter für [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]<br /><br /> .NET Framework-Datenfeedanbieter für [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]|  
|Office Database Connection-Dateien||ODC||  
  
  
##  <a name="bkmk_supported_ds_dq"></a> Unterstützte Datenquellen für DirectQuery-Modelle  
 DirectQuery ist eine Alternative zum In-Memory-Speichermodus. Abfragen werden an Back-End-Datensysteme geleitet und direkt von diesen zurückgegeben, statt dass alle Daten innerhalb des Modells (und im Arbeitsspeicher, sobald das Modell geladen wird) gespeichert werden. Da Analysis Services Abfragen in der systemeigenen Datenbankabfragesyntax-Datenbank formulieren muss, wird eine kleinere Teilmenge von Datenquellen für diesen Modus unterstützt.  
  
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
  
OLE DB-Anbieter können in einigen Fällen bessere Leistung für große Datenmengen anbieten. Bei der Auswahl zwischen unterschiedlichen Anbietern für die gleiche Datenquelle sollten Sie zuerst den OLE DB-Anbieter wählen.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenquellen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/data-sources-ssas-tabular.md)   
 [Importieren von Daten &#40;SSAS – tabellarisch&#41;](http://msdn.microsoft.com/library/6617b2a2-9f69-433e-89e0-4c5dc92982cf)  
  
  

