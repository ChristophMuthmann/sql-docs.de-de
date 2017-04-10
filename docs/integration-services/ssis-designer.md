---
title: "SSIS-Designer | Microsoft Docs"
ms.custom: ""
ms.date: "08/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.controlflowwindow.f1"
  - "sql13.dts.designer.dataflowwindow.f1"
  - "sql13.dts.designer.eventhandlerwindow.f1"
  - "sql13.dts.designer.treeview.f1"
  - "sql13.dts.designer.progress.f1"
  - "sql13.dts.designer.connectionstray.f1"
helpviewer_keywords: 
  - "SQL Server Integration Services, SSIS-Designer"
  - "Business Intelligence Development Studio, Integration Services in"
  - "Tools [Integration Services], SSIS-Designer"
  - "SSIS, SSIS-Designer"
  - "SSIS-Designer, Informationen zum SSIS-Designer"
  - "Integration Services, SSIS-Designer"
ms.assetid: 006d68ea-1b5c-4c1e-8079-3910288e012c
caps.latest.revision: 59
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 58
---
# SSIS-Designer
  [!INCLUDE[ssIS](../includes/ssis-md.md)] Designer ist ein grafisches Tool, mit dem Sie [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Pakete erstellen und verwalten können. [!INCLUDE[ssIS](../includes/ssis-md.md)] Designer ist in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] im Rahmen eines [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Projekts verfügbar.  
  
 Mit dem [!INCLUDE[ssIS](../includes/ssis-md.md)]-Designer können die folgenden Aufgaben ausgeführt werden:  
  
-   Erstellen der Ablaufsteuerung in einem Paket.  
  
-   Erstellen der Datenflüsse in einem Paket.  
  
-   Hinzufügen von Ereignishandlern zum Paket und zu Paketobjekten.  
  
-   Anzeigen des Paketinhalts.  
  
-   Zur Laufzeit, Anzeigen des Ausführungsstatus des Pakets.  
  
 Im folgenden Diagramm werden der [!INCLUDE[ssIS](../includes/ssis-md.md)]-Designer und das Fenster **Toolbox** angezeigt.  
  
 ![Screenshot von SSIS-Designer und -Toolbox](../integration-services/media/denali-designerandtoolbox.gif "Screenshot von SSIS-Designer und -Toolbox")  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] enthält zusätzliche Dialogfelder und Fenster, um Paketen Funktionalität hinzuzufügen, und [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] stellt Fenster und Dialogfelder zum Konfigurieren der Entwicklungsumgebung und zum Verwenden von Paketen bereit. Weitere Informationen finden Sie unter [SQL Server Integration Services-Benutzeroberfläche](../integration-services/integration-services-user-interface.md).  
  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] Designer ist nicht vom [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Dienst abhängig (der Dienst, mit dem Pakete verwaltet und überwacht werden), und der Dienst muss nicht ausgeführt werden, um Pakete im [!INCLUDE[ssIS](../includes/ssis-md.md)]-Designer zu erstellen oder zu ändern. Wenn Sie jedoch den Dienst beenden, während der [!INCLUDE[ssIS](../includes/ssis-md.md)]-Designer geöffnet ist, können Sie die Dialogfelder des [!INCLUDE[ssIS](../includes/ssis-md.md)]-Designers nicht mehr öffnen und möglicherweise wird die Fehlermeldung „Der RPC-Server ist nicht verfügbar“ angezeigt. Sie müssen den Designer schließen, [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] beenden und anschließend [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], das [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Projekt und das Paket öffnen, um den [!INCLUDE[ssIS](../includes/ssis-md.md)]-Designer zurückzusetzen und die Verwendung des Pakets fortzusetzen.  
  
## Rückgängig machen und Wiederholen  
 Sie können bis zu 20 Aktionen im [!INCLUDE[ssIS](../includes/ssis-md.md)]-Designer rückgängig machen und wiederholen. Bei Paketen ist Rückgängig/Wiederholen auf den Registerkarten **Ablaufsteuerung**, **Datenfluss**, **Ereignishandler** und **Parameter** sowie im Fenster **Variablen** verfügbar. Bei Projekten ist Rückgängig/Wiederholen im Fenster **Projektparameter** verfügbar.  
  
 An der neuen **SSIS-Toolbox** können Sie keine Rückgängig/Wiederholen-Änderungen vornehmen.  
  
 Wenn Sie Änderungen an einer Komponente vornehmen, für die der Komponenten-Editor verwendet wird, können Sie Änderungen gruppenweise statt einzeln rückgängig machen und wiederholen. Die Gruppe von Änderungen wird in der Dropdownliste zum Rückgängigmachen und Wiederholen als einzelne Aktion angezeigt.  
  
 Klicken Sie auf die Symbolleistenschaltfläche „Rückgängig“, auf das Menüelement **Bearbeiten/Rückgängig** oder drücken Sie STRG+Z, um eine Aktion rückgängig zu machen. Klicken Sie auf die Symbolleistenschaltfläche „Wiederholen“, auf das Menüelement **Bearbeiten/Wiederholen** oder drücken Sie STRG+Y, um eine Aktion zu wiederholen. Sie können mehrere Aktionen rückgängig machen und wiederholen, indem Sie auf den Pfeil neben der Symbolleistenschaltfläche klicken, um mehrere Aktionen in der Dropdownliste zu markieren, und anschließend in der Liste klicken.  
  
## Teile des SSIS-Designers  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] Designer weist fünf ständig angezeigte Registerkarten auf, nämlich je eine Registerkarte zum Erstellen der Paketablaufsteuerung, der Datenflüsse, der Parameter und der Ereignishandler sowie eine Registerkarte zum Anzeigen der Inhalte eines Pakets. Zur Laufzeit wird eine sechste Registerkarte angezeigt, auf der der Ausführungsstatus eines ausgeführten Pakets und nach Beendigung des Pakets die Ausführungsergebnisse angezeigt werden.  
  
 Darüber hinaus enthält der [!INCLUDE[ssIS](../includes/ssis-md.md)]-Designer den Verbindungs-Manager-Bereich zum Hinzufügen und Konfigurieren der Verbindungs-Manager, die von einem Paket zum Herstellen einer Verbindung mit Daten verwendet werden.  
  
### Ablaufsteuerung (Registerkarte)  
 Die Ablaufsteuerung in einem Paket erstellen Sie in der Entwurfsoberfläche der Registerkarte **Ablaufsteuerung**. Ziehen Sie Elemente aus dem Fenster **Toolbox** auf die Entwurfsoberfläche, und verbinden Sie sie zu einer Ablaufsteuerung. Klicken Sie dazu auf das Elementsymbol, und ziehen Sie den Pfeil von einem Element zum anderen.  
  
 Weitere Informationen finden Sie unter [Control Flow](../integration-services/control-flow/control-flow.md).  
  
### Datenfluss (Registerkarte)  
 Falls ein Paket einen Datenflusstask enthält, können Sie dem Paket Datenflüsse hinzufügen. Die Datenflüsse in einem Paket erstellen Sie in der Entwurfsoberfläche der Registerkarte **Datenfluss**. Ziehen Sie Elemente aus dem Fenster **Toolbox** auf die Entwurfsoberfläche, und verbinden Sie sie zu einem Datenfluss. Klicken Sie dazu auf das Elementsymbol, und ziehen Sie den Pfeil von einem Element zum anderen.  
  
 Weitere Informationen finden Sie unter [Data Flow](../integration-services/data-flow/data-flow.md).  
  
### Parameter (Registerkarte)  
 Mit Integration Services-Parametern (SSIS) können Sie Eigenschaften in Paketen zur Zeit der Paketausführung Werte zuweisen. Sie können Projektparameter auf Projektebene und Paketparameter auf Paketebene erstellen. Projektparameter werden verwendet, um jegliche externen Eingaben bereitzustellen, die das Projekt für ein oder mehrere Pakete im Projekt empfängt. Mit Paketparametern können Sie die Paketausführung ändern, ohne das Paket bearbeiten und erneut bereitstellen zu müssen. Mit dieser Registerkarte können Sie Paketparameter verwalten.  
  
 Weitere Informationen zu Parametern finden Sie unter [Integration Services-Parameter (SSIS)](https://msdn.microsoft.com/library/hh213214.aspx).  
  
> **WICHTIG!**  Parameter sind nur für Projekte verfügbar, die für das Projektbereitstellungsmodell entwickelt wurden. Daher sehen Sie die Registerkarte "Parameter" nur für Pakete, die ein Teil eines Projekts sind, das für die Verwendung des Projektbereitstellungsmodells konfiguriert wurde.  
  
### Registerkarte Ereignishandler  
 Die Ereignisse in einem Paket erstellen Sie in der Entwurfsoberfläche der Registerkarte **Ereignishandler**. Wählen Sie auf der Registerkarte **Ereignishandler** das Paket oder das Paketobjekt aus, für das Sie einen Ereignishandler erstellen möchten, und wählen Sie anschließend das Ereignis aus, das dem Ereignishandler zugeordnet werden soll. Ein Ereignishandler weist eine Ablaufsteuerung und optional Datenflüsse auf.  
  
 Weitere Informationen finden Sie unter [Hinzufügen eines Ereignishandlers zu einem Paket](../Topic/Add%20an%20Event%20Handler%20to%20a%20Package.md).  
  
### Registerkarte Paket-Explorer  
 Pakete können komplex sein und viele Tasks, Verbindungs-Manager, Variablen und sonstige Elemente einschließen. Im Paket-Explorer wird eine vollständige Liste der Paketelemente angezeigt.  
  
 Weitere Informationen finden Sie unter [Anzeigen von Paketobjekten](../integration-services/view-package-objects.md).  
  
#### Status/Ausführungsergebnisse (Registerkarten)  
 Während ein Paket ausgeführt wird, wird auf der Registerkarte **Status** der Ausführungsstatus des Pakets angezeigt. Wenn die Ausführung des Pakets beendet wurde, sind die Ausführungsergebnisse weiterhin auf der Registerkarte **Ausführungsergebnisse** verfügbar.  
  
> **HINWEIS:** Zum Aktivieren bzw. Deaktivieren der Anzeige von Meldungen auf der Registerkarte **Status** schalten Sie die Option **Debug-Statusbericht** im Menü **SSIS** um.  
  
##### Verbindungs-Manager (Bereich)  
 Die Verbindungs-Manager, die ein Paket verwendet, können Sie im Bereich **Verbindungs-Manager** hinzufügen und ändern. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] enthält Verbindungs-Manager zum Herstellen von Verbindungen mit verschiedenen Datenquellen, beispielsweise mit Textdateien, OLE DB-Datenbanken und .NET-Providern.  
  
 Weitere Informationen finden Sie unter [Integration Services-Verbindungen &#40;SSIS&#41;](../integration-services/connection-manager/integration-services-ssis-connections.md) und [Erstellen von Verbindungs-Managern](../Topic/Create%20Connection%20Managers.md).  
  
## Verwandte Aufgaben  
  
-   [Erstellen von Paketen in SQL Server-Datentools](../integration-services/create-packages-in-sql-server-data-tools.md)  
  
## Siehe auch  
 [SQL Server Integration Services-Benutzeroberfläche](../integration-services/integration-services-user-interface.md)  
  
  