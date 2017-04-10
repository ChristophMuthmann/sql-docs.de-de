---
title: "Debuggen der Ablaufsteuerung | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Fortschrittsberichterstellung [Integration Services]"
  - "Breakpoints [Integration Services]"
  - "Debuggen [Integration Services], Ablaufsteuerung"
  - "Ablaufsteuerung [Integration Services], Debuggen"
  - "Farbcodierung in der Fortschrittsberichterstellung [Integration Services]"
  - "Breakpoints festlegen (Dialogfeld)"
ms.assetid: 54a458cc-9f4f-4b48-8cf2-db2e0fa7756c
caps.latest.revision: 54
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 54
---
# Debuggen der Ablaufsteuerung
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] und [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] include features und tools that you can use to troubleshoot the control flow in an [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket behandeln können.  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] unterstützt Breakpoints für Container und Tasks.  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer stellt zur Laufzeit Fortschrittsberichte bereit.  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] stellt Debugfenster bereit.  
  
## Breakpoints  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer stellt das Dialogfeld **Breakpoints festlegen** bereit, in dem Sie Breakpoints festlegen können. Hierzu aktivieren Sie Unterbrechungsbedingungen und geben an, wie häufig ein Breakpoint auftreten kann, bevor die Ausführung des Pakets angehalten wird. Breakpoints können auf Paketebene oder auf der Ebene der einzelnen Komponenten aktiviert werden. Falls Unterbrechungsbedingungen auf der Task- oder Containerebene aktiviert sind, wird das Breakpointsymbol neben dem Task oder Container auf der Entwurfsoberfläche der Registerkarte **Ablaufsteuerung** angezeigt. Falls die Unterbrechungsbedingungen im Paket aktiviert sind, wird das Breakpointsymbol in der Bezeichnung der Registerkarte **Ablaufsteuerung** angezeigt.  
  
 Wird ein Breakpoint erreicht, ändert sich das Breakpointsymbol, damit Sie die Quelle des Breakpoints identifizieren können. Sie können beim Ausführen des Pakets Breakpoints hinzufügen, löschen und ändern.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] stellt zehn Unterbrechungsbedingungen bereit, die Sie für alle Tasks und Container aktivieren können. Im Dialogfeld **Breakpoints festlegen** können Sie Breakpoints für die folgenden Bedingungen aktivieren:  
  
|Unterbrechungsbedingung|Description|  
|---------------------|-----------------|  
|Wenn der Task oder Container das **OnPreExecute** -Ereignis empfängt.|Wird aufgerufen, unmittelbar bevor ein Task ausgeführt wird. Dieses Ereignis wird durch einen Task oder Container ausgelöst, unmittelbar bevor er ausgeführt wird.|  
|Wenn der Task oder Container das **OnPostExecute** -Ereignis empfängt.|Wird aufgerufen, unmittelbar nachdem die Ausführungslogik des Tasks beendet wurde. Dieses Ereignis wird durch einen Task oder Container ausgelöst, unmittelbar nachdem er ausgeführt wurde.|  
|Wenn der Task oder Container das **OnError** -Ereignis empfängt.|Wird durch einen Task oder Container bei einem Fehler aufgerufen.|  
|Wenn der Task oder Container das **OnWarning** -Ereignis empfängt.|Wird aufgerufen, wenn der Task einen Status aufweist, der keinen Fehler, aber eine Warnung rechtfertigt.|  
|Wenn der Task oder Container das **OnInformation** -Ereignis empfängt.|Wird aufgerufen, wenn der Task Informationen bereitstellen muss.|  
|Wenn der Task oder Container das **OnTaskFailed** -Ereignis empfängt.|Wird durch den Taskhost bei einem Fehler aufgerufen.|  
|Wenn der Task oder Container das **OnProgress** -Ereignis empfängt.|Wird aufgerufen, um den Status der Taskausführung zu aktualisieren.|  
|Wenn der Task oder Container das **OnQueryCancel** -Ereignis empfängt.|Wird zu einem beliebigen Zeitpunkt der Taskverarbeitung aufgerufen, wenn Sie die Ausführung abbrechen.|  
|Wenn der Task oder Container das **OnVariableValueChanged** -Ereignis empfängt.|Wird durch die [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Laufzeit aufgerufen, wenn sich der Wert einer Variablen ändert. Das RaiseChangeEvent der Variablen muss auf **TRUE** festgelegt werden, damit dieses Ereignis ausgelöst wird.<br /><br /> **\*\* Warnung \*\*** Die diesem Breakpoint zugeordnete Variable muss im **Containerbereich** definiert werden. Wenn die Variable im Paketbereich definiert wird, wird der Breakpoint nicht erreicht.|  
|Wenn der Task oder Container das **OnCustomEvent** -Ereignis empfängt.|Wird durch Tasks aufgerufen, um benutzerdefinierte Taskereignisse auszulösen.|  
  
 Neben den Unterbrechungsbedingungen, die für alle Tasks und Container verfügbar sind, enthalten manche Tasks und Container spezielle Unterbrechungsbedingungen zum Festlegen von Breakpoints. Beispielsweise können Sie eine Unterbrechungsbedingung für den For-Schleifencontainer aktivieren, um einen Breakpoint festzulegen, der die Ausführung zu Beginn jeder Iteration der Schleife anhält.  
  
 Wenn Sie einen Breakpoint flexibler und leistungsfähiger gestalten möchten, können Sie dessen Verhalten durch Angeben der folgenden Optionen ändern:  
  
-   Die Trefferanzahl oder die Angabe, oder nach dem wievielten Auftreten einer Unterbrechungsbedingung die Ausführung angehalten wird.  
  
-   Den Typ der Trefferanzahl oder die Regel, die angibt, wann die Unterbrechungsbedingung den Breakpoint auslöst.  
  
 Die Typen der Trefferanzahl, mit Ausnahme des Typs Immer, werden durch die Trefferanzahl weiter definiert. Beispielsweise wird beim Typ "Trefferanzahl ist gleich" und der Trefferanzahl 5 die Ausführung angehalten, wenn die Unterbrechungsbedingung das sechste Mal auftritt.  
  
 In der folgenden Tabelle sind die Typen der Trefferanzahl aufgeführt.  
  
|Typ der Trefferanzahl|Description|  
|--------------------|-----------------|  
|Always|Die Ausführung wird immer angehalten, wenn der Breakpoint erreicht wird.|  
|Trefferanzahl ist gleich|Die Ausführung wird angehalten, wenn die Anzahl des Auftretens des Breakpoints der Trefferanzahl entspricht.|  
|Trefferanzahl ist größer als oder gleich|Die Ausführung wird angehalten, wenn die Anzahl des Auftretens des Breakpoints mindestens so groß wie die Trefferanzahl ist.|  
|Trefferanzahl mehrfach|Die Ausführung wird angehalten, wenn ein Mehrfaches der Trefferanzahl erreicht wird. Wenn Sie z. B. diese Option auf 5 festlegen, wird die Ausführung bei jedem fünften Mal angehalten.|  
  
#### So legen Sie Breakpoints fest  
  
-   [Debuggen eines Pakets durch Festlegen von Breakpoints auf einem Task oder Container](../../integration-services/troubleshooting/debug-a-package-by-setting-breakpoints-on-a-task-or-a-container.md)  
  
## Fortschrittsberichte  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer enthält zwei Arten von Fortschrittsberichten: Farbcodierung auf der Entwurfsoberfläche der Registerkarte **Ablaufsteuerung** und Statusmeldungen auf der Registerkarte **Status**.  
  
 Wenn Sie ein Paket ausführen, wird der Ausführungsstatus im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer gekennzeichnet, indem jeder Task oder Container in einer Farbe angezeigt wird, die Ausschluss über den Ausführungsstatus gibt. Anhand der Farbe wissen Sie, ob das Element auf die Ausführung wartet, zurzeit ausgeführt wird, erfolgreich ausgeführt wurde oder nicht erfolgreich beendet wurde. Nachdem Sie die Paketausführung beendet haben, verschwindet die Farbcodierung.  
  
 In der folgenden Tabelle werden die Farben beschrieben, die zum Kennzeichnen des Ausführungsstatus verwendet werden.  
  
|Farbe|Ausführungsstatus|  
|-----------|----------------------|  
|Grau|Wartet auf die Ausführung|  
|Gelb|Wird ausgeführt|  
|Green|Wurde erfolgreich ausgeführt|  
|Hervorgehoben|Wurde mit Fehlern ausgeführt|  
  
 Auf der Registerkarte **Status** werden Tasks und Container in der Ausführungsreihenfolge aufgeführt. Diese Registerkarte enthält außerdem die Start- und Beendigungszeiten, Warnungen und Fehlermeldungen. Wenn die Ausführung des Pakets beendet wurde, sind die Statusinformationen weiterhin auf der Registerkarte **Ausführungsergebnisse** verfügbar.  
  
> [!NOTE]  
>  Zum Aktivieren bzw. Deaktivieren der Anzeige von Meldungen auf der Registerkarte **Status** schalten Sie die Option **Debug-Statusbericht** im Menü **SSIS** um.  
  
 Im folgenden Diagramm wird die Registerkarte **Status** angezeigt.  
  
 ![Status (Registerkarte) des SSIS-Designers](../../integration-services/troubleshooting/media/mw-dtsflow04.gif "Status (Registerkarte) des SSIS-Designers")  
  
## Debugfenster  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] enthält viele Fenster, in denen Sie Breakpoints verwenden und Pakete, die Breakpoints enthalten, debuggen können. Um weitere Informationen zu den einzelnen Fenstern zu erhalten, öffnen Sie das entsprechende Fenster, und drücken Sie F1, um die zugehörige Hilfe anzuzeigen.  
  
 Zeigen Sie zum Öffnen dieser Fenster in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]im Menü **Debuggen** auf **Fenster**, und klicken Sie dann auf **Breakpoints**, **Ausgabe**oder **Direkt**.  
  
 In der folgenden Tabelle sind diese Fenster beschrieben.  
  
|Fenster|Description|  
|------------|-----------------|  
|Breakpoints|Listet die Breakpoints in einem Paket auf und stellt Optionen zum Aktivieren und Löschen von Breakpoints bereit.|  
|Ausgabe|Zeigt Statusmeldungen für Funktionen in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]an.|  
|Direkt|Wird zum Debuggen und Auswerten von Ausdrücken und zum Drucken von Variablenwerten verwendet.|  
  
## Siehe auch  
 [Tools zur Problembehandlung für die Paketentwicklung](../../integration-services/troubleshooting/troubleshooting-tools-for-package-development.md)  
  
  