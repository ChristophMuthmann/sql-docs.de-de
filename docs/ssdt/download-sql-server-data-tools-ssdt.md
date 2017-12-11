---
title: Herunterladen von SQL Server Data Tools (SSDT) | Microsoft-Dokumentation
ms.custom: 
ms.date: 10/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssdt
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssdt
ms.tgt_pltfrm: 
ms.topic: article
keywords: SSDT installieren, SSDT herunterladen, aktuelle SSDT-Version
ms.assetid: b0fc4987-d260-4d0a-9dd1-98099835b361
caps.latest.revision: "113"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: 46b86d31a7d5b03bf0c43f61c3c7c7fcf4c2a8ce
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="download-sql-server-data-tools-ssdt"></a>Herunterladen von SQL Server Data Tools (SSDT)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
**[SQL Server Datatools](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx)** ist ein modernes und kostenlos herunterladbares Entwicklungstool für relationale SQL Server-Datenbanken, Azure SQL-Datenbanken, Integration Services-Pakete, Analysis Services-Datenmodelle und Reporting Services-Berichte. Mit SSDT lassen sich Datenbanken und andere Inhaltstypen für SQL Server entwerfen und bereitstellen – und zwar ebenso einfach wie eine Anwendung in Visual Studio. 

SSDT für Visual Studio 2017 (15.4.0, Vorschauversion) ist jetzt verfügbar. Mit diesem Release wird für Projekte von SQL Server-Datenbank, Analysis Services, Reporting Services und Integration Services in Visual Studio 2017 15.4 oder höher eine eigenständige, benutzerfreundliche Webinstallation eingeführt.

| SSDT für Visual Studio 2017 (Vorschauversion) | SSDT für Visual Studio 2015 | 
|:--|:--|
|[![Download](../ssdt/media/download.png) Laden Sie SSDT für Visual Studio 2017 (15.4.0, Vorschauversion) herunter](https://go.microsoft.com/fwlink/?LinkId=860015) | [![Download](../ssdt/media/download.png) Herunterladen von SSDT für Visual Studio 2015 (17.3)](https://go.microsoft.com/fwlink/?linkid=858660)|
|||

> [!IMPORTANT]
> Schließen Sie vor der Installation von SSDT für Visual Studio 2017 (15.4.0, Vorschauversion) alle Instanzen von Visual Studio, und deinstallieren Sie die Erweiterungen „Microsoft Analysis Services-Projekte“ und „Microsoft Reporting Services-Projekte“, wenn diese bereits für Visual Studio 2017 installiert wurden. 
> 
> SSDT für Visual Studio 2017 (15.3.0, Vorschauversion) unterstützt keine Upgrades, daher müssen Sie diese Version deinstallieren, bevor Sie SSDT für Visual Studio 2017 (15.4.0, Vorschauversion) installieren. 


SSDT für Visual Studio 2015 und SSDT für Visual Studio 2017 verwenden beide DacFx 17.3: [Herunterladen von Data-Tier Application Framework (DacFx) 17.3](https://www.microsoft.com/download/details.aspx?id=56048)



## <a name="ssdt-for-visual-studio-2017"></a>SSDT für Visual Studio 2017
**Versionsinformationen**  
  
Releasenummer: 15.4.0, Vorschauversion  
Buildnummer dieses Releases: 14.0.16134.0

Eine vollständige Liste der Änderungen finden Sie unter [changelog (Änderungsprotokoll)](changelog-for-sql-server-data-tools-ssdt.md).

SSDT für Visual Studio 2017 hat die gleichen Systemanforderungen wie die Installation von Visual Studio. Die unterstützten Betriebssysteme sind Windows 7 SP1, Windows 8.1 oder Windows Server 2012 R2 sowie Windows 10 oder Windows Server 2016.  

### <a name="available-languages---ssdt-for-vs-2017"></a>Verfügbare Sprachen: SSDT für Visual Studio 2017
  
 Diese Vorschauversion von SSDT ist zurzeit nur auf Englisch verfügbar.




## <a name="ssdt-for-visual-studio-2015"></a>SSDT für Visual Studio 2015
**Versionsinformationen**  
  
Versionsnummer: 17.3

Buildnummer dieses Release: 14.0.61709.290
  
Eine vollständige Liste der Änderungen finden Sie unter [changelog (Änderungsprotokoll)](changelog-for-sql-server-data-tools-ssdt.md).

### <a name="available-languages---ssdt-for-vs-2015"></a>Verfügbare Sprachen: SSDT für Visual Studio 2015
  
Diese Version von SSDT kann in folgenden Sprachen installiert werden:  

[Chinesisch (Volksrepublik China)]( https://go.microsoft.com/fwlink/?linkid=858660&clcid=0x804) | 
[Chinesisch (Taiwan)]( https://go.microsoft.com/fwlink/?linkid=858660&clcid=0x404) | 
[Englisch (Vereinigte Staaten)]( https://go.microsoft.com/fwlink/?linkid=858660&clcid=0x409) | 
[Französisch]( https://go.microsoft.com/fwlink/?linkid=858660&clcid=0x40c)  
[Deutsch]( https://go.microsoft.com/fwlink/?linkid=858660&clcid=0x407) | 
[Italienisch]( https://go.microsoft.com/fwlink/?linkid=858660&clcid=0x410) | 
[Japanisch]( https://go.microsoft.com/fwlink/?linkid=858660&clcid=0x411) | 
[Koreanisch]( https://go.microsoft.com/fwlink/?linkid=858660&clcid=0x412) | 
[Portugiesisch (Brasilien)]( https://go.microsoft.com/fwlink/?linkid=858660&clcid=0x416) | 
[Russisch]( https://go.microsoft.com/fwlink/?linkid=858660&clcid=0x419) | 
[Spanisch]( https://go.microsoft.com/fwlink/?linkid=858660&clcid=0x40a)  

### <a name="iso-images---ssdt-for-vs-2015"></a>ISO-Images: SSDT für Visual Studio 2015

Alternativ zur Installation von SSDT oder zur Einrichtung eines Administratorinstallationspunkts kann ein ISO-Image von SSDT verwendet werden. Das ISO-Image ist eine eigenständige Datei, die alle für SSDT erforderlichen Komponenten enthält und mit einem Download-Manager heruntergeladen werden kann, der einen Neustart ermöglicht und besonders für begrenzte oder schwankende Netzwerkbandbreiten geeignet ist. Nach dem Download kann das ISO-Image als Laufwerk eingebunden oder auf eine DVD gebrannt werden.

[Chinesisch (Volksrepublik China)]( https://go.microsoft.com/fwlink/?linkid=858663&clcid=0x804) |
[Chinesisch (Taiwan)]( https://go.microsoft.com/fwlink/?linkid=858663&clcid=0x404) |
[Englisch (Vereinigte Staaten)]( https://go.microsoft.com/fwlink/?linkid=858663&clcid=0x409) |
[Französisch]( https://go.microsoft.com/fwlink/?linkid=858663&clcid=0x40c)  
[Deutsch]( https://go.microsoft.com/fwlink/?linkid=858663&clcid=0x407) |
[Italienisch]( https://go.microsoft.com/fwlink/?linkid=858663&clcid=0x410) |
[Japanisch]( https://go.microsoft.com/fwlink/?linkid=858663&clcid=0x411) |
[Koreanisch]( https://go.microsoft.com/fwlink/?linkid=858663&clcid=0x412) |
[Portugiesisch (Brasilien)]( https://go.microsoft.com/fwlink/?linkid=858663&clcid=0x416) |
[Russisch]( https://go.microsoft.com/fwlink/?linkid=858663&clcid=0x419) |
[Spanisch]( https://go.microsoft.com/fwlink/?linkid=858663&clcid=0x40a)


## <a name="download-visual-studio"></a>Herunterladen von Visual Studio

* [**Herunterladen von Visual Studio**](https://www.visualstudio.com/downloads)

## <a name="installing-ssdt-without-visual-studio-pre-installed"></a>Installieren von SSDT ohne vorinstalliertes Visual Studio

Wenn Visual Studio auf Ihrem Computer noch nicht installiert ist, wird bei der Installation von SSDT für Visual Studio eine reduzierte Version von Visual Studio installiert. Diese Version von Visual Studio kann kostenlos installiert und auf so vielen Computern wie gewünscht verwendet werden. Dadurch erhalten Sie alle Projekttypen von SQL Server sowie den *SQL Server-Objekt-Explorer* und weitere SQL-Tools.

Wenn Visual Studio 2015 (oder eine höhere Version) bereits installiert ist, werden mit der Installation von SSDT alle SQL Server-Tools in Ihre vorhandene Installation von Visual Studio eingefügt. In Visual Studio sind viele Features enthalten, die Sie verwenden können – z.B. die Integration der Quellcodeverwaltung und nicht-SQL Sprachunterstützung. Es wird empfohlen, Visual Studio 2015 oder höher zu verwenden, um beim Entwickeln von T-SQL die bestmögliche Erfahrung zu haben.


## <a name="supported-sql-versions"></a>Unterstützte SQL-Versionen
  
|Projektvorlagen|Unterstützte SQL-Plattformen|  
|-------------------|--------------------|  
Relationale Datenbanken|  SQL Server 2005* – SQL Server 2017 <br /><br />Azure SQL-Datenbank<br /><br />Azure SQL Data Warehouse (unterstützt nur Abfragen, Datenbankprojekte werden noch nicht unterstützt)<br /><br />  * SQL Server 2005-Support ist veraltet,<br /><br /> wechseln Sie bitte zu einer offiziell unterstützten SQL-Version|
  |Analysis Services-Modelle<br /><br />Reporting Services-Berichte | SQL Server 2008 – SQL Server 2017|
  |Integration Services-Pakete| SQL Server 2012 – SQL Server 2017    |
  
## <a name="next-steps"></a>Nächste Schritte  
Gehen Sie nach der Installation von SSDT die folgenden Tutorials durch, um zu erfahren, wie Sie mithilfe von SSDT Datenbanken, Pakete, Datenmodelle und Berichte erstellen:  
  
-   [Projektorientierte Offlinedatenbankentwicklung](https://msdn.microsoft.com/library/hh272702(v=vs.103).aspx)  
  
-   [SSIS-Tutorial: Erstellen eines einfachen ETL-Pakets](../integration-services/ssis-how-to-create-an-etl-package.md)  
  
-   [Analysis Services-Tutorials](../analysis-services/analysis-services-tutorials-ssas.md)  
  
-   [Erstellen eines einfachen Tabellenberichts (SSRS-Lernprogramm)](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)  
  



## <a name="see-also"></a>Siehe auch  
[SQL Server Data Tools in Visual Studio](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx)  
[SSDT MSDN-Forum](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=ssdt)  
[SSDT-Team-Blog](http://blogs.msdn.com/b/ssdt/)  
[SSDT Connect Feedback](https://connect.microsoft.com/SQLServer/Feedback)  
[SSDT-Dokumentation](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx)  
[DACFx-API-Referenz](https://msdn.microsoft.com/library/dn645454.aspx)  
[Herunterladen von SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)  
