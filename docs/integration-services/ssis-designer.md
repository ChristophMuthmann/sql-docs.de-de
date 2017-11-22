---
title: SSIS-Designer | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/31/2016
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.controlflowwindow.f1
- sql13.dts.designer.dataflowwindow.f1
- sql13.dts.designer.eventhandlerwindow.f1
- sql13.dts.designer.treeview.f1
- sql13.dts.designer.progress.f1
- sql13.dts.designer.connectionstray.f1
helpviewer_keywords:
- SQL Server Integration Services, SSIS Designer
- Business Intelligence Development Studio, Integration Services in
- tools [Integration Services], SSIS Designer
- SSIS, SSIS Designer
- SSIS Designer, about SSIS Designer
- Integration Services, SSIS Designer
ms.assetid: 006d68ea-1b5c-4c1e-8079-3910288e012c
caps.latest.revision: "59"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 1b132be5de44e4bb669ce0c1aa014b89aec07a63
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="ssis-designer"></a>SSIS-Designer
  [!INCLUDE[ssIS](../includes/ssis-md.md)] Designer ist ein grafisches Tool, mit dem Sie [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Pakete erstellen und verwalten können. [!INCLUDE[ssIS](../includes/ssis-md.md)] Designer ist in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] im Rahmen eines [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekts verfügbar.  
  
 Mit dem [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designer können die folgenden Aufgaben ausgeführt werden:  
  
-   Erstellen der Ablaufsteuerung in einem Paket.  
  
-   Erstellen der Datenflüsse in einem Paket.  
  
-   Hinzufügen von Ereignishandlern zum Paket und zu Paketobjekten.  
  
-   Anzeigen des Paketinhalts.  
  
-   Zur Laufzeit, Anzeigen des Ausführungsstatus des Pakets.  
  
 Im folgenden Diagramm werden der [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designer und das Fenster **Toolbox** angezeigt.  
  
 ![Screenshot des SSIS-Designers und der Toolbox](../integration-services/media/denali-designerandtoolbox.gif "Screenshot of SSIS Designer and Toolbox")  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] enthält zusätzliche Dialogfelder und Fenster, um Paketen Funktionalität hinzuzufügen, und [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] stellt Fenster und Dialogfelder zum Konfigurieren der Entwicklungsumgebung und zum Verwenden von Paketen bereit. Weitere Informationen finden Sie unter [SQL Server Integration Services-Benutzeroberfläche](../integration-services/integration-services-user-interface.md).  
  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] Designer ist nicht vom [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Dienst abhängig (der Dienst, mit dem Pakete verwaltet und überwacht werden), und der Dienst muss nicht ausgeführt werden, um Pakete im [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designer zu erstellen oder zu ändern. Wenn Sie jedoch den Dienst beenden, während der [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designer geöffnet ist, können Sie die Dialogfelder des [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designers nicht mehr öffnen und möglicherweise wird die Fehlermeldung „Der RPC-Server ist nicht verfügbar“ angezeigt. Sie müssen den Designer schließen, [!INCLUDE[ssIS](../includes/ssis-md.md)] beenden und anschließend [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], das [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]-Projekt und das Paket öffnen, um den [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Designer zurückzusetzen und die Verwendung des Pakets fortzusetzen.  
  
## <a name="undo-and-redo"></a>Rückgängig machen und Wiederholen  
 Sie können bis zu 20 Aktionen im [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designer rückgängig machen und wiederholen. Bei Paketen ist Rückgängig/Wiederholen auf den Registerkarten **Ablaufsteuerung**, **Datenfluss**, **Ereignishandler**und **Parameter** sowie im Fenster **Variablen** verfügbar. Bei Projekten ist Rückgängig/Wiederholen im Fenster **Projektparameter** verfügbar.  
  
 An der neuen **SSIS-Toolbox**können Sie keine Rückgängig/Wiederholen-Änderungen vornehmen.  
  
 Wenn Sie Änderungen an einer Komponente vornehmen, für die der Komponenten-Editor verwendet wird, können Sie Änderungen gruppenweise statt einzeln rückgängig machen und wiederholen. Die Gruppe von Änderungen wird in der Dropdownliste zum Rückgängigmachen und Wiederholen als einzelne Aktion angezeigt.  
  
 Klicken Sie auf die Symbolleistenschaltfläche „Rückgängig“, auf das Menüelement **Bearbeiten/Rückgängig** oder drücken Sie STRG+Z, um eine Aktion rückgängig zu machen. Klicken Sie auf die Symbolleistenschaltfläche „Wiederholen“, auf das Menüelement **Bearbeiten/Wiederholen** oder drücken Sie STRG+Y, um eine Aktion zu wiederholen. Sie können mehrere Aktionen rückgängig machen und wiederholen, indem Sie auf den Pfeil neben der Symbolleistenschaltfläche klicken, um mehrere Aktionen in der Dropdownliste zu markieren, und anschließend in der Liste klicken.  
  
## <a name="parts-of-the-ssis-designer"></a>Teile des SSIS-Designers  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] Designer weist fünf ständig angezeigte Registerkarten auf, nämlich je eine Registerkarte zum Erstellen der Paketablaufsteuerung, der Datenflüsse, der Parameter und der Ereignishandler sowie eine Registerkarte zum Anzeigen der Inhalte eines Pakets. Zur Laufzeit wird eine sechste Registerkarte angezeigt, auf der der Ausführungsstatus eines ausgeführten Pakets und nach Beendigung des Pakets die Ausführungsergebnisse angezeigt werden.  
  
 Darüber hinaus enthält der [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designer den Verbindungs-Manager-Bereich zum Hinzufügen und Konfigurieren der Verbindungs-Manager, die von einem Paket zum Herstellen einer Verbindung mit Daten verwendet werden.  
  
### <a name="control-flow-tab"></a>Ablaufsteuerung (Registerkarte)  
 Die Ablaufsteuerung in einem Paket erstellen Sie in der Entwurfsoberfläche der Registerkarte **Ablaufsteuerung** . Ziehen Sie Elemente aus dem Fenster **Toolbox** auf die Entwurfsoberfläche, und verbinden Sie sie zu einer Ablaufsteuerung. Klicken Sie dazu auf das Elementsymbol, und ziehen Sie den Pfeil von einem Element zum anderen.  
  
 Weitere Informationen finden Sie unter [Control Flow](../integration-services/control-flow/control-flow.md).  
  
### <a name="data-flow-tab"></a>Datenfluss (Registerkarte)  
 Falls ein Paket einen Datenflusstask enthält, können Sie dem Paket Datenflüsse hinzufügen. Die Datenflüsse in einem Paket erstellen Sie in der Entwurfsoberfläche der Registerkarte **Datenfluss** . Ziehen Sie Elemente aus dem Fenster **Toolbox** auf die Entwurfsoberfläche, und verbinden Sie sie zu einem Datenfluss. Klicken Sie dazu auf das Elementsymbol, und ziehen Sie den Pfeil von einem Element zum anderen.  
  
 Weitere Informationen finden Sie unter [Data Flow](../integration-services/data-flow/data-flow.md).  
  
### <a name="parameters-tab"></a>Parameter (Registerkarte)  
 Mit Integration Services-Parametern (SSIS) können Sie Eigenschaften in Paketen zur Zeit der Paketausführung Werte zuweisen. Sie können Projektparameter auf Projektebene und Paketparameter auf Paketebene erstellen. Projektparameter werden verwendet, um jegliche externen Eingaben bereitzustellen, die das Projekt für ein oder mehrere Pakete im Projekt empfängt. Mit Paketparametern können Sie die Paketausführung ändern, ohne das Paket bearbeiten und erneut bereitstellen zu müssen. Mit dieser Registerkarte können Sie Paketparameter verwalten.  
  
 Weitere Informationen zu Parametern finden Sie unter [Integration Services-Parameter (SSIS)](integration-services-ssis-package-and-project-parameters.md).  
  
> **WICHTIG!**  Parameter sind nur für Projekte verfügbar, die für das Projektbereitstellungsmodell entwickelt wurden. Daher sehen Sie die Registerkarte "Parameter" nur für Pakete, die ein Teil eines Projekts sind, das für die Verwendung des Projektbereitstellungsmodells konfiguriert wurde.  
  
### <a name="event-handlers-tab"></a>Registerkarte Ereignishandler  
 Die Ereignisse in einem Paket erstellen Sie in der Entwurfsoberfläche der Registerkarte **Ereignishandler** . Wählen Sie auf der Registerkarte **Ereignishandler** das Paket oder das Paketobjekt aus, für das Sie einen Ereignishandler erstellen möchten, und wählen Sie anschließend das Ereignis aus, das dem Ereignishandler zugeordnet werden soll. Ein Ereignishandler weist eine Ablaufsteuerung und optional Datenflüsse auf.  
  
 Weitere Informationen finden Sie unter [Hinzufügen eines Ereignishandlers zu einem Paket](http://msdn.microsoft.com/library/5e56885d-8658-480a-bed9-3f2f8003fd78).  
  
### <a name="package-explorer-tab"></a>Registerkarte Paket-Explorer  
 Pakete können komplex sein und viele Tasks, Verbindungs-Manager, Variablen und sonstige Elemente einschließen. Im Paket-Explorer wird eine vollständige Liste der Paketelemente angezeigt.  
  
 Weitere Informationen finden Sie unter [Anzeigen von Paketobjekten](../integration-services/view-package-objects.md).  
  
### <a name="progressexecution-result-tab"></a>Status/Ausführungsergebnisse (Registerkarten)  
 Während ein Paket ausgeführt wird, wird auf der Registerkarte **Status** der Ausführungsstatus des Pakets angezeigt. Wenn die Ausführung des Pakets beendet wurde, sind die Ausführungsergebnisse weiterhin auf der Registerkarte **Ausführungsergebnisse** verfügbar.  
  
> **HINWEIS:** Zum Aktivieren bzw. Deaktivieren der Anzeige von Meldungen auf der Registerkarte **Status** schalten Sie die Option **Debug-Statusbericht** im Menü **SSIS** um.  
  
#### <a name="connection-managers-area"></a>Verbindungs-Manager (Bereich)  
 Die Verbindungs-Manager, die ein Paket verwendet, können Sie im Bereich **Verbindungs-Manager** hinzufügen und ändern. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] enthält Verbindungs-Manager zum Herstellen von Verbindungen mit verschiedenen Datenquellen, beispielsweise mit Textdateien, OLE DB-Datenbanken und .NET-Providern.  
  
 Weitere Informationen finden Sie unter [Integration Services-Verbindungen &#40;SSIS&#41;](../integration-services/connection-manager/integration-services-ssis-connections.md) und [Erstellen von Verbindungs-Managern](http://msdn.microsoft.com/library/6ca317b8-0061-4d9d-b830-ee8c21268345).  
 
## <a name="control-flow-tab"></a>Ablaufsteuerung (Registerkarte)
Verwenden Sie die Registerkarte **Ablaufsteuerung** des [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designers, um die Ablaufsteuerung eines [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Pakets zu erstellen.  
  
 Erstellen Sie die Ablaufsteuerung, indem Sie grafische – [!INCLUDE[ssIS](../includes/ssis-md.md)] -Tasks und -Container darstellende – Objekte aus der **Toolbox** auf die Entwurfsoberfläche der Registerkarte **Ablaufsteuerung** ziehen und die Objekte anschließend miteinander verbinden, indem Sie den Konnektor eines Objekts auf ein anderes ziehen. Jede Verbindungslinie stellt eine Rangfolgeneinschränkung dar, die die Reihenfolge angibt, in der die Tasks und Container ausgeführt werden.  
  
 Sie können den [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designer auch verwenden, um dem Paket die folgenden Funktionalitäten aus der Registerkarte **Ablaufsteuerung** hinzuzufügen:  
  
-   Implementieren der Protokollierung  
  
-   Erstellen von Paketkonfigurationen  
  
-   Signieren von Paketen mit einem Zertifikat  
  
-   Verwalten von Variablen  
  
-   Hinzufügen von Anmerkungen  
  
-   Konfigurieren von Breakpoints  
  
 Um diese Funktionen einzelnen Tasks und Containern in [!INCLUDE[ssIS](../includes/ssis-md.md)] hinzuzufügen, klicken Sie mit der rechten Maustaste auf das entsprechende Objekt auf der Entwurfsoberfläche, und wählen Sie dann die gewünschte Option.  
 
## <a name="data-flow-tab"></a>Datenfluss (Registerkarte)
Verwenden Sie die Registerkarte **Datenfluss** des [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designers, um Datenflüsse in einem [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Paket zu erstellen.  
  
 Erstellen Sie die Datenflüsse, indem Sie grafische – Datenquellen, Transformationen oder Datenziele darstellende – Objekte aus der **Toolbox** auf die Entwurfsoberfläche der Registerkarte **Datenfluss** ziehen und die Objekte anschließend miteinander verbinden, um Pfade zu erstellen, die die Transformationssequenz bestimmen.  
  
 Klicken Sie mit der rechten Maustaste auf einen Pfad, und klicken Sie dann auf **Daten-Viewer** , um Daten-Viewer hinzuzufügen, in denen Sie die Daten vor und nach dem jeweiligen Datenflussobjekt anzeigen können.  
  
 Sie können den [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designer auch verwenden, um dem Datenflussobjekt die folgenden Funktionalitäten aus der Registerkarte **Datenfluss** hinzuzufügen:  
  
-   Verwalten von Variablen  
  
-   Hinzufügen von Anmerkungen  
  
 Um diese [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designerfunktionen hinzuzufügen, klicken Sie mit der rechten Maustaste auf die Entwurfoberfläche, und wählen Sie dann die gewünschte Option.  
 
## <a name="event-handlers-tab"></a>Registerkarte Ereignishandler
  Verwenden Sie die Registerkarte **Ereignishandler** von [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designer zum Erstellen eines Steuerungsflusses in einem [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Paket. Ein Ereignishandler wird als Reaktion auf ein Ereignis ausgeführt, das von einem Paket, Task oder Container ausgelöst wird.  
  
## <a name="options"></a>enthalten  
 **Ausführbare Datei**  
 Wählen Sie die ausführbare Datei aus, für die Sie einen Ereignishandler erstellen möchten. Bei der ausführbaren Datei kann es sich um ein Paket, einen Task oder Container im Paket handeln.  
  
 **Ereignishandler**  
 Wählen Sie einen Typ von Ereignishandler aus. Erstellen Sie den Ereignishandler, indem Sie Elemente aus der **Toolbox**ziehen.  
  
 **Delete**  
 Wählen Sie einen Ereignishandler aus, und entfernen Sie ihn anschließend aus dem Paket, indem Sie auf **Löschen** klicken.  
  
 **Klicken Sie hier, um einen \<Ereignishandlername\> für die ausführbare Datei \<Name der ausführbaren Datei\> zu erstellen.**  
 Klicken Sie, um den Ereignishandler zu erstellen.  
  
 Erstellen Sie den Steuerungsfluss, indem Sie grafische Objekte, die [!INCLUDE[ssIS](../includes/ssis-md.md)] -Tasks und -Container darstellen, aus der **Toolbox** auf die Entwurfsoberfläche der Registerkarte **Ereignishandler** ziehen und diese Objekte dann verbinden, indem Sie Rangfolgeneinschränkungen zum Definieren der Ausführungssequenz verwenden.  
  
 Klicken Sie außerdem mit der rechten Maustaste auf die Entwurfsoberfläche, um Anmerkungen hinzuzufügen, und klicken Sie anschließend im Menü auf **Anmerkung hinzufügen**.  
 
## <a name="package-explorer-tab"></a>Registerkarte Paket-Explorer
Auf der Registerkarte **Paket-Explorer** des [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designers wird eine hierarchische Ansicht aller in einem Paket enthaltenen Elemente angezeigt: Konfigurationen, Verbindungen, Ereignishandler, ausführbare Objekte wie Tasks und Container, Protokollanbieter, Rangfolgeneinschränkungen und Variablen. Wenn das Paket einen Datenflusstask enthält, befindet sich auf der Registerkarte **Paket-Explorer** ein Knoten, der eine hierarchische Sicht der Datenflusskomponenten enthält.  
  
 Klicken Sie mit der rechten Maustaste auf das Paketelement und dann auf **Eigenschaften** , damit die Eigenschaften des Elements im Fenster **Eigenschaften** angezeigt werden. Oder klicken Sie auf **Löschen** , um das Element zu löschen. 
 
## <a name="progress-tab"></a>Status (Registerkarte)
Verwenden Sie die Registerkarte **Status** im [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designer, um den Status der Ausführung eines [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Pakets anzuzeigen, wenn Sie das Paket in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]ausführen. Die Registerkarte **Status** listet die Startzeit, die Beendigungszeit und die für die Überprüfung und Ausführung des Pakets und der enthaltenen ausführbaren Dateien verstrichene Zeit sowie sämtliche Informationen oder Warnungen für das Paket, Statusbenachrichtigungen, Informationen zum Erfolg oder Fehlschlagen des Pakets und sämtliche Fehlermeldungen, die bei der Ausführung des Pakets generiert wurden, auf.  
  
 Zum Aktivieren bzw. Deaktivieren der Anzeige von Meldungen auf der Registerkarte **Status** schalten Sie die Option **Debug-Statusbericht** im Menü **SSIS** um. Beim Ausführen eines komplexen Pakets in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]kann eine Deaktivierung der Statusberichterstellung zur Verbesserung der Leistung beitragen.  
  
 Nachdem die Ausführung des Pakets beendet wurde, wird die Registerkarte **Status** in die Registerkarte **Ausführungsergebnisse** umgewandelt.  
 
## <a name="connection-managers-area"></a>Verbindungs-Manager (Bereich)
Pakete verwenden Verbindungs-Manager, um Verbindungen mit Datenquellen, beispielsweise Dateien, relationalen Datenbanken oder Servern herzustellen.  
  
 Verwenden Sie den Bereich **Verbindungs-Manager** in [!INCLUDE[ssIS](../includes/ssis-md.md)] Designer zum Hinzufügen, Löschen, Ändern, Umbenennen sowie zum Kopieren und Einfügen der Verbindungs-Manager.  
  
 Klicken Sie mit der rechten Maustaste in diesen Bereich, und klicken Sie dann im Menü auf die Option für den Task, den Sie ausführen möchten.
 
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
-   [Erstellen von Paketen in SQL Server-Datentools](../integration-services/create-packages-in-sql-server-data-tools.md)  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Integration Services-Benutzeroberfläche](../integration-services/integration-services-user-interface.md)  
  
  
