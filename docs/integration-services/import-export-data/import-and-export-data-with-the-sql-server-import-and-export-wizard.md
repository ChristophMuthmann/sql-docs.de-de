---
title: Importieren und Exportieren von Daten mit der SQL Server-Import / Export-Assistent | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- exporting data
- mapping files [Integration Services]
- SQL Server Import and Export Wizard
- SSIS packages, creating
- packages [Integration Services], copying
- Integration Services packages, creating
- packages [Integration Services], creating
- SQL Server Integration Services packages, creating
- Import and Export Wizard
- copying data [Integration Services]
- importing data, SSIS packages
- sources [Integration Services], copying data
ms.assetid: c0e4d867-b2a9-4b2a-844b-2fe45be88f81
caps.latest.revision: 160
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: 58908fc8a7b18cff36a41ee26e7a3eab8e84a5d0
ms.contentlocale: de-de
ms.lasthandoff: 09/21/2017

---
# <a name="import-and-export-data-with-the-sql-server-import-and-export-wizard"></a>Importieren und Exportieren von Daten mit dem SQL Server-Import/Export-Assistenten

 > Inhalt im Zusammenhang mit früheren Versionen von SQL Server, finden Sie unter [führen Sie die SQL Server-Import / Export-Assistenten](https://msdn.microsoft.com/en-US/library/ms140052(SQL.120).aspx).

 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Mit dem Import/Export-Assistenten können Daten mühelos aus einer Quelle in ein Ziel kopiert werden. In dieser Übersicht werden die Datenquellen, die der Assistent als Quellen und Zielen verwenden kann sowie die Berechtigungen, die Sie benötigen, um den Assistenten auszuführen.

## <a name="get-the-wizard"></a>Abrufen des Assistenten
Wenn Sie den Assistenten ausführen möchten, aber Sie verfügen nicht über [! UMFASSEN[MsCoName](/sql-docs/docs/ssdt/download-sql-server-data-tools-ssdt).

## <a name="what-happens-when-i-run-the-wizard"></a>Was geschieht, wenn ich den Assistenten ausführen?
-    **Zeigen Sie die Liste der Schritte an.** Eine Beschreibung der Schritte im Assistenten, finden Sie unter [Schritte in der SQL Server-Import / Export-Assistenten](../../integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard.md). Es gibt auch eine separate Seite der Dokumentation für jede Seite des Assistenten.  
    \- oder \-
-   **Finden Sie ein einfaches Beispiel.** Für einen kurzen Blick auf die mehrere Bildschirme in eine typische Sitzung angezeigt werden soll, sehen Sie sich diesem einfachen End-to-End-Beispiel auf einer Seite - [beginnen Sie mit diesem einfachen Beispiel des Import / Export-Assistenten](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md).  

##  <a name="wizardSources"></a>Verwenden Quellen und Ziele kann ich?  
 Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Import / Export-Assistenten können Daten kopieren in und aus den Datenquellen in der folgenden Tabelle aufgeführt. Um einige der Datenquellen zu verbinden, müssen Sie möglicherweise zusätzliche Dateien herunterladen und installieren.
 
| Datenquelle | Muss ich weitere Dateien herunterladen? |
|-------------|-----------------------------------------|
|**Unternehmensdatenbanken**<br/>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Oracle, DB2 und andere.|SQL Server- oder SQL Server Data Tools (SSDT) installiert die Dateien, die Sie benötigen für die Verbindung [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Aber SSDT nicht alle Dateien, die Sie für die Verbindung mit anderen Enterprise-Datenbanken, z. B. Oracle- oder IBM DB2 müssen installiert werden.<br/><br/>Um eine Verbindung mit einer Enterprise-Datenbank herstellen, benötigen Sie in der Regel zwei Dinge:<br/><br/>1. **Clientsoftware**. Wenn Sie bereits die Clientsoftware für Ihr Unternehmensdatenbank-System installiert haben, verfügen Sie in der Regel über das, was zum Herstellen einer Verbindung erforderlich ist. Wenn die Clientsoftware nicht installiert ist, bitten Sie den Datenbankadministrator, eine lizenzierte Kopie zu installieren.<br/><br/>2. **Treiber oder Anbieter**. Microsoft installierten Treiber und Anbieter für die Verbindung mit Oracle. Zur Verbindung mit IBM DB2 erhalten Sie die Microsoft® OLE DB-Anbieter für DB2 V5. 0 für Microsoft SQL Server aus der [Microsoft SQL Server 2016 Feature Pack](https://www.microsoft.com/download/details.aspx?id=52676).|
|**Textdateien** (Flatfile-Dateien)|Keine zusätzlichen Dateien erforderlich.|
|**Microsoft Excel- und Microsoft Access-Dateien**|Mit Microsoft Office werden nicht alle Dateien installiert, die Sie benötigen, um eine Verbindung mit Excel- und Access-Dateien als Datenquellen herzustellen. Rufen Sie den folgenden Download - [Microsoft Access Database Engine 2016 Redistributable](https://www.microsoft.com/download/details.aspx?id=54920).<br/><br/>Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit einer Excel-Datenquelle](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md) oder [Herstellen einer Verbindung mit einer Access-Datenquelle](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md).|
|**Azure-Datenquellen**<br/>Derzeit nur Azure BLOB-Speicher.|SQL Server Data Tools installieren nicht die Dateien, die Sie zum Azure-Blob-Speicher als Datenquelle herstellen müssen. Laden Sie Folgendes herunter: [Microsoft SQL Server 2016 Integration Services Feature Pack für Azure](https://www.microsoft.com/download/details.aspx?id=49492).<br/><br/>Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit Azure BLOB Storage](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md).|
|**Open Source-Datenbanken**<br/>PostgreSQL, MySQL- und andere.|Sie müssen zusätzliche Dateien für die Verbindung mit diesen Datenquellen herunterladen.<br/><br/>– Für **PostgreSQL**, finden Sie unter [Herstellen einer Verbindung mit einer Datenquelle PostgreSQL](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md).<br/>– Für **MySql**, finden Sie unter [Herstellen einer Verbindung mit einer Datenquelle MySQL](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md).|
|**Eine beliebige andere Datenquelle, für die ein Treiber oder Anbieter verfügbar ist**|Sie müssen in der Regel zusätzliche Dateien für die Verbindung mit den folgenden Arten von Datenquellen herunterladen.<br/><br/>- Jede Quelle, für die ein **ODBC-Treiber** verfügbar ist. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit einer ODBC-Datenquelle](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).<br/>- Jede Datenquelle, für die ein **.NET Framework-Datenanbieter** verfügbar ist.<br/>- Jede Quelle, für die ein **OLE DB-Treiber** verfügbar ist.<br/><br/>Drittanbieter-Komponenten, die Quell- und Zielserver für andere Datenquellen ermöglichen werden als Add-On-Produkten für SQL Server Integration Services (SSIS) manchmal vertrieben.|

## <a name="how-do-i-connect-to-my-data"></a>Wie verbinde ich mich mit meiner Daten?
Informationen zum Herstellen einer Verbindung mit einer häufig verwendeten Datenquelle finden Sie unter den folgenden Seiten.
-   [Connect to SQL Server (Herstellen einer Verbindung mit SQL Server)](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)
-   [Herstellen einer Verbindung mit Oracle](../../integration-services/import-export-data/connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)
-   [Herstellen einer Verbindung mit Flatfile-Dateien (Textdateien)](../../integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)
-   [Herstellen einer Verbindung mit Excel](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)
-   [Herstellen einer Verbindung mit Access](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)
-   [Herstellen einer Verbindung mit Azure-Blob-Speicher](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)
-   [Herstellen einer Verbindung mit ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)
-   [Herstellen einer Verbindung mit PostgreSQL](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)
-   [Herstellen einer Verbindung mit MySQL](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)


Informationen zum Herstellen einer Verbindung mit einer Datenquelle, die hier nicht aufgeführt ist, finden Sie unter [der Zeichenfolgen-Verbindungsverweis](https://www.connectionstrings.com/). Diese Site eines Drittanbieters enthält Beispiele für Verbindungszeichenfolgen und Weitere Informationen zu Datenanbietern und die Verbindungsinformationen, die sie benötigen.

## <a name="what-permissions-do-i-need"></a>Welche Berechtigungen benötige ich?  
 Zum erfolgreichen Ausführen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Import/Export-Assistenten müssen Sie mindestens über die folgenden Berechtigungen verfügen. Wenn Sie bereits mit der Datenquelle und dem Ziel arbeiten, verfügen Sie wahrscheinlich bereits über die erforderlichen Berechtigungen.
  
|Sie benötigen Berechtigungen für diese Vorgänge:|Wenn Sie die Verbindung mit SQL Server herstellen, benötigen Sie diese bestimmten Berechtigungen |  
|-------------------------|----------------------------------------------------|  
|Verbindungen mit den Quell- und Zieldatenbanken bzw. Dateifreigaben herstellen|Anmelderechte für Server und Datenbanken|  
|Daten aus der Quelldatenbank bzw. -datei exportieren oder lesen|SELECT-Berechtigungen für die Quelltabellen und -sichten|  
|Daten in die Zieldatenbank oder -datei importieren oder schreiben|INSERT-Berechtigungen für die Zieltabellen|  
|Zieldatenbank oder -datei erstellen, falls zutreffend|Die Berechtigungen CREATE DATABASE bzw. CREATE TABLE|  
|Das vom Assistenten erstellte SSIS-Paket speichern, falls zutreffend|Wenn Sie das Paket in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]speichern möchten, ausreichende Berechtigungen zum Speichern des Pakets in der **msdb** -Datenbank.|  
  
## <a name="get-help-while-the-wizard-is-running"></a>Aufrufen der Hilfe während der Ausführung des Assistent
> [!TIP]
> Drücken Sie auf einer beliebigen Seite oder in einem beliebigen Dialogfeld des Assistenten F1, um die Dokumentation für die aktuelle Seite anzuzeigen.   
  
##  <a name="wizardSSIS"></a> Der Assistent verwendet SQL Server Integration Services (SSIS)  
 Der Assistent verwendet SQL Server Integration Services (SSIS) zum Kopieren von Daten. SSIS ist ein Tool zum Extrahieren, Transformieren und Laden von Daten (ETL). Auf den Seiten des Assistenten wird Terminologie von SSIS verwendet.
  
 In SSIS ist das **Paket**die Basiseinheit. Der Assistent erstellt ein SSIS-Paket im Arbeitsspeicher, während Sie die Seiten des Assistenten durchlaufen und Optionen festlegen.    
  
Wenn nach Durchlaufen des Assistenten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard Edition oder höher installiert ist, können Sie das SSIS-Paket optional speichern. Sie können das Paket später wiederverwenden und erweitern, indem Sie mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer Tasks, Transformationen und ereignisgesteuerte Logik hinzufügen. Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Import/Export-Assistent ist die einfachste Methode, ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket zu erstellen, mit dem Daten aus einer Quelle in ein Ziel kopiert werden.

Weitere Informationen zu SSIS finden Sie unter [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md).

## <a name="whats-next"></a>Wie geht es weiter?  
 Starten Sie den Assistenten. Weitere Informationen finden Sie unter [Starten des SQL Server-Import/Export-Assistenten](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md).  

## <a name="see-also"></a>Siehe auch
[Erste Schritte mit diesem einfachen Beispiel des Import/Export-Assistenten](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)  
[Zuordnung von Datentypen mit dem SQL Server-Import/Export-Assistenten](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)



