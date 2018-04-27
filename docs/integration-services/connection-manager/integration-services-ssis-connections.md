---
title: Integration Services-Verbindungen (SSIS) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: connection-manager
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.asvs.connectionmanager.f1
- sql13.dts.designer.adddtsconnection.f1
helpviewer_keywords:
- Integration Services packages, connections
- SSIS packages, connections
- sources [Integration Services], connections
- packages [Integration Services], connections
- destinations [Integration Services], connections
- tasks [Integration Services], connections
- connections [Integration Services], about connections
- connections [Integration Services]
- SQL Server Integration Services packages, connections
ms.assetid: 72f5afa3-d636-410b-9e81-2ffa27772a8c
caps.latest.revision: 92
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 0f11d9e2acfac903bd77b2931a06d5a17af9782c
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="integration-services-ssis-connections"></a>Integration Services-Verbindungen (SSIS)
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
  
## <a name="connection-managers"></a>Verbindungs-Manager  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] verwendet den Verbindungs-Manager als logische Darstellung einer Verbindung. Zur Entwurfszeit legen Sie die Eigenschaften eines Verbindungs-Managers fest, um die physische Verbindung zu beschreiben, die [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] beim Ausführen des Pakets erstellt. Beispielsweise enthält ein Verbindungs-Manager die **ConnectionString** -Eigenschaft, die Sie zur Entwurfszeit festlegen. Zur Laufzeit wird mithilfe des Werts in der ConnectionString-Eigenschaft eine physische Verbindung erstellt.  
  
 Ein Paket kann mehrere Instanzen eines Verbindungs-Manager-Typs verwenden, und Sie können die Eigenschaften für jede Instanz festlegen. Zur Laufzeit erstellt jede Instanz eines Verbindungs-Manager-Typs eine Verbindung mit verschiedenen Attributen.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] stellt verschiedene Typen von Verbindungs-Managern bereit, mit denen Pakete eine Verbindung mit einer Reihe von Datenquellen und Servern herstellen können:  
  
-   Einige integrierte Verbindungs-Manager werden bei der Installation von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]installiert.  
  
-   Andere Verbindungs-Manager stehen auf der [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Website zum Herunterladen zur Verfügung.  
  
-   Sie können einen eigenen benutzerdefinierten Verbindungs-Manager erstellen, wenn die vorhandenen Verbindungs-Manager Ihren Anforderungen nicht entsprechen.  

### <a name="package-level-and-project-level-connection-managers"></a>Verbindungs-Manager auf Paket- und Projektebene
Ein Verbindungs-Manager kann auf Paketebene oder auf Projektebene erstellt werden. Ein auf Projektebene erstellter Verbindungs-Manager ist für alle Pakete im Projekt verfügbar. Ein auf Paketebene erstellter Verbindungs-Manager ist nur für das betreffende Paket verfügbar.  
  
 Auf Projektebene erstellte Verbindungs-Manager werden anstelle von Datenquellen verwendet, um Verbindungen mit Quellen freizugeben. Damit ein Verbindungs-Manager auf Projektebene hinzugefügt werden kann, muss das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt das Projektbereitstellungsmodell verwenden. Wenn ein Projekt für die Verwendung des Modells konfiguriert wurde, wird der Ordner **Verbindungs-Manager** im **Projektmappen-Explorer**angezeigt, und der Ordner **Datenquellen** wird aus dem **Projektmappen-Explorer**entfernt.  
  
> [!NOTE]  
>  Wenn Sie Datenquellen im Paket verwenden möchten, müssen Sie das Projekt in das Paketbereitstellungsmodell konvertieren.  
>   
>  Weitere Informationen zu den beiden Modellen und zum Konvertieren eines Projekts in das Projektbereitstellungsmodell finden Sie unter [Deploy Integration Services (SSIS) Projects and Packages](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md) (Bereitstellen von SQL Server Integration Services-Projekten und -Paketen [SSIS]).

### <a name="built-in-connection-managers"></a>Integrierte Verbindungs-Manager  
 In der folgenden Tabelle werden die Verbindungs-Manager-Typen aufgeführt, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] zur Verfügung gestellt werden.  
  
|Typ|Description|Thema|  
|----------|-----------------|-----------|  
|ADO|Stellt eine Verbindung mit ADO-Objekten (ActiveX Data Objects) her.|[ADO-Verbindungs-Manager](../../integration-services/connection-manager/ado-connection-manager.md)|  
|ADO.NET|Stellt eine Verbindung mit einer Datenquelle mithilfe eines .NET-Anbieters her.|[ADO.NET-Verbindungs-Manager](../../integration-services/connection-manager/ado-net-connection-manager.md)|  
|CACHE|Liest Daten aus dem Datenfluss oder einer Cachedatei (.caw) und kann Daten in der Cachedatei speichern.|[Cacheverbindungs-Manager](../../integration-services/connection-manager/cache-connection-manager.md)|  
|DQS|Stellt eine Verbindung mit einem Data Quality Services-Server und einer Data Quality Services-Datenbank auf dem Server her.|[Verbindungs-Manager für DQS-Bereinigung](../../integration-services/connection-manager/dqs-cleansing-connection-manager.md)|  
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
|SMOServer|Stellt eine Verbindung mit einem SMO-Server ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects) her.|[SMO-Verbindungs-Manager](../../integration-services/connection-manager/smo-connection-manager.md)|  
|SMTP|Stellt eine Verbindung mit einem SMTP-Mailserver her.|[SMTP-Verbindungs-Manager](../../integration-services/connection-manager/smtp-connection-manager.md)|  
|SQLMOBILE|Stellt eine Verbindung mit einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact-Datenbank her.|[SQL Server Compact Edition-Verbindungs-Manager](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|  
|WMI|Stellt eine Verbindung mit einem Server her und gibt den Bereich der WMI-Verwaltung (Windows Management Instrumentation, Windows-Verwaltungsinstrumentation) auf dem Server an.|[WMI-Verbindungs-Manager](../../integration-services/connection-manager/wmi-connection-manager.md)|  
  
### <a name="connection-managers-available-for-download"></a>Zum Herunterladen verfügbare Verbindungs-Manager  
 In der folgenden Tabelle sind weitere Typen von Verbindungs-Managern aufgeführt, die von der [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Website heruntergeladen werden können.  
  
> [!IMPORTANT]  
>  Die in der folgenden Tabelle aufgelisteten Verbindungs-Manager funktionieren nur mit [!INCLUDE[ssEnterpriseEd11](../../includes/ssenterpriseed11-md.md)] und [!INCLUDE[ssDeveloperEd11](../../includes/ssdevelopered11-md.md)].  
  
|Typ|Description|Thema|  
|----------|-----------------|-----------|  
|ORACLE|Stellt eine Verbindung mit einem Oracle-\<Versionsinfo\>-Server her.|Der Oracle-Verbindungs-Manager ist die Verbindungs-Manager-Komponente des [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Connectors für Oracle von Attunity. Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Connector für Oracle von Attunity enthält auch eine Quelle und ein Ziel. Weitere Informationen finden Sie auf der Downloadseite [Microsoft Connectors for Oracle and Teradata by Attunity](http://go.microsoft.com/fwlink/?LinkId=251526).|  
|SAPBI|Stellt eine Verbindung mit einem System mit SAP NetWeaver BI, Version 7 her.|Der SAP BI-Verbindungs-Manager ist die Verbindungs-Manager-Komponente des [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Connectors für SAP BI. Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Connector für SAP BI enthält auch eine Quelle und ein Ziel. Weitere Informationen finden Sie auf der Downloadseite [Microsoft SQL Server 2008 Feature Pack](http://go.microsoft.com/fwlink/?LinkId=262016).|  
|TERADATA|Stellt eine Verbindung mit einem Teradata-\<Versionsinfo\>-Server her.|Der Teradata-Verbindungs-Manager ist die Verbindungs-Manager-Komponente des [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Connectors für Teradata von Attunity. Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Connector für Teradata von Attunity enthält auch eine Quelle und ein Ziel. Weitere Informationen finden Sie auf der Downloadseite [Microsoft Connectors for Oracle and Teradata by Attunity](http://go.microsoft.com/fwlink/?LinkId=251526).|  
  
### <a name="custom-connection-managers"></a>Benutzerdefinierte Verbindungs-Manager  
 Sie können auch benutzerdefinierte Verbindungs-Manager schreiben. Weitere Informationen finden Sie unter [Developing a Custom Connection Manager](../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md).  
  
## <a name="create-connection-managers"></a>Erstellen von Verbindungs-Managern
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] enthält eine Reihe von Verbindungs-Managern für Tasks, mit denen eine Verbindung mit verschiedenen Server- und Datenquellentypen hergestellt wird. Verbindungs-Manager werden von den Datenflusskomponenten verwendet, die Daten in verschiedenen Arten von Datenspeichern extrahieren und laden, und von den Protokollanbietern, die Protokolle auf einen Server, in eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle oder eine Datei schreiben. Beispielsweise verwendet ein Paket mit einem Task Mail senden einen SMTP-Verbindungs-Manager, um eine Verbindung mit einem SMTP-Server (Simple Mail Transfer Protocol) herzustellen. Ein Paket mit einem Task SQL ausführen kann einen OLE DB-Verbindungs-Manager zum Herstellen einer Verbindung mit einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank verwenden. Weitere Informationen finden Sie unter [Integration Services-Verbindungen &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md).  
  
 Um die Verbindungs-Manager beim Erstellen eines Pakets automatisch zu erstellen und zu konfigurieren, können Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Import/Export-Assistenten verwenden. Dieser Assistent hilft Ihnen auch, die Quellen und Ziele zu erstellen und zu konfigurieren, die die Verbindungs-Manager verwenden. Weitere Informationen finden Sie unter [Create Packages in SQL Server Data Tools](../../integration-services/create-packages-in-sql-server-data-tools.md).  
  
 Um manuell einen neuen Verbindungs-Manager zu erstellen und ihn einem vorhandenen Paket hinzuzufügen, verwenden Sie den Bereich **Verbindungs-Manager** auf den Registerkarten **Ablaufsteuerung**, **Datenfluss**und **Ereignishandler** des [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designers. Im Bereich **Verbindungs-Manager** wählen Sie in einem Dialogfeld des [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designers den Typ des Verbindungs-Managers zum Erstellen und dann zum Festlegen der Eigenschaften des Verbindungs-Managers aus. Weitere Informationen finden Sie im Abschnitt "Verwenden des Verbindungs-Manager-Bereichs" weiter unten in diesem Thema.  
  
 Nachdem der Verbindungs-Manager einem Paket hinzugefügt wurde, können Sie ihn in Tasks, Foreach-Schleifencontainern, Quellen, Transformationen und Zielen verwenden. Weitere Informationen finden Sie unter [Integration Services-Tasks](../../integration-services/control-flow/integration-services-tasks.md), [Foreach-Schleifencontainer](../../integration-services/control-flow/foreach-loop-container.md), und [Datenfluss](../../integration-services/data-flow/data-flow.md).  
  
### <a name="using-the-connection-managers-area"></a>Verwenden des Verbindungs-Manager-Bereichs  
 Sie können Verbindungs-Manager erstellen, während die Registerkarte **Ablaufsteuerung**, **Datenfluss**oder **Ereignishandler** des [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designers aktiviert ist.  
  
 Im folgenden Diagramm wird der Bereich **Verbindungs-Manager** auf der Registerkarte **Ablaufsteuerung** des [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designers angezeigt.  
  
 ![Screenshot des Ablaufsteuerungs-Designers mit Paket](../../integration-services/connection-manager/media/samplecontrolflow.gif "Screenshot des Ablaufsteuerungs-Designers mit Paket")    
  
### <a name="32-bit-and-64-bit-providers-for-connection-managers"></a>32-Bit- und 64-Bit-Anbieter für Verbindungs-Manager  
 Viele der von Verbindungs-Managern verwendeten Anbieter sind in der 32-Bit- und 64-Bit-Version verfügbar. Die [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Entwurfsumgebung ist eine 32-Bit-Umgebung, sodass beim Entwerfen eines Pakets nur 32-Bit-Anbieter angezeigt werden. Daher können Sie einen Verbindungs-Manager nur dann zum Verwenden eines bestimmten 64-Bit-Anbieters konfigurieren, wenn die 32-Bit-Version desselben Anbieters ebenfalls installiert ist.  
  
 Zur Laufzeit wird stets die richtige Version verwendet, unabhängig davon, ob Sie zur Entwurfszeit die 32-Bit-Version des Anbieters angegeben haben. Die 64-Bit-Version des Anbieters kann auch dann ausgeführt werden, wenn das Paket in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ausgeführt wird.  
  
  Beide Versionen des Anbieters verfügen über die gleiche ID. Um anzugeben, ob die [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Laufzeit eine verfügbare 64-Bit-Version des Anbieters verwenden soll, müssen Sie die Run64BitRuntime-Eigenschaft des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Projekts festlegen. Ist die Run64BitRuntime-Eigenschaft auf **TRUE** festgelegt, wird über die Laufzeit der 64-Bit-Anbieter gefunden und verwendet. Ist die Run64BitRuntime-Eigenschaft jedoch auf **FALSE** festgelegt, wird über die Laufzeit der 32-Bit-Anbieter gefunden und verwendet. Weitere Informationen zu Eigenschaften, die Sie in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Projekten festlegen können, finden Sie unter [Integration Services- (SSIS) und Studio-Umgebungen](https://msdn.microsoft.com/library/ms140028.aspx).   

## <a name="add-a-connection-manager"></a>Hinzufügen eines Verbindungs-Managers
###  <a name="wizard"></a> Hinzufügen eines Verbindungs-Managers beim Erstellen eines Pakets  
  
-   Verwenden des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Import-/Export-Assistenten  
  
     Die Assistenten helfen Ihnen nicht nur bei dem Erstellen und Konfigurieren eines Verbindungs-Managers, sondern auch beim Erstellen und Konfigurieren der Quellen und Ziele, die einen Verbindungs-Manager verwenden. Weitere Informationen finden Sie unter [Create Packages in SQL Server Data Tools](../../integration-services/create-packages-in-sql-server-data-tools.md).  
  
###  <a name="package"></a> Hinzufügen eines Verbindungs-Managers zu einem vorhandenen Paket  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer auf die Registerkarte **Ablaufsteuerung** , **Datenfluss** oder **Ereignishandler** , um den Bereich **Verbindungs-Manager** anzuzeigen.  
  
4.  Klicken Sie mit der rechten Maustaste an eine beliebige Stelle im Bereich **Verbindungs-Manager** , und gehen Sie anschließend wie folgt vor:  
  
    -   Klicken Sie auf den Verbindungs-Manager-Typ, den Sie dem Paket hinzufügen möchten.  
  
         – oder –  
  
    -   Wenn der Typ, den Sie hinzufügen möchten, nicht aufgelistet ist, klicken Sie auf **Neue Verbindung** . Das Dialogfeld **SSIS-Verbindungs-Manager hinzufügen** wird aufgerufen. Wählen Sie einen Verbindungs-Manager-Typ aus, und klicken Sie dann auf **OK**.  
  
     Das benutzerdefinierte Dialogfeld für den ausgewählten Verbindungs-Manager-Typ wird aufgerufen. Weitere Informationen zu den Verbindungs-Manager-Typen und den verfügbaren Optionen finden Sie in der folgenden Optionentabelle.  
  
    |Ziel-Editor für Dimensionsverarbeitung|Tastatur|  
    |------------------------|-------------|  
    |[ADO-Verbindungs-Manager](../../integration-services/connection-manager/ado-connection-manager.md)|[OLE DB-Verbindungs-Manager konfigurieren](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)|  
    |[ADO.NET-Verbindungs-Manager](../../integration-services/connection-manager/ado-net-connection-manager.md)|[ADO.NET-Verbindungs-Manager konfigurieren](../../integration-services/connection-manager/configure-ado-net-connection-manager.md)|  
    |[Analysis Services-Verbindungs-Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md)|[Referenz zur Benutzeroberfläche des Dialogfelds „Analysis Services-Verbindungs-Manager hinzufügen“](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Excel-Verbindungs-Manager](../../integration-services/connection-manager/excel-connection-manager.md)|[Verbindungs-Manager-Editor für Excel](../../integration-services/connection-manager/excel-connection-manager-editor.md)|  
    |[Dateiverbindungs-Manager](../../integration-services/connection-manager/file-connection-manager.md)|[Dateiverbindungs-Manager-Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)|  
    |[Verbindungs-Manager für mehrere Dateien](../../integration-services/connection-manager/multiple-files-connection-manager.md)|[Referenz zur Benutzeroberfläche des Dialogfelds „Dateiverbindungs-Manager hinzufügen“](../../integration-services/connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[Verbindungs-Manager für Flatfiles](../../integration-services/connection-manager/flat-file-connection-manager.md)|[Verbindungs-Manager-Editor für Flatfiles &#40;Seite Allgemein&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-general-page.md)<br /><br /> [Verbindungs-Manager-Editor für Flatfiles &#40;Seite Spalten&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-columns-page.md)<br /><br /> [Verbindungs-Manager-Editor für Flatfiles &#40;Seite Erweitert&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-advanced-page.md)<br /><br /> [Verbindungs-Manager-Editor für Flatfiles &#40;Seite Vorschau&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md)|  
    |[Verbindungs-Manager für mehrere Flatfiles](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)|[Verbindungs-Manager-Editor für mehrere Flatfiles &#40;Seite „Allgemein“&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-general-page.md)<br /><br /> [Verbindungs-Manager-Editor für mehrere Flatfiles &#40;Seite „Spalten“&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-columns-page.md)<br /><br /> [Verbindungs-Manager-Editor für mehrere Flatfiles &#40;Seite „Erweitert“&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-advanced-page.md)<br /><br /> [Verbindungs-Manager-Editor für mehrere Flatfiles &#40;Seite „Vorschau“&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-preview-page.md)|  
    |[FTP-Verbindungs-Manager](../../integration-services/connection-manager/ftp-connection-manager.md)|[FTP-Verbindungs-Manager-Editor](../../integration-services/connection-manager/ftp-connection-manager-editor.md)|  
    |[HTTP-Verbindungs-Manager](../../integration-services/connection-manager/http-connection-manager.md)|[HTTP-Verbindungs-Manager-Editor &#40;Seite „Server“&#41;](../../integration-services/connection-manager/http-connection-manager-editor-server-page.md)<br /><br /> [HTTP-Verbindungs-Manager-Editor &#40;Seite „Proxy“&#41;](../../integration-services/connection-manager/http-connection-manager-editor-proxy-page.md)|  
    |[MSMQ-Verbindungs-Manager](../../integration-services/connection-manager/msmq-connection-manager.md)|[MSMQ-Verbindungs-Manager-Editor](../../integration-services/connection-manager/msmq-connection-manager-editor.md)|  
    |[ODBC-Verbindungs-Manager](../../integration-services/connection-manager/odbc-connection-manager.md)|[ODBC-Verbindungs-Manager – Referenz zur Benutzeroberfläche](../../integration-services/connection-manager/odbc-connection-manager-ui-reference.md)|  
    |[OLE DB-Verbindungs-Manager](../../integration-services/connection-manager/ole-db-connection-manager.md)|[OLE DB-Verbindungs-Manager konfigurieren](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)|  
    |[SMO-Verbindungs-Manager](../../integration-services/connection-manager/smo-connection-manager.md)|[SMO-Verbindungs-Manager-Editor](../../integration-services/connection-manager/smo-connection-manager-editor.md)|  
    |[SMTP-Verbindungs-Manager](../../integration-services/connection-manager/smtp-connection-manager.md)|[SMTP-Verbindungs-Manager-Editor](../../integration-services/connection-manager/smtp-connection-manager-editor.md)|  
    |[SQL Server Compact Edition-Verbindungs-Manager](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|[Verbindungs-Manager-Editor für SQL Server Compact Edition &#40;Seite „Verbindung“&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-connection-page.md)<br /><br /> [Verbindungs-Manager-Editor für SQL Server Compact Edition &#40;Seite „Alle“&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-all-page.md)|  
    |[WMI-Verbindungs-Manager](../../integration-services/connection-manager/wmi-connection-manager.md)|[WMI-Verbindungs-Manager-Editor](../../integration-services/connection-manager/wmi-connection-manager-editor.md)|  
  
     Der Bereich **Verbindungs-Manager** enthält eine Liste mit den hinzugefügten Verbindungs-Managern.  
  
5.  Klicken Sie wahlweise mit der rechten Maustaste auf den Verbindungs-Manager, klicken Sie auf **Umbenennen**, und ändern Sie anschließend den Standardnamen des Verbindungs-Managers.  
  
6.  Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  
  
###  <a name="project"></a> Hinzufügen eines Verbindungs-Manager auf Projektebene  
  
1.  Öffnen Sie das [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]-Projekt in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
2.  Klicken Sie im **Projektmappen-Explorer**mit der rechten Maustaste auf **Verbindungs-Manager**, und klicken Sie auf **Neuer Verbindungs-Manager**.  
  
3.  Wählen Sie im Dialogfeld **SSIS-Verbindungs-Manager hinzufügen** den Typ des Verbindungs-Managers aus, und klicken Sie dann auf **Hinzufügen**.  
  
     Das benutzerdefinierte Dialogfeld für den ausgewählten Verbindungs-Manager-Typ wird aufgerufen. Weitere Informationen zu den Verbindungs-Manager-Typen und den verfügbaren Optionen finden Sie in der folgenden Optionentabelle.  
  
    |Ziel-Editor für Dimensionsverarbeitung|Tastatur|  
    |------------------------|-------------|  
    |[ADO-Verbindungs-Manager](../../integration-services/connection-manager/ado-connection-manager.md)|[OLE DB-Verbindungs-Manager konfigurieren](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)|  
    |[ADO.NET-Verbindungs-Manager](../../integration-services/connection-manager/ado-net-connection-manager.md)|[ADO.NET-Verbindungs-Manager konfigurieren](../../integration-services/connection-manager/configure-ado-net-connection-manager.md)|  
    |[Analysis Services-Verbindungs-Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md)|[Referenz zur Benutzeroberfläche des Dialogfelds „Analysis Services-Verbindungs-Manager hinzufügen“](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Excel-Verbindungs-Manager](../../integration-services/connection-manager/excel-connection-manager.md)|[Verbindungs-Manager-Editor für Excel](../../integration-services/connection-manager/excel-connection-manager-editor.md)|  
    |[Dateiverbindungs-Manager](../../integration-services/connection-manager/file-connection-manager.md)|[Dateiverbindungs-Manager-Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)|  
    |[Verbindungs-Manager für mehrere Dateien](../../integration-services/connection-manager/multiple-files-connection-manager.md)|[Referenz zur Benutzeroberfläche des Dialogfelds „Dateiverbindungs-Manager hinzufügen“](../../integration-services/connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[Verbindungs-Manager für Flatfiles](../../integration-services/connection-manager/flat-file-connection-manager.md)|[Verbindungs-Manager-Editor für Flatfiles &#40;Seite Allgemein&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-general-page.md)<br /><br /> [Verbindungs-Manager-Editor für Flatfiles &#40;Seite Spalten&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-columns-page.md)<br /><br /> [Verbindungs-Manager-Editor für Flatfiles &#40;Seite Erweitert&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-advanced-page.md)<br /><br /> [Verbindungs-Manager-Editor für Flatfiles &#40;Seite Vorschau&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md)|  
    |[Verbindungs-Manager für mehrere Flatfiles](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)|[Verbindungs-Manager-Editor für mehrere Flatfiles &#40;Seite „Allgemein“&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-general-page.md)<br /><br /> [Verbindungs-Manager-Editor für mehrere Flatfiles &#40;Seite „Spalten“&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-columns-page.md)<br /><br /> [Verbindungs-Manager-Editor für mehrere Flatfiles &#40;Seite „Erweitert“&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-advanced-page.md)<br /><br /> [Verbindungs-Manager-Editor für mehrere Flatfiles &#40;Seite „Vorschau“&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-preview-page.md)|  
    |[FTP-Verbindungs-Manager](../../integration-services/connection-manager/ftp-connection-manager.md)|[FTP-Verbindungs-Manager-Editor](../../integration-services/connection-manager/ftp-connection-manager-editor.md)|  
    |[HTTP-Verbindungs-Manager](../../integration-services/connection-manager/http-connection-manager.md)|[HTTP-Verbindungs-Manager-Editor &#40;Seite „Server“&#41;](../../integration-services/connection-manager/http-connection-manager-editor-server-page.md)<br /><br /> [HTTP-Verbindungs-Manager-Editor &#40;Seite „Proxy“&#41;](../../integration-services/connection-manager/http-connection-manager-editor-proxy-page.md)|  
    |[MSMQ-Verbindungs-Manager](../../integration-services/connection-manager/msmq-connection-manager.md)|[MSMQ-Verbindungs-Manager-Editor](../../integration-services/connection-manager/msmq-connection-manager-editor.md)|  
    |[ODBC-Verbindungs-Manager](../../integration-services/connection-manager/odbc-connection-manager.md)|[ODBC-Verbindungs-Manager – Referenz zur Benutzeroberfläche](../../integration-services/connection-manager/odbc-connection-manager-ui-reference.md)|  
    |[OLE DB-Verbindungs-Manager](../../integration-services/connection-manager/ole-db-connection-manager.md)|[OLE DB-Verbindungs-Manager konfigurieren](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)|  
    |[SMO-Verbindungs-Manager](../../integration-services/connection-manager/smo-connection-manager.md)|[SMO-Verbindungs-Manager-Editor](../../integration-services/connection-manager/smo-connection-manager-editor.md)|  
    |[SMTP-Verbindungs-Manager](../../integration-services/connection-manager/smtp-connection-manager.md)|[SMTP-Verbindungs-Manager-Editor](../../integration-services/connection-manager/smtp-connection-manager-editor.md)|  
    |[SQL Server Compact Edition-Verbindungs-Manager](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|[Verbindungs-Manager-Editor für SQL Server Compact Edition &#40;Seite „Verbindung“&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-connection-page.md)<br /><br /> [Verbindungs-Manager-Editor für SQL Server Compact Edition &#40;Seite „Alle“&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-all-page.md)|  
    |[WMI-Verbindungs-Manager](../../integration-services/connection-manager/wmi-connection-manager.md)|[WMI-Verbindungs-Manager-Editor](../../integration-services/connection-manager/wmi-connection-manager-editor.md)|  
  
     Der Verbindungs-Manager, den Sie hinzugefügt haben, wird unter dem Knoten **Verbindungs-Manager** im **Projektmappen-Explorer**angezeigt. Er wird auch auf der Registerkarte **Verbindungs-Manager** im Fenster **SSIS-Designer** für alle Pakete im Projekt angezeigt. Der Name des Verbindungs-Managers auf dieser Registerkarte enthält **(project)** als Präfix, um diesen Verbindungs-Manager auf Projektebene von den Verbindungs-Managern auf Paketebene zu unterscheiden.  
  
4.  Klicken Sie optional mit der rechten Maustaste auf den Verbindungs-Manager im Fenster des **Projektmappen-Explorer** unter dem Knoten **Verbindungs-Manager** , bzw. klicken Sie auf der Registerkarte **Verbindungs-Manager** des Fensters **SSIS-Designer** auf **Umbenennen**, und ändern Sie anschließend den Standardnamen des Verbindungs-Managers.  
  
    > [!NOTE]  
    >  Auf der Registerkarte **Verbindungs-Manager** des Fensters **SSIS-Designer** kann das Präfix **(project)** im Namen des Verbindungs-Managers nicht überschrieben werden. Dies ist beabsichtigt.  

### <a name="add-ssis-connection-manager-dialog-box"></a>SSIS-Verbindungs-Manager hinzufügen (Dialogfeld)
Im Dialogfeld **SSIS-Verbindungs-Manager hinzufügen** können Sie den Verbindungstyp auswählen, der dem Paket hinzugefügt werden soll.  
  
 Weitere Informationen zu Verbindungs-Managern finden Sie unter [Integration Services-Verbindungen &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md).  
  
#### <a name="options"></a>Tastatur  
 **Typ des Verbindungs-Managers**  
 Wählen Sie einen Verbindungstyp aus, und klicken Sie anschließend auf **Hinzufügen**, oder doppelklicken Sie auf einen Verbindungstyp, um mithilfe des Editors für den jeweiligen Verbindungstyp die Eigenschaften der Verbindung anzugeben.  
  
 **Hinzufügen**  
 Geben Sie mithilfe des Editors für den jeweiligen Verbindungstyp die Eigenschaften der Verbindung an.  
   
##  <a name="parameter"></a> Erstellen eines Parameters für eine Verbindungs-Manager-Eigenschaft  
  
1.  Klicken Sie mit der rechten Maustaste im Bereich **Verbindungs-Manager** auf den Verbindungs-Manager, für den Sie einen Parameter erstellen möchten, und klicken Sie anschließend auf **Parametrisieren**.  
  
2.  Konfigurieren Sie die Parametereinstellungen im Dialogfeld **Parametrisieren** . Weitere Informationen finden Sie unter [Parameterize Dialog Box](http://msdn.microsoft.com/library/fac02b6d-d247-447a-8940-e8700c7ac350).  

## <a name="delete-a-connection-manager"></a>Löschen eines Verbindungs-Managers 
###  <a name="DeletePackageLevel"></a> Löschen eines Verbindungs-Managers aus einem Paket  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer auf die Registerkarte **Ablaufsteuerung** , **Datenfluss** oder **Ereignishandler** , um den Bereich **Verbindungs-Manager** anzuzeigen.  
  
4.  Klicken Sie mit der rechten Maustaste auf den Verbindungs-Manager, den Sie löschen möchten, und klicken Sie anschließend auf **Löschen**.  
  
     Wenn Sie einen Verbindungs-Manager löschen, der von Paketelementen wie dem Task SQL ausführen oder einer OLE DB-Quelle verwendet wird, erhalten Sie die folgenden Ergebnisse:  
  
    -   Auf dem Paketelement, das den gelöschten Verbindungs-Manager verwendet hat, wird ein Fehlersymbol angezeigt.  
  
    -   Die Überprüfung des Pakets schlägt fehl.  
  
    -   Das Paket kann nicht ausgeführt werden.  
  
5.  Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  
  
###  <a name="DeleteProjectLevel"></a> Löschen eines gemeinsam genutzten Verbindungs-Managers (Verbindungs-Manager auf Projektebene)  
  
1.  Klicken Sie mit der rechten Maustaste auf den Verbindungs-Manager unter dem Knoten **Verbindungs-Manager** im Fenster des **Projektmappen-Explorers** , und klicken Sie anschließend auf **Löschen**, um einen Verbindungs-Manager auf Projektebene zu löschen. [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] zeigt die folgende Warnmeldung an:  
  
    > [!WARNING]  
    >  Wenn Sie einen Verbindungs-Manager auf Projektebene löschen, könnten Pakete, die den Verbindungs-Manager verwenden, nicht ausgeführt werden. Dieser Vorgang lässt sich nicht rückgängig machen. Möchten Sie den Verbindungs-Manager löschen?  
  
2.  Klicken Sie auf "OK", um den Verbindungs-Manager zu löschen, oder auf "Abbrechen", um ihn beizubehalten.  
  
    > [!NOTE]  
    >  Sie können auch einen Verbindungs-Manager auf Projektebene von der Registerkarte **Verbindungs-Manager** des Fensters **SSIS-Designer** löschen, das für ein beliebiges Paket im Projekt geöffnet wurde. Klicken Sie hierfür mit der rechten Maustaste auf den Verbindungs-Manager auf der Registerkarte und anschließend auf **Löschen**. 
    
## <a name="set-the-properties-of-a-connection-manager"></a>Festlegen der Eigenschaften eines Verbindungs-Managers
Alle Verbindungs-Manager können im Fenster **Eigenschaften** konfiguriert werden.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] enthält auch benutzerdefinierte Dialogfelder zum Ändern verschiedener Typen des Verbindungs-Managers in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Das Dialogfeld enthält je nach Typ des Verbindungs-Managers verschiedene Gruppen mit Optionen.  
  
### <a name="modify-a-connection-manager-using-the-properties-window"></a>Ändern eines Verbindungs-Managers mithilfe des Eigenschaftenfensters  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie im SSIS-Designer auf die Registerkarte **Ablaufsteuerung** , die Registerkarte **Datenfluss** oder die Registerkarte **Ereignishandler** , um den Bereich **Verbindungs-Manager** verfügbar zu machen.  
  
4.  Klicken Sie mit der rechten Maustaste auf den Verbindungs-Manager, und klicken Sie dann auf **Eigenschaften**.  
  
5.  Ändern Sie im Fenster **Eigenschaften** die Eigenschaftswerte. Das Fenster **Eigenschaften** bietet Zugriff auf einige Eigenschaften, die im Standard-Editor für einen Verbindungs-Manager nicht konfigurierbar sind.  
  
6.  Klicken Sie auf **OK**.  
  
7.  Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  
  
### <a name="modify-a-connection-manager-using-a-connection-manager-dialog-box"></a>Ändern eines Verbindungs-Managers mithilfe des Dialogfelds „Verbindungs-Manager“  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer auf die Registerkarte **Ablaufsteuerung** , **Datenfluss** oder **Ereignishandler** , um den Bereich **Verbindungs-Manager** anzuzeigen.  
  
4.  Doppelklicken Sie im Bereich **Verbindungs-Manager** auf den Verbindungs-Manager, um das Dialogfeld **Verbindungs-Manager** zu öffnen. Informationen über bestimmte Verbindungs-Manager-Typen und die für jeden Typ verfügbaren Optionen finden Sie in der folgenden Tabelle.  
  
    |Ziel-Editor für Dimensionsverarbeitung|Tastatur|  
    |------------------------|-------------|  
    |[ADO-Verbindungs-Manager](../../integration-services/connection-manager/ado-connection-manager.md)|[OLE DB-Verbindungs-Manager konfigurieren](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)|  
    |[ADO.NET-Verbindungs-Manager](../../integration-services/connection-manager/ado-net-connection-manager.md)|[ADO.NET-Verbindungs-Manager konfigurieren](../../integration-services/connection-manager/configure-ado-net-connection-manager.md)|  
    |[Analysis Services-Verbindungs-Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md)|[Referenz zur Benutzeroberfläche des Dialogfelds „Analysis Services-Verbindungs-Manager hinzufügen“](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Excel-Verbindungs-Manager](../../integration-services/connection-manager/excel-connection-manager.md)|[Verbindungs-Manager-Editor für Excel](../../integration-services/connection-manager/excel-connection-manager-editor.md)|  
    |[Dateiverbindungs-Manager](../../integration-services/connection-manager/file-connection-manager.md)|[Dateiverbindungs-Manager-Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)|  
    |[Verbindungs-Manager für mehrere Dateien](../../integration-services/connection-manager/multiple-files-connection-manager.md)|[Referenz zur Benutzeroberfläche des Dialogfelds „Dateiverbindungs-Manager hinzufügen“](../../integration-services/connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[Verbindungs-Manager für Flatfiles](../../integration-services/connection-manager/flat-file-connection-manager.md)|[Verbindungs-Manager-Editor für Flatfiles &#40;Seite Allgemein&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-general-page.md)<br /><br /> [Verbindungs-Manager-Editor für Flatfiles &#40;Seite Spalten&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-columns-page.md)<br /><br /> [Verbindungs-Manager-Editor für Flatfiles &#40;Seite Erweitert&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-advanced-page.md)<br /><br /> [Verbindungs-Manager-Editor für Flatfiles &#40;Seite Vorschau&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md)|  
    |[Verbindungs-Manager für mehrere Flatfiles](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)|[Verbindungs-Manager-Editor für mehrere Flatfiles &#40;Seite „Allgemein“&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-general-page.md)<br /><br /> [Verbindungs-Manager-Editor für mehrere Flatfiles &#40;Seite „Spalten“&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-columns-page.md)<br /><br /> [Verbindungs-Manager-Editor für mehrere Flatfiles &#40;Seite „Erweitert“&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-advanced-page.md)<br /><br /> [Verbindungs-Manager-Editor für mehrere Flatfiles &#40;Seite „Vorschau“&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-preview-page.md)|  
    |[FTP-Verbindungs-Manager](../../integration-services/connection-manager/ftp-connection-manager.md)|[FTP-Verbindungs-Manager-Editor](../../integration-services/connection-manager/ftp-connection-manager-editor.md)|  
    |[HTTP-Verbindungs-Manager](../../integration-services/connection-manager/http-connection-manager.md)|[HTTP-Verbindungs-Manager-Editor &#40;Seite „Server“&#41;](../../integration-services/connection-manager/http-connection-manager-editor-server-page.md)<br /><br /> [HTTP-Verbindungs-Manager-Editor &#40;Seite „Proxy“&#41;](../../integration-services/connection-manager/http-connection-manager-editor-proxy-page.md)|  
    |[MSMQ-Verbindungs-Manager](../../integration-services/connection-manager/msmq-connection-manager.md)|[MSMQ-Verbindungs-Manager-Editor](../../integration-services/connection-manager/msmq-connection-manager-editor.md)|  
    |[ODBC-Verbindungs-Manager](../../integration-services/connection-manager/odbc-connection-manager.md)|[ODBC-Verbindungs-Manager – Referenz zur Benutzeroberfläche](../../integration-services/connection-manager/odbc-connection-manager-ui-reference.md)|  
    |[OLE DB-Verbindungs-Manager](../../integration-services/connection-manager/ole-db-connection-manager.md)|[OLE DB-Verbindungs-Manager konfigurieren](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)|  
    |[SMO-Verbindungs-Manager](../../integration-services/connection-manager/smo-connection-manager.md)|[SMO-Verbindungs-Manager-Editor](../../integration-services/connection-manager/smo-connection-manager-editor.md)|  
    |[SMTP-Verbindungs-Manager](../../integration-services/connection-manager/smtp-connection-manager.md)|[SMTP-Verbindungs-Manager-Editor](../../integration-services/connection-manager/smtp-connection-manager-editor.md)|  
    |[SQL Server Compact Edition-Verbindungs-Manager](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|[Verbindungs-Manager-Editor für SQL Server Compact Edition &#40;Seite „Verbindung“&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-connection-page.md)<br /><br /> [Verbindungs-Manager-Editor für SQL Server Compact Edition &#40;Seite „Alle“&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-all-page.md)|  
    |[WMI-Verbindungs-Manager](../../integration-services/connection-manager/wmi-connection-manager.md)|[WMI-Verbindungs-Manager-Editor](../../integration-services/connection-manager/wmi-connection-manager-editor.md)|  
  
5.  Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  

## <a name="related-content"></a>Verwandte Inhalte  
  
-   Video, [Nutzen der Vorteile von Microsoft Attunity Connector für Oracle zur Erweiterung der Paketleistung](http://technet.microsoft.com/sqlserver/gg598963.aspx), auf technet.microsoft.com  
  
-   Wiki-Artikel, [SSIS-Konnektivität](http://social.technet.microsoft.com/wiki/contents/articles/sql-server-integration-services-ssis.aspx#Connectivity), auf social.technet.microsoft.com  
  
-   Blogeintrag [Verbinden mit MySQL von SSIS](http://go.microsoft.com/fwlink/?LinkId=217669)auf blogs.msdn.com.  
  
-   Technischer Artikel zum [Extrahieren und Laden von SharePoint-Daten in SQL Server Integration Services](http://go.microsoft.com/fwlink/?LinkId=247826)auf msdn.microsoft.com.  
  
-   Technischer Artikel [You get "DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER" error message when using Oracle connection manager in SSIS (Sie erhalten die Fehlermeldung "DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER" bei der Verwendung eines Oracle-Verbindungs-Managers in SSIS)](http://go.microsoft.com/fwlink/?LinkId=233696)auf support.microsoft.com.  
  
  
