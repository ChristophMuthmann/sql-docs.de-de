---
title: "WMI-Ereignis&#252;berwachung (Task) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.wmieventwatchertask.f1"
helpviewer_keywords: 
  - "WQL [Integration Services]"
  - "WMI-Ereignisüberwachung (Task) [Integration Services]"
ms.assetid: b5bb52e9-a77e-41e1-93f9-d4c3bc6b2c9a
caps.latest.revision: 53
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 53
---
# WMI-Ereignis&#252;berwachung (Task)
  Der Task "WMI-Ereignisüberwachung" überwacht ein WMI-Ereignis (Windows Management Instrumentation) mithilfe einer WQL-Ereignisabfrage (Windows Management Instrumentation Query Language), um relevante Ereignisse anzugeben. Der Task WMI-Ereignisüberwachung kann für folgende Zwecke verwendet werden:  
  
-   Warten auf die Benachrichtigung, dass Dateien einem Ordner hinzugefügt wurden, und dann Initiieren der Dateiverarbeitung.  
  
-   Ausführen eines Pakets, mit dem Dateien gelöscht werden, wenn der verfügbare Arbeitsspeicher auf einem Server unter einen angegebenen Prozentsatz sinkt.  
  
-   Überwachen der Installation einer Anwendung und dann Ausführen eines Pakets, das die Anwendung verwendet.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] enthält einen Task, der WMI-Informationen liest.  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zu diesem Task zu erhalten:  
  
-   [WMI-Datenleser (Task)](../../integration-services/control-flow/wmi-data-reader-task.md)  
  
## WQL-Abfragen  
 WQL ist ein Dialekt von SQL mit Erweiterungen zur Unterstützung der WMI-Ereignisbenachrichtigung und sonstigen WMI-spezifischen Funktionen. Weitere Informationen zu WQL finden Sie in der WMI-Dokumentation in der [MSDN Library](http://go.microsoft.com/fwlink/?linkid=62553).  
  
> [!NOTE]  
>  Die WMI-Klassen variieren in den verschiedenen Windows-Versionen.  
  
 Die folgende Abfrage überwacht die Benachrichtigung, dass die CPU-Nutzung über 40 % beträgt.  
  
```  
SELECT * from __InstanceModificationEvent WITHIN 2 WHERE TargetInstance ISA 'Win32_Processor' and TargetInstance.LoadPercentage > 40  
```  
  
 Die folgende Abfrage überwacht die Benachrichtigung, dass einem Ordner eine Datei hinzugefügt wurde.  
  
```  
SELECT * FROM __InstanceCreationEvent WITHIN 10 WHERE TargetInstance ISA "CIM_DirectoryContainsFile" and TargetInstance.GroupComponent= "Win32_Directory.Name=\"c:\\\\WMIFileWatcher\""   
```  
  
## Verfügbare benutzerdefinierte Meldungen für die Protokollierung für den Task "WMI-Ereignisüberwachung"  
 In der folgenden Tabelle werden die benutzerdefinierten Protokolleinträge für den Task WMI-Ereignisüberwachung aufgelistet. Weitere Informationen finden Sie unter [Integration Services-Protokollierung &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md) und [Benutzerdefinierte Meldungen für die Protokollierung](../../integration-services/performance/custom-messages-for-logging.md).  
  
|Protokolleintrag|Description|  
|---------------|-----------------|  
|**WMIEventWatcherEventOccurred**|Zeigt an, dass ein vom Task überwachtes Ereignis aufgetreten ist.|  
|**WMIEventWatcherTimedout**|Zeigt an, dass beim Task ein Timeout eingetreten ist.|  
|**WMIEventWatcherWatchingForWMIEvents**|Zeigt an, dass die Ausführung der WQL-Abfrage begonnen wurde. Der Eintrag schließt die Abfrage ein.|  
  
## Konfiguration des Tasks "WMI-Ereignisüberwachung"  
 Es gibt folgende Möglichkeiten, um den Task WMI-Datenleser zu konfigurieren:  
  
-   Geben Sie den zu verwendenden WMI-Verbindungs-Manager an.  
  
-   Geben Sie die Quelle der WQL-Abfrage an. Die Quelle kann extern zum Task oder eine Variable bzw. Datei sein, die Abfrage kann aber auch in einer Taskeigenschaft gespeichert sein.  
  
-   Geben Sie die Aktion an, die der Task ausführt, wenn das WMI-Ereignis auftritt. Sie können die Ereignisbenachrichtigung und den Status nach dem Ereignis protokollieren oder benutzerdefinierte [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Ereignisse auslösen, die Informationen zum WMI-Ereignis, zur Benachrichtigung und zum Status nach dem Ereignis bereitstellen.  
  
-   Definieren Sie, wie der Task auf das Ereignis antwortet. Der Task kann je nach Ereignis erfolgreich ausgeführt werden oder einen Fehler melden, der Task kann aber auch lediglich das Ereignis erneut überwachen.  
  
-   Geben Sie die Aktion an, die der Task bei einem Timeout der WMI-Abfrage ausführt. Sie können das Timeout und den Status nach dem Timeout protokollieren oder aber ein benutzerdefiniertes [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Ereignis mit dem Hinweis, dass beim WMI-Ereignis ein Timeout aufgetreten ist, auslösen und das Timeout und den Timeoutstatus protokollieren.  
  
-   Definieren Sie, wie der Task auf das Timeout antwortet. Der Task kann erfolgreich ausgeführt werden oder einen Fehler melden, der Task kann aber auch lediglich das Ereignis erneut überwachen.  
  
-   Geben Sie an, wie oft der Task das Ereignis überwacht.  
  
-   Geben Sie das Timeout an.  
  
 Falls die Quelle eine Datei ist, verwendet der Task WMI-Ereignisüberwachung einen Dateiverbindungs-Manager zum Herstellen einer Verbindung mit der Datei. Weitere Informationen finden Sie unter [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
 Der Task "WMI-Ereignisüberwachung" verwendet einen WMI-Verbindungs-Manager zum Herstellen einer Verbindung mit dem Server, von dem er WMI-Informationen liest. Weitere Informationen finden Sie unter [WMI Connection Manager](../../integration-services/connection-manager/wmi-connection-manager.md).  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [Editor für den Task „WMI-Ereignisüberwachung“ &#40;Seite „Allgemein“&#41;](../../integration-services/control-flow/wmi-event-watcher-task-editor-general-page.md)  
  
-   [Editor für den Task „WMI-Ereignisüberwachung“ &#40;Seite „WMI-Optionen“&#41;](../../integration-services/control-flow/wmi-event-watcher-task-editor-wmi-options-page.md)  
  
-   [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum Festlegen dieser Eigenschaften im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer zu erhalten:  
  
-   [Festlegen der Eigenschaften eines Tasks oder Containers](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
## Programmgesteuerte Konfiguration des Tasks "WMI-Ereignisüberwachung"  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum programmgesteuerten Festlegen dieser Eigenschaften anzuzeigen:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WmiEventWatcherTask.WmiEventWatcherTask>  
  
  