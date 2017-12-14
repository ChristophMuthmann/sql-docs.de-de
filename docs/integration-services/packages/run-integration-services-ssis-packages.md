---
title: "Ausführen von Integration Services-Paketen (SSIS) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: packages
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ssis.ssms.ispackageexecute.f1
- sql13.ssis.ssms.executepackage.f1
helpviewer_keywords:
- Integration Services packages, running
- SSIS packages, running
- packages [Integration Services], running
- SQL Server Integration Services packages, running
- executing packages [Integration Services]
- running packages [Integration Services]
- Integration Services, (See also Integration Services packages)
ms.assetid: c5fecc23-6f04-4fb2-9a29-01492ea41404
caps.latest.revision: "65"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: fa8080adf06263de7a3055d790b9c5fe89633e20
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="run-integration-services-ssis-packages"></a>Ausführen von Integration Services-Paketen (SSIS)
  Zum Ausführen eines [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Pakets können Sie, abhängig vom Speicherort dieser Pakete, unterschiedliche Tools verwenden. Die Tools werden in der Tabelle unten aufgeführt.  
  
 Zum Speichern eines Pakets auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server verwenden Sie das Projektbereitstellungsmodell, um das Projekt auf dem Server bereitzustellen. Weitere Informationen finden Sie unter [Bereitstellen von SQL Server Integration Services-Projekten und Paketen (SSIS)](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md).  
  
 Zum Speichern eines Pakets im SSIS-Paketspeicher, in der MSDB-Datenbank oder im Dateisystem verwenden Sie das Paketbereitstellungsmodell. Weitere Informationen finden Sie unter [Legacy-Paketbereitstellung &#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md).  
  
|Tool|Pakete, die auf dem Integration Services-Server gespeichert werden|Im SSIS-Paketspeicher oder in der MSDB-Datenbank gespeicherte Pakete|Pakete, die im Dateisystem außerhalb des Speicherorts, der Teil des SSIS-Paketspeichers ist, gespeichert werden|  
|----------|-----------------------------------------------------------------|--------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|  
|**SQL Server Data Tools**|Nein|Nein<br /><br /> Sie können jedoch einem Projekt ein vorhandenes Paket aus dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Paketspeicher hinzufügen, der die msdb-Datenbank enthält. Wenn ein vorhandenes Paket auf diese Weise dem Projekt hinzugefügt wird, wird im Dateisystem eine lokale Kopie des Pakets erstellt.|ja|  
|**SQL Server Management Studio, wenn eine Verbindung mit einer Instanz des Datenbankmoduls besteht, das den Server Integration Services hostet**<br /><br /> Weitere Informationen finden Sie unter [Execute Package Dialog Box](#execute_package_dialog).|ja|Nein<br /><br /> Pakete können jedoch von diesen Speicherorten auf den Server importiert werden.|Nein<br /><br /> Pakete können jedoch aus dem Dateisystem auf den Server importiert werden.|
|**SQL Server Management Studio, wenn eine Verbindung mit einer Instanz des Datenbankmoduls besteht, das den Integration Services-Server hostet, der als Master für horizontales Hochskalieren aktiviert ist**<br /><br /> Weitere Informationen finden Sie unter [Ausführen von Paketen in horizontaler Hochskalierung für Integration Services (SSIS)](../../integration-services/scale-out/run-packages-in-integration-services-ssis-scale-out.md).|ja|Nein|Nein|
|**SQL Server Management Studio, wenn eine Verbindung mit dem Integration Services-Dienst besteht, der den SSIS-Paketspeicher verwaltet**|Nein|Ja|Nein<br /><br /> Pakete können jedoch aus dem Dateisystem in den [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Paketspeicher importiert werden.|  
|**dtexec**<br /><br /> Weitere Informationen finden Sie unter [dtexec Utility](../../integration-services/packages/dtexec-utility.md).|ja|ja|ja|  
|**dtexecui**<br /><br /> Weitere Informationen finden Sie unter [Paketausführungshilfsprogramm &#40;DtExecUI&#41; – Referenz zur Benutzeroberfläche](../../integration-services/packages/execute-package-utility-dtexecui-ui-reference.md).|Nein|Ja|ja|  
|**SQL Server-Agent**<br /><br /> Mit einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Auftrag können Sie ein Paket planen.<br /><br /> Weitere Informationen finden Sie unter [SQL Server Agent Jobs for Packages](../../integration-services/packages/sql-server-agent-jobs-for-packages.md).|ja|ja|ja|  
|**Integrierte gespeicherte Prozedur**<br /><br /> Weitere Informationen finden Sie unter [catalog.start_execution &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md).|Ja|Nein|Nein|  
|**Verwaltete API, mit Typen und Elementen im** <xref:Microsoft.SqlServer.Management.IntegrationServices> -Namespace|ja|Nein|Nein|  
|**Verwaltete API, mit Typen und Elementen im** <xref:Microsoft.SqlServer.Dts.Runtime> -Namespace|Gegenwärtig nicht|ja|ja|  

## <a name="execution-and-logging"></a>Ausführung und Protokollierung  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Pakete können für die Protokollierung aktiviert werden, und Sie können die Laufzeitinformationen in Protokolldateien erfassen. Weitere Informationen finden Sie unter [Integration Services-Protokollierung &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
 Mit Vorgangsberichten können Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Pakete überwachen, die auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server bereitgestellt und ausgeführt werden. Die Berichte sind in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]verfügbar. Weitere Informationen finden Sie unter [Berichte für den Integration Services-Server](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports).  
  
## <a name="run-a-package-in-sql-server-data-tools"></a>Ausführen eines Pakets in SQL Server Data Tools
  Das Ausführen von Paketen in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] erfolgt zumeist beim Entwickeln, Debuggen und Testen von Paketen. Wenn Sie ein Paket im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer ausführen, wird das Paket immer sofort ausgeführt.  
  
 Während ein Paket ausgeführt wird, zeigt der [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer den Fortschritt der Paketausführung auf der **Status** -Registerkarte an. Sie können den Start- und Endzeitpunkt des Pakets sowie seine Tasks und Container sehen. Außerdem werden Informationen über Tasks und Container im Paket angezeigt, deren Ausführung fehlerhaft ist. Wenn die Ausführung des Pakets beendet wurde, sind die Laufzeitinformationen weiterhin auf der Registerkarte **Ausführungsergebnisse** verfügbar. Weitere Informationen finden Sie im Abschnitt "Fortschrittsberichte" im Thema [Debugging Control Flow](../../integration-services/troubleshooting/debugging-control-flow.md).  
  
 **Entwurfszeitbereitstellung**. Wenn Sie ein Paket in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]ausführen, wird das Paket erstellt und dann in einem Ordner bereitgestellt. Vor dem Ausführen des Pakets können Sie den Ordner angeben, in dem das Paket bereitgestellt wird. Wenn Sie keinen Ordner angeben, wird standardmäßig der Ordner **bin** verwendet. Dieser Bereitstellungstyp wird als Entwurfszeitbereitstellung bezeichnet.  
  
### <a name="to-run-a-package-in-sql-server-data-tools"></a>So führen Sie ein Paket in SQL Server-Datentools aus  
  
1.  Wenn die Projektmappe mehrere Projekte enthält, klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem Paket, und klicken Sie anschließend auf **Als Startobjekt festlegen** , um das Startprojekt festzulegen.  
  
2.  Wenn das Projekt mehrere Pakete enthält, klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf das Paket, und klicken Sie anschließend auf **Als Startobjekt** festlegen, um das Startpaket festzulegen.  
  
3.  Sie können ein Paket mit einem der folgenden Schritte ausführen:  
  
    -   Öffnen Sie das Paket, das Sie ausführen möchten, und klicken Sie auf der Menüleiste auf **Debuggen starten** , oder drücken Sie F5. Nachdem das Paket ausgeführt wurde, drücken Sie UMSCHALT+F5, um zum Entwurfsmodus zurückzukehren.  
  
    -   Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf das Paket, und klicken Sie anschließend auf **Paket ausführen**.  
  
### <a name="to-specify-a-different-folder-for-design-time-deployment"></a>So geben Sie einen anderen Ordner für die Entwurfszeitbereitstellung an  
  
1.  Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projektordner, der das auszuführende Paket enthält. Klicken Sie anschließend auf **Eigenschaften**.  
  
2.  Klicken Sie im Dialogfeld **\<Projektname>-Eigenschaftenseiten** auf **Erstellen**.  
  
3.  Aktualisieren Sie den Wert der OutputPath-Eigenschaft, und geben Sie den Ordner an, den Sie für die Entwurfszeitbereitstellung verwenden möchten. Klicken Sie anschließend auf **OK**.  


## <a name="run-a-package-on-the-ssis-server-using-sql-server-management-studio"></a>Ausführen eines Pakets auf dem SSIS-Server mit SQL Server Management Studio
  Nachdem Sie das Projekt auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server bereitgestellt haben, können Sie das Paket auf dem Server ausführen.  
  
 Sie können Vorgangsberichte verwenden, um Informationen über Pakete anzuzeigen, deren Ausführung abgeschlossen ist bzw. die derzeit auf dem Server ausgeführt werden. Weitere Informationen finden Sie unter [Berichte für den Integration Services-Server](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports).  
  
### <a name="to-run-a-package-on-the-server-using-sql-server-management-studio"></a>So führen Sie mit SQL Server Management Studio ein Paket auf dem Server aus  
  
1.  Öffnen Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , und stellen Sie eine Verbindung mit der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] her, die den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Katalog enthält.  
  
2.  Erweitern Sie im Objekt-Explorer den Knoten **Integration Services-Kataloge** und den Knoten **SSISDB** , und navigieren Sie zu dem Paket, das im bereitgestellten Projekt enthalten ist.  
  
3.  Klicken Sie mit der rechten Maustaste auf den Paketnamen, und wählen Sie **Ausführen**aus.  
  
4.  Konfigurieren Sie die Paketausführung mit den Einstellungen im Dialogfeld **Paket ausführen**auf den Registerkarten **Parameter**, **Verbindungs-Managern** und **Erweitert** .  
  
5.  Klicken Sie auf **OK** , um das Paket auszuführen.  
  
     -oder-  
  
     Verwenden Sie gespeicherte Prozeduren zum Ausführen des Pakets. Klicken Sie auf **Skript** , um die Transact-SQL-Anweisung zu generieren, die eine Instanz der Ausführung erstellt und startet. Die Anweisung enthält einen Aufruf der gespeicherten Prozeduren catalog.create_execution, catalog.set_execution_parameter_value und catalog.start_execution. Weitere Informationen zu diesen gespeicherten Prozeduren finden Sie unter [catalog.create_execution &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md), [catalog.set_execution_parameter_value &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md) und [catalog.start_execution &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md).  

## <a name="execute_package_dialog"></a> Execute Package Dialog Box
  Mit dem Dialogfeld **Paket ausführen** können Sie ein Paket auszuführen, das auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server gespeichert ist.  
  
 Ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket kann Parameter enthalten, die auf in Umgebungsvariablen gespeicherte Werte verweisen. Vor dem Ausführen eines solchen Pakets müssen Sie angeben, mit welcher Umgebung die Werte für die Umgebungsvariablen bereitgestellt werden sollen. Ein Projekt kann mehrere Umgebungen enthalten, aber nur eine Umgebung kann zum Binden von Umgebungsvariablenwerten bei der Ausführung verwendet werden. Wenn keine Umgebungsvariablen im Paket verwendet werden, ist auch keine Umgebung erforderlich.  
  
 Was möchten Sie tun?  
  
-   [Öffnen des Dialogfelds "Paket ausführen"](#open_dialog)  
  
-   [Festlegen der Optionen auf der Seite "Allgemein"](#general)  
  
-   [Festlegen der Optionen auf der Registerkarte "Parameter"](#parameters)  
  
-   [Festlegen der Optionen auf der Registerkarte "Verbindungs-Manager"](#connection)  
  
-   [Festlegen der Optionen auf der Registerkarte "Erweitert"](#advanced)  
  
-   [Erstellen der Optionen im Dialogfeld Paket ausführen](#script)  
  
###  <a name="open_dialog"></a> Öffnen des Dialogfelds "Paket ausführen"  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung zum [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server her.  
  
     Sie stellen eine Verbindung mit der [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] -Instanz her, die die SSISDB-Datenbank hostet.  
  
2.  Erweitern Sie im Objekt-Explorer die Struktur, um den Knoten **Integration Services-Kataloge** anzuzeigen.  
  
3.  Erweitern Sie den **SSISDB** -Knoten.  
  
4.  Erweitern Sie den Ordner, der das auszuführende Paket enthält.  
  
5.  Klicken Sie mit der rechten Maustaste auf das Paket, und klicken Sie anschließend auf **Ausführen**.  
  
###  <a name="general"></a> Festlegen der Optionen auf der Seite "Allgemein"  
 Wählen Sie **Umgebung** aus, um die Umgebung anzugeben, die für das ausgeführte Paket angewendet wird.  
  
###  <a name="parameters"></a> Festlegen der Optionen auf der Registerkarte "Parameter"  
 Verwenden Sie die Registerkarte **Parameter** , um die Parameterwerte zu ändern, die bei der Ausführung des Pakets verwendet werden.  
  
###  <a name="connection"></a> Festlegen der Optionen auf der Registerkarte "Verbindungs-Manager"  
 Verwenden Sie die Registerkarte "Verbindungs-Manager", um die Eigenschaften des jeweiligen Paketverbindungs-Managers festzulegen.  
  
###  <a name="advanced"></a> Festlegen der Optionen auf der Registerkarte "Erweitert"  
 Verwenden Sie die Registerkarte "Erweitert", um Eigenschaften und andere Paketeinstellungen zu verwalten.  
  
 **Hinzufügen**, **Bearbeiten**, **Entfernen**  
 Klicken Sie auf die entsprechende Option, um eine Eigenschaft hinzuzufügen, zu bearbeiten oder zu entfernen.  
  
 **Protokolliergrad**  
 Wählen Sie den Protokolliergrad für die Paketausführung aus. Weitere Informationen finden Sie unter [catalog.set_execution_parameter_value &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md).  
  
 **Speichern bei Fehlern**  
 Geben Sie an, ob eine Dumpdatei erstellt wird, wenn Fehler während der Paketausführung auftreten. Weitere Informationen finden Sie unter [Generating Dump Files for Package Execution](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md).  
  
 **32-Bit-Laufzeit**  
 Geben Sie an, dass das Paket auf einem 32-Bit-System ausgeführt wird.  
  
###  <a name="script"></a> Erstellen der Optionen im Dialogfeld Paket ausführen  
 Im Dialogfeld **Paket ausführen** können Sie auch die Schaltfläche **Skript** verwenden, um Code für [!INCLUDE[tsql](../../includes/tsql-md.md)] zu erstellen. Mit dem generierten Skript werden die gespeicherten Prozeduren für [catalog.start_execution &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md) mit den gleichen Optionen ausgeführt, die im Dialogfeld **Paket ausführen** ausgewählt wurden. Das Skript wird in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]in einem neuen Skriptfenster angezeigt.  

## <a name="see-also"></a>Siehe auch  
 [dtexec (Hilfsprogramm)](../../integration-services/packages/dtexec-utility.md)   
[Starten des SQL Server-Import/Export-Assistenten](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)
  
  
