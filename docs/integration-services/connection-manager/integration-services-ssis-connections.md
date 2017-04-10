---
title: "Integration Services-Verbindungen (SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.asvs.connectionmanager.f1"
  - "sql13.dts.designer.adddtsconnection.f1"
helpviewer_keywords: 
  - "Integration Services-Pakete, Verbindungen"
  - "SSIS-Pakete, Verbindungen"
  - "Quellen [Integration Services], Verbindungen"
  - "Pakete [Integration Services], Verbindungen"
  - "Ziele [Integration Services], Verbindungen"
  - "Tasks, [Integration Services], Verbindungen"
  - "Verbindungen [Integration Services], Über Verbindungen"
  - "Verbindungen [Integration Services]"
  - "SQL Server Integration Services-Pakete, Verbindungen"
ms.assetid: 72f5afa3-d636-410b-9e81-2ffa27772a8c
caps.latest.revision: 92
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 91
---
# Integration Services-Verbindungen (SSIS)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Pakete verwenden Verbindungen zum Ausführen verschiedener Tasks und zum Implementieren von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Funktionen.  
  
-   Herstellen einer Verbindung mit Quell- und Zieldatenspeichern, z. B. Text, XML, Excel-Arbeitsmappen und relationale Datenbanken, zum Extrahieren und Laden von Daten.  
  
-   Herstellen einer Verbindung mit relationalen Datenbanken, die Verweisdaten zum Ausführen von genauen oder Fuzzysuchvorgängen beinhalten.  
  
-   Herstellen einer Verbindung mit relationalen Datenbanken zum Ausführen von SQL-Anweisungen, z. B. der Befehle SELECT-, DELETE- und INSERT, sowie zum Ausführen gespeicherter Prozeduren.  
  
-   Herstellen einer Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zum Durchführen von Wartungs- und Übertragungstasks, z. B. dem Sichern von Datenbanken und Übertragen von Anmeldungen.  
  
-   Schreiben von Protokolleinträgen in Text- und XML-Dateien und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabellen sowie Paketkonfigurationen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabellen.  
  
-   Herstellen einer Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zum Erstellen temporärer Arbeitstabellen, die von einigen Transformationen benötigt werden.  
  
-   Herstellen einer Verbindung mit [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekten und -Datenbanken für den Zugriff auf Data Mining-Modelle, zum Verarbeiten von Cubes und Dimensionen und zum Ausführen von DDL-Code.  
  
-   Angeben vorhandener Dateien und Ordner bzw. Erstellen neuer Dateien und Ordner für die Verwendung mit Foreach-Schleifenenumeratoren und Tasks.  
  
-   Herstellen einer Verbindung mit Meldungswarteschlangen sowie mit der Windows-Verwaltungsinstrumentation (WMI, Windows Management Instrumentation), mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects (SMO), dem Web und mit Mailservern.  
  
 Um diese Verbindungen herzustellen, verwendet [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Verbindungs-Manager. Dies wird im nächsten Abschnitt beschrieben.  
  
## Verbindungs-Manager  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] verwendet den Verbindungs-Manager als logische Darstellung einer Verbindung. Zur Entwurfszeit legen Sie die Eigenschaften eines Verbindungs-Managers fest, um die physische Verbindung zu beschreiben, die [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] beim Ausführen des Pakets erstellt. Beispielsweise enthält ein Verbindungs-Manager die **ConnectionString** -Eigenschaft, die Sie zur Entwurfszeit festlegen. Zur Laufzeit wird mithilfe des Werts in der ConnectionString-Eigenschaft eine physische Verbindung erstellt.  
  
 Ein Paket kann mehrere Instanzen eines Verbindungs-Manager-Typs verwenden, und Sie können die Eigenschaften für jede Instanz festlegen. Zur Laufzeit erstellt jede Instanz eines Verbindungs-Manager-Typs eine Verbindung mit verschiedenen Attributen.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] stellt verschiedene Typen von Verbindungs-Managern bereit, mit denen Pakete eine Verbindung mit einer Reihe von Datenquellen und Servern herstellen können:  
  
-   Einige integrierte Verbindungs-Manager werden bei der Installation von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] installiert.  
  
-   Andere Verbindungs-Manager stehen auf der [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Website zum Herunterladen zur Verfügung.  
  
-   Sie können einen eigenen benutzerdefinierten Verbindungs-Manager erstellen, wenn die vorhandenen Verbindungs-Manager Ihren Anforderungen nicht entsprechen.  
  
### Integrierte Verbindungs-Manager  
 In der folgenden Tabelle werden die Verbindungs-Manager-Typen aufgeführt, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] zur Verfügung gestellt werden.  
  
|Typ|Description|Thema|  
|----------|-----------------|-----------|  
|ADO|Stellt eine Verbindung mit ADO-Objekten (ActiveX Data Objects) her.|[ADO-Verbindungs-Manager](../../integration-services/connection-manager/ado-connection-manager.md)|  
|ADO.NET|Stellt eine Verbindung mit einer Datenquelle mithilfe eines .NET-Anbieters her.|[ADO.NET-Verbindungs-Manager](../../integration-services/connection-manager/ado-net-connection-manager.md)|  
|CACHE|Liest Daten aus dem Datenfluss oder einer Cachedatei (.caw) und kann Daten in der Cachedatei speichern.|[Cacheverbindungs-Manager](../../integration-services/data-flow/transformations/cache-connection-manager.md)|  
|DQS|Stellt eine Verbindung mit einem Data Quality Services-Server und einer Data Quality Services-Datenbank auf dem Server her.|[Verbindungs-Manager für DQS-Bereinigung](../../integration-services/data-flow/transformations/dqs-cleansing-connection-manager.md)|  
|EXCEL|Stellt eine Verbindung mit einer Excel-Arbeitsmappendatei her.|[Excel-Verbindungs-Manager](../../integration-services/connection-manager/excel-connection-manager.md)|  
|FILE|Stellt eine Verbindung mit einer Datei oder einem Ordner her.|[Dateiverbindungs-Manager](../../integration-services/connection-manager/file-connection-manager.md)|  
|FLATFILE|Stellt eine Verbindung mit Daten in einer einzelnen Flatfile her.|[Verbindungs-Manager für Flatfiles](../../integration-services/connection-manager/flat-file-connection-manager.md)|  
|FTP|Stellt eine Verbindung mit einem FTP-Server her.|[FTP-Verbindungs-Manager](../../integration-services/connection-manager/ftp-connection-manager.md)|  
|HTTP|Stellt eine Verbindung mit einem Webserver her.|[HTTP-Verbindungs-Manager](../../integration-services/connection-manager/http-connection-manager.md)|  
|MSMQ|Stellt eine Verbindung mit einer Nachrichtenwarteschlange her.|[MSMQ-Verbindungs-Manager](../../integration-services/connection-manager/msmq-connection-manager.md)|  
|MSOLAP100|Stellt eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oder einem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt her.|[Analysis Services-Verbindungs-Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md)|  
|MULTIFILE|Stellt eine Verbindung mit mehreren Dateien und Ordnern her.|[Verbindungs-Manager für mehrere Dateien](../../integration-services/connection-manager/multiple-files-connection-manager.md)|  
|MULTIFLATFILE|Stellt eine Verbindung mit mehreren Datendateien und Ordnern her.|[Verbindungs-Manager für mehrere Flatfiles](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)|  
|OLEDB|Stellt eine Verbindung mit einer Datenquelle mithilfe eines OLE DB-Anbieters her.|[OLE DB-Verbindungs-Manager](../../integration-services/connection-manager/ole-db-connection-manager.md)|  
|ODBC|Stellt eine Verbindung mit einer Datenquelle mithilfe von ODBC her.|[ODBC-Verbindungs-Manager](../../integration-services/connection-manager/odbc-connection-manager.md)|  
|SMOServer|Stellt eine Verbindung mit einem SMO-Server ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects) her.|[SMO-Verbindungs-Manager](../../integration-services/connection-manager/smo-connection-manager.md)|  
|SMTP|Stellt eine Verbindung mit einem SMTP-Mailserver her.|[SMTP-Verbindungs-Manager](../../integration-services/connection-manager/smtp-connection-manager.md)|  
|SQLMOBILE|Stellt eine Verbindung mit einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact-Datenbank her.|[SQL Server Compact Edition-Verbindungs-Manager](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|  
|WMI|Stellt eine Verbindung mit einem Server her und gibt den Bereich der WMI-Verwaltung (Windows Management Instrumentation, Windows-Verwaltungsinstrumentation) auf dem Server an.|[WMI-Verbindungs-Manager](../../integration-services/connection-manager/wmi-connection-manager.md)|  
  
### Zum Herunterladen verfügbare Verbindungs-Manager  
 In der folgenden Tabelle sind weitere Typen von Verbindungs-Managern aufgeführt, die von der [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Website heruntergeladen werden können.  
  
> [!IMPORTANT]  
>  Die in der folgenden Tabelle aufgelisteten Verbindungs-Manager funktionieren nur mit [!INCLUDE[ssEnterpriseEd11](../../includes/ssenterpriseed11-md.md)] und [!INCLUDE[ssDeveloperEd11](../../includes/ssdevelopered11-md.md)].  
  
|Typ|Description|Thema|  
|----------|-----------------|-----------|  
|ORACLE|Stelle eine Verbindung mit einem Oracle \<Versionsinfo>-Server her.|Der Oracle-Verbindungs-Manager ist die Verbindungs-Manager-Komponente des [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Connectors für Oracle von Attunity. Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Connector für Oracle von Attunity enthält auch eine Quelle und ein Ziel. Weitere Informationen finden Sie auf der Downloadseite [Microsoft Connectors for Oracle and Teradata by Attunity](http://go.microsoft.com/fwlink/?LinkId=251526).|  
|SAPBI|Stellt eine Verbindung mit einem System mit SAP NetWeaver BI, Version 7 her.|Der SAP BI-Verbindungs-Manager ist die Verbindungs-Manager-Komponente des [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Connectors für SAP BI. Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Connector für SAP BI enthält auch eine Quelle und ein Ziel. Weitere Informationen finden Sie auf der Downloadseite [Microsoft SQL Server 2008 Feature Pack](http://go.microsoft.com/fwlink/?LinkId=262016).|  
|TERADATA|Stellt eine Verbindung mit einem Teradata \<Versionsinfo>-Server her.|Der Teradata-Verbindungs-Manager ist die Verbindungs-Manager-Komponente des [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Connectors für Teradata von Attunity. Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Connector für Teradata von Attunity enthält auch eine Quelle und ein Ziel. Weitere Informationen finden Sie auf der Downloadseite [Microsoft Connectors for Oracle and Teradata by Attunity](http://go.microsoft.com/fwlink/?LinkId=251526).|  
  
### Benutzerdefinierte Verbindungs-Manager  
 Sie können auch benutzerdefinierte Verbindungs-Manager schreiben. Weitere Informationen finden Sie unter [Developing a Custom Connection Manager](../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md).  
  
## Verwandte Aufgaben  
 Ausführliche Informationen zum Hinzufügen oder Löschen eines Verbindungs-Managers in einem Paket finden Sie unter [Hinzufügen, Löschen oder Freigeben eines Verbindungs-Managers in einem Paket](../Topic/Add,%20Delete,%20or%20Share%20a%20Connection%20Manager%20in%20a%20Package.md).  
  
 Details zum Festlegen der Eigenschaften eines Verbindungs-Managers in einem Paket finden Sie unter [Festlegen der Eigenschaften eines Verbindungs-Managers](../Topic/Set%20the%20Properties%20of%20a%20Connection%20Manager.md).  
  
## Verwandte Inhalte  
  
-   Video, [Nutzen der Vorteile von Microsoft Attunity Connector für Oracle zur Erweiterung der Paketleistung](http://technet.microsoft.com/sqlserver/gg598963.aspx), auf technet.microsoft.com  
  
-   Wiki-Artikel, [SSIS-Konnektivität](http://social.technet.microsoft.com/wiki/contents/articles/sql-server-integration-services-ssis.aspx#Connectivity), auf social.technet.microsoft.com  
  
-   Blogeintrag [Verbinden mit MySQL von SSIS](http://go.microsoft.com/fwlink/?LinkId=217669)auf blogs.msdn.com.  
  
-   Technischer Artikel zum [Extrahieren und Laden von SharePoint-Daten in SQL Server Integration Services](http://go.microsoft.com/fwlink/?LinkId=247826)auf msdn.microsoft.com.  
  
-   Technischer Artikel [You get "DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER" error message when using Oracle connection manager in SSIS (Sie erhalten die Fehlermeldung "DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER" bei der Verwendung eines Oracle-Verbindungs-Managers in SSIS)](http://go.microsoft.com/fwlink/?LinkId=233696) auf support.microsoft.com.  
  
  