---
title: "Importieren und Exportieren von Daten mit dem SQL Server-Import/Export-Assistenten | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Exportieren von Daten"
  - "Zuordnen von Dateien [Integration Services]"
  - "SQL Server-Import/Export-Assistent"
  - "SSIS-Pakete, Erstellen"
  - "Pakete [Integration Services], Kopieren"
  - "Integration Services-Pakete, Erstellen"
  - "Pakete [Integration Services], erstellen"
  - "SQL Server Integration Services-Pakete, Erstellen"
  - "Import/Export-Assistent"
  - "Kopieren von Daten [Integration Services]"
  - "Importieren von Daten, SSIS-Pakete"
  - "Quellen [Integration Services], Kopieren von Daten"
ms.assetid: c0e4d867-b2a9-4b2a-844b-2fe45be88f81
caps.latest.revision: 160
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 134
---
# Importieren und Exportieren von Daten mit dem SQL Server-Import/Export-Assistenten
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Mit dem Import/Export-Assistenten können Daten mühelos aus einer Quelle in ein Ziel kopiert werden. SQL Server muss zum Ausführen des Assistenten nicht installiert sein. In dieser Übersicht werden die Datenquellen beschrieben, zu denen Sie mithilfe des Assistenten Daten importieren, oder aus denen heraus Sie Daten exportieren können, und die Berechtigungen, die Sie zum Ausführen des Assistenten benötigen.

Dieses Thema bietet nur einen **Überblick** über den Assistenten.
-   Wenn Sie bereit sind, den Assistenten auszuführen, und nur wissen möchten, wie Sie ihn starten, lesen Sie [Starten des SQL Server-Import/Export-Assistenten](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md).
-   Wenn Sie Informationen zu den Schritten im Assistenten suchen, wählen Sie die gewünschte Seite im Inhaltsnavigationsmenü aus. Es ist eine eigene Dokumentationsseite für jede Seite des Assistenten. Drücken Sie alternativ auf einer beliebigen Seite oder in einem beliebigen Dialogfeld des Assistenten auf F1, um die Dokumentation für die aktuelle Seite anzuzeigen.

**So erhalten Sie den Wizard.** Wenn Sie den Assistenten ausführen möchten, [!INCLUDE[msCoName] (../Token/msCoName_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aber nicht auf Ihrem Computer installiert ist, können Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Import/Export-Assistenten mit den SQL Server Data Tools (SSDT) installieren. Weitere Informationen finden Sie unter [Herunterladen von SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).

> [!TIP] Wenn Sie mehrere Datenbanken oder andere Datenbankobjekte als Tabellen und Sichten kopieren müssen, verwenden Sie anstelle des Import/Export-Assistenten den Assistenten zum Kopieren von Datenbanken. Weitere Informationen finden Sie unter [Verwenden des Assistenten zum Kopieren von Datenbanken](../../relational-databases/databases/use-the-copy-database-wizard.md).

## <a name="example-of-a-common-use-case---exporting-data-to-excel-video"></a>Beispiel für einen allgemeinen Verwendungsfall – Exportieren von Daten in Excel (Video)  
Eine häufige Verwendung des Assistenten ist das Exportieren von Daten nach Excel. Hier können Sie sich ein vierminütiges YouTube-Video ansehen, dass den Assistenten demonstriert und erklärt durch klare und einfache Anweisungen, wie Sie Ihn verwenden – [Using the SQL Server Import and Export Wizard to Export to Excel (Verwenden des SQL Server-Import/Export-Assistenten zum Exportieren nach Excel; in englischer Sprache](https://go.microsoft.com/fwlink/?linkid=829049).

##  <a name="a-namewizardsourcesa-what-data-sources-and-destinations-can-i-use"></a><a name="wizardSources"></a> Welche Datenquellen und -ziele kann ich verwenden?  
 Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Import/Export-Assistent kann Daten in und aus den folgenden Datenquellen kopieren. Um einige dieser Datenquellen verwenden zu können, müssen Sie möglicherweise zusätzliche Dateien herunterladen und installieren.

| Datenquelle | Muss ich weitere Dateien herunterladen? |
|-------------|-----------------------------------------|
|**Unternehmensdatenbanken**<br/>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Oracle und andere.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert die Dateien, die Sie für die Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und Oracle benötigten, nicht jedoch die Dateien, die Sie für die Verbindung mit anderen Unternehmensdatenbanken wie IBM DB2 oder Informix benötigen.<br/>- Wenn Sie bereits die Clientsoftware für Ihr Unternehmensdatenbank-System installiert haben, verfügen Sie in der Regel über das, was zum Herstellen einer Verbindung erforderlich ist.<br/>- Wenn die Clientsoftware nicht installiert ist, bitten Sie den Datenbankadministrator, eine lizenzierte Kopie zu installieren.|
|**Open Source-Datenbanken**<br/>MySql, PostgreSQL, SQLite und andere.|Sie müssen zusätzliche Dateien für die Verbindung mit diesen Datenquellen herunterladen.<br/><br/>- Informationen zu **MySql** finden Sie unter [MySQL-Connectors](http://dev.mysql.com/downloads/connector/).<br/>- Informationen zu **PostgreSQL** finden Sie unter [psqlODBC – PostgreSQL ODBC-Treiber](https://odbc.postgresql.org/) und zu Drittanbieterprodukten unter [Npgsql - .NET Data Provider for PostgreSQL](http://www.npgsql.org/).<br/>- Treffen Sie für **SQLite** eine Auswahl unter mehreren Open-Source-Anbietern und -Treibern, die online zur Verfügung stehen.|
|**Textdateien** (Flatfiles).|Keine zusätzlichen Dateien erforderlich.|
|**Microsoft Excel- und Microsoft Access-Dateien**|Mit Microsoft Office werden nicht alle Dateien installiert, die Sie benötigen, um eine Verbindung mit Excel- und Access-Dateien als Datenquellen herzustellen. Laden Sie Folgendes herunter: [Microsoft Access 2016 Runtime](https://www.microsoft.com/download/details.aspx?id=50040).|
|**Azure-Datenquellen**<br/>Derzeit nur Azure BLOB-Speicher.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert nicht die Dateien, die Sie benötigen, um eine Verbindung mit Azure Blob Storage als Datenquelle herzustellen. Laden Sie Folgendes herunter: [Microsoft SQL Server 2016 Integration Services Feature Pack für Azure](https://www.microsoft.com/download/details.aspx?id=49492).|
|**Eine beliebige andere Datenquelle, für die ein Verbinder verfügbar ist**.|Sie müssen in der Regel zusätzliche Dateien für die Verbindung mit den folgenden Arten von Datenquellen herunterladen.<br/><br/>- Jede Quelle, für die ein **ODBC-Treiber** verfügbar ist. Stellen Sie eine ODBC-Verbindung (Open Database Connectivity) durch Auswahl des .NET Framework-Datenanbieters für ODBC auf der Seite **Datenquelle auswählen** oder **Ziel auswählen** des Assistenten her. Geben Sie anschließend eine Verbindungszeichenfolge oder einen vorhandenen Datenquellennamen (Data Source Name, DSN) an, der auf den ODBC-Treiber verweist.<br/>- Jede Quelle, für die ein **OLE DB-Treiber** verfügbar ist.<br/>- Jede Datenquelle, für die ein **.NET Framework-Datenanbieter** verfügbar ist.<br/>- Andere Datenquellen, für die **Drittanbieterkomponenten** Quell- und Zielfunktionen zur Verfügung stellen. In der Regel werden diese Produkte von Drittanbietern als Add-On-Produkte für SQL Server Integration Services (SSIS) vermarktet.|
  
> [!TIP] Wenn Ihre Datenquelle eine Verbindungszeichenfolge erfordert, finden Sie Beispiele dafür auf der Drittanbieterseite [The Connection Strings Reference](https://www.connectionstrings.com/) (Die Verbindungszeichenfolgen-Referenz).  
  
## <a name="what-permissions-do-i-need-to-run-the-wizard"></a>Welche Berechtigungen benötige ich zum Ausführen des Assistenten?  
 Zum erfolgreichen Ausführen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Import/Export-Assistenten müssen Sie mindestens über die folgenden Berechtigungen verfügen. Wenn Sie bereits mit der Datenquelle und dem Ziel arbeiten, verfügen Sie wahrscheinlich bereits über die erforderlichen Berechtigungen.
  
|Sie benötigen Berechtigungen für diese Vorgänge:|Wenn Sie eine Verbindung mit SQL Server herstellen, benötigen Sie diese Berechtigungen: |  
|-------------------------|----------------------------------------------------|  
|Verbindungen mit den Quell- und Zieldatenbanken bzw. Dateifreigaben herstellen|Anmelderechte für Server und Datenbanken|  
|Daten aus der Quelldatenbank bzw. -datei exportieren oder lesen|SELECT-Berechtigungen für die Quelltabellen und -sichten|  
|Daten in die Zieldatenbank oder -datei importieren oder schreiben|INSERT-Berechtigungen für die Zieltabellen|  
|Zieldatenbank oder -datei erstellen, falls zutreffend|Die Berechtigungen CREATE DATABASE bzw. CREATE TABLE|  
|Das vom Assistenten erstellte SSIS-Paket speichern, falls zutreffend|Wenn Sie das Paket in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] speichern möchten, ausreichende Berechtigungen zum Speichern des Pakets in der **msdb**-Datenbank.|  
  
##  <a name="a-namewizardssisa-the-wizard-uses-sql-server-integration-services-ssis"></a><a name="wizardSSIS"></a> Der Assistent verwendet SQL Server Integration Services (SSIS)  
 Der Assistent verwendet SQL Server Integration Services (SSIS) zum Kopieren von Daten. SSIS ist ein Tool zum Extrahieren, Transformieren und Laden von Daten (ETL). Auf den Seiten des Assistenten wird Terminologie von SSIS verwendet.
  
 In SSIS ist das **Paket** die Basiseinheit. Der Assistent erstellt ein SSIS-Paket im Arbeitsspeicher, während Sie die Seiten des Assistenten durchlaufen und Optionen festlegen.    
  
Wenn nach Durchlaufen des Assistenten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard Edition oder höher installiert ist, können Sie das SSIS-Paket optional speichern. Sie können das Paket später wiederverwenden und erweitern, indem Sie mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)]-Designer Tasks, Transformationen und ereignisgesteuerte Logik hinzufügen. Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Import/Export-Assistent ist die einfachste Methode, ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Paket zu erstellen, mit dem Daten aus einer Quelle in ein Ziel kopiert werden.

Weitere Informationen zu SSIS finden Sie unter [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md).

## <a name="get-help-while-the-wizard-is-running"></a>Aufrufen der Hilfe während der Ausführung des Assistent
> [!TIP] Drücken Sie auf einer beliebigen Seite oder in einem beliebigen Dialogfeld des Assistenten F1, um die Dokumentation für die aktuelle Seite anzuzeigen.   
  
## <a name="whats-next"></a>Wie geht es weiter?  
 Starten Sie den Assistenten. Weitere Informationen finden Sie unter [Starten des SQL Server-Import/Export-Assistenten](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md).  
  
## <a name="see-also"></a>Siehe auch
[Zuordnung von Datentypen mit dem SQL Server-Import/Export-Assistenten](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)
