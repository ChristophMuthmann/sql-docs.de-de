---
title: Importieren und Exportieren von Daten mit dem SQL Server-Import/Export-Assistenten | Microsoft-Dokumentation
ms.custom: 
ms.date: 10/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
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
caps.latest.revision: "160"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 2bb672edb72392a8ae215160719aa3476c2452f1
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/01/2017
---
# <a name="import-and-export-data-with-the-sql-server-import-and-export-wizard"></a>Importieren und Exportieren von Daten mit dem SQL Server-Import/Export-Assistenten

 > Inhalte im Zusammenhang mit früheren Versionen von SQL Server finden Sie unter [Run the SQL Server Import and Export Wizard (Ausführen des Import/Export-Assistenten von SQL Server)](https://msdn.microsoft.com/library/ms140052(SQL.120).aspx).

 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Mit dem Import/Export-Assistenten können Daten mühelos aus einer Quelle in ein Ziel kopiert werden. In dieser Übersicht werden die Datenquellen beschrieben, die der Assistent als Quelle oder Ziel verwenden kann, sowie die Berechtigungen, die für das Ausführen des Assistenten erforderlich sind.

## <a name="get-the-wizard"></a>Installieren des Assistenten
Wenn Sie den Assistenten ausführen möchten, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aber nicht auf Ihrem Computer installiert ist, können Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Import/Export-Assistenten mit den SQL Server Data Tools (SSDT) installieren. Weitere Informationen finden Sie unter [Herunterladen von SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).

## <a name="what-happens-when-i-run-the-wizard"></a>Was geschieht, wenn der Assistent ausgeführt wird?
-    **Liste der Schritte** Eine Beschreibung der einzelnen Schritte des Assistenten finden Sie auf der Seite [Steps in the SQL Server Import and Export Wizard (Schritte im SQL Server Import/Export-Assistenten)](../../integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard.md). Es ist außerdem eine eigene Dokumentationsseite für jede Seite des Assistenten verfügbar.  
    \- oder \-
-   **Beispiel** Sehen Sie sich ein einfaches Beispiel auf der Seite [Get started with this simple example of the Import and Export Wizard (Erste Schritte mit diesem einfachen Beispiel für den Import/Export-Assistenten)](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md) an, um einen schnellen Überblick über die verschiedenen Bildschirme in einer typischen Sitzung zu erhalten.  

##  <a name="wizardSources"></a> Welche Quellen und Ziele können verwendet werden?  
 Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Import/Export-Assistent kann Daten in und aus den Datenquellen kopieren, die in der folgenden Tabelle aufgeführt sind. Sie müssen möglicherweise zusätzliche Dateien herunterladen und installieren, um eine Verbindung mit einigen dieser Datenquellen herstellen zu können.
 
| Datenquelle | Muss ich weitere Dateien herunterladen? |
|-------------|-----------------------------------------|
|**Unternehmensdatenbanken**<br/>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Oracle, DB2 und andere.|Durch SQL Server oder SQL Server Data Tools (SSDT) werden die Dateien installiert, die Sie für das Herstellen einer Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] benötigen. SSDT installiert jedoch nicht alle Dateien, die Sie für das Herstellen einer Verbindung mit anderen Enterprise-Datenbanken benötigen, z.B. Oracle oder IBM DB2.<br/><br/>Für das Herstellen einer Verbindung mit einer Enterprise-Datenbank sind folgende Voraussetzungen erforderlich:<br/><br/>1. **Clientsoftware** Wenn Sie bereits die Clientsoftware für Ihr Unternehmensdatenbank-System installiert haben, verfügen Sie in der Regel über das, was zum Herstellen einer Verbindung erforderlich ist. Wenn die Clientsoftware nicht installiert ist, bitten Sie den Datenbankadministrator, eine lizenzierte Kopie zu installieren.<br/><br/>2. **Treiber oder Anbieter** Microsoft installiert die Treiber und Anbieter, die für das Herstellen einer Verbindung mit Oracle erforderlich sind. Rufen Sie den Microsoft® OLEDB-Anbieter für DB2 v5.0 für Microsoft SQL Server aus dem [Microsoft SQL Server 2016 Feature Pack](https://www.microsoft.com/download/details.aspx?id=52676) ab, um eine Verbindung mit IBM DB2 herzustellen.<br/><br/>Weitere Informationen finden Sie unter [Connect to a SQL Server Data Source (Herstellen einer Verbindung mit einer SQL Server-Datenquelle)](connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md) oder [Connect to an Oracle Data Source (Herstellen einer Verbindung mit einer Oracle-Datenquelle)](connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md).|
|**Textdateien** (Flatfiles)|Keine zusätzlichen Dateien erforderlich.<br/><br/>Weitere Informationen finden Sie unter[Connect to a Flat File Data Source (Herstellen einer Verbindung mit einer Flatfile-Datenquelle)](connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md).|
|**Microsoft Excel- und Microsoft Access-Dateien**|Mit Microsoft Office werden nicht alle Dateien installiert, die Sie benötigen, um eine Verbindung mit Excel- und Access-Dateien als Datenquellen herzustellen. Laden Sie [Microsoft Access Database Engine 2016 – Weitervertreibbare Komponente](https://www.microsoft.com/download/details.aspx?id=54920) herunter.<br/><br/>Weitere Informationen finden Sie unter [Connect to an Excel Data Source (Herstellen einer Verbindung mit einer Excel-Datenquelle)](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md) oder [Connect to an Access Data Source (Herstellen einer Verbindung mit einer Access-Datenquelle)](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md).|
|**Azure-Datenquellen**<br/>Derzeit nur Azure BLOB-Speicher.|SQL Server Data Tools installiert nicht die Dateien, die Sie benötigen, um eine Verbindung mit Azure Blob Storage als Datenquelle herzustellen. Laden Sie Folgendes herunter: [Microsoft SQL Server 2016 Integration Services Feature Pack für Azure](https://www.microsoft.com/download/details.aspx?id=49492).<br/><br/>Weitere Informationen finden Sie unter [Connect to Azure Blob Storage (Herstellen einer Verbindung mit Azure Blob Storage)](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md).|
|**Open Source-Datenbanken**<br/>PostgreSQL, MySQL usw.|Sie müssen zusätzliche Dateien herunterladen, um eine Verbindung mit diesen Datenquellen herzustellen.<br/><br/>Weitere Informationen zu **PostgreSQL** finden Sie unter [Connect to a PostgreSQL Data Source (Herstellen einer Verbindung mit einer PostgreSQL-Datenquelle)](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md).<br/>Weitere Informationen zu **MySQL** finden Sie unter [Connect to a MySQL Data Source (Herstellen einer Verbindung mit einer MySQL-Datenquelle)](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md).|
|**Eine beliebige andere Datenquelle, für die ein Treiber oder Anbieter verfügbar ist**|Sie müssen in der Regel zusätzliche Dateien für die Verbindung mit den folgenden Arten von Datenquellen herunterladen.<br/><br/>- Jede Quelle, für die ein **ODBC-Treiber** verfügbar ist. Weitere Informationen finden Sie unter [Connect to an ODBC Data Source (SQL Server Import and Export Wizard)](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md) (Herstellen einer Verbindung mit einer ODBC-Datenquelle [SQL Server-Import/Export-Assistent]).<br/>- Jede Datenquelle, für die ein **.NET Framework-Datenanbieter** verfügbar ist.<br/>- Jede Quelle, für die ein **OLE DB-Treiber** verfügbar ist.<br/><br/>Manche Drittanbieterkomponenten, die Quell- und Zielfunktionen für andere Datenquellen bereitstellen, werden als Add-On-Produkte für SQL Server Integration Services (SSIS) vertrieben.|

## <a name="how-do-i-connect-to-my-data"></a>Wie kann eine Verbindung mit meinen Daten hergestellt werden?
Weitere Informationen zum Herstellen einer Verbindung mit einer häufig verwendeten Datenquelle finden Sie auf folgenden Seiten:
-   [Connect to SQL Server (Herstellen einer Verbindung mit SQL Server)](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)
-   [Herstellen einer Verbindung mit Oracle](../../integration-services/import-export-data/connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)
-   [Connect to flat files (text files)](../../integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md) (Herstellen einer Verbindung mit Flatfiles [Textdateien])
-   [Connect to Excel](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md) (Herstellen einer Verbindung mit Excel)
-   [Connect to Access (Herstellen einer Verbindung mit Access)](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)
-   [Connect to Azure Blob Storage (Herstellen einer Verbindung mit Azure Blob Storage)](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)
-   [Connect with ODBC (Herstellen einer Verbindung mit ODBC)](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)
-   [Connect to PostgreSQL (Herstellen einer Verbindung mit PostgreSQL)](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)
-   [Connect to MySQL (Herstellen einer Verbindung mit MySQL)](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)


Weitere Informationen zum Herstellen einer Verbindung mit einer Datenquelle, die hier nicht aufgeführt ist, finden Sie unter [The Connection Strings Reference (Verweis auf Verbindungszeichenfolgen)](https://www.connectionstrings.com/). Auf dieser Website eines Drittanbieters sind Beispielverbindungszeichenfolgen aufgelistet, und es werden Angaben zu Datenanbietern und den erforderlichen Verbindungsinformationen bereitgestellt.

## <a name="what-permissions-do-i-need"></a>Welche Berechtigungen sind erforderlich?  
 Zum erfolgreichen Ausführen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Import/Export-Assistenten müssen Sie mindestens über die folgenden Berechtigungen verfügen. Wenn Sie bereits mit der Datenquelle und dem Ziel arbeiten, verfügen Sie wahrscheinlich bereits über die erforderlichen Berechtigungen.
  
|Sie benötigen Berechtigungen für diese Vorgänge:|Wenn Sie eine Verbindung mit SQL Server herstellen, benötigen Sie diese spezifischen Berechtigungen: |  
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


