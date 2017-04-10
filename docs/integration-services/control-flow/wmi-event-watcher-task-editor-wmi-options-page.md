---
title: "Editor f&#252;r den Task &#39;WMI-Ereignis&#252;berwachung&#39; (Seite WMI-Optionen) | Microsoft Docs"
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
  - "sql13.dts.designer.wmieventwatcher.wmiquery.f1"
helpviewer_keywords: 
  - "Editor für den Task WMI-Ereignisüberwachung"
ms.assetid: 525f3de7-a021-4e52-9939-3a83c88f131a
caps.latest.revision: 38
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 38
---
# Editor f&#252;r den Task &#39;WMI-Ereignis&#252;berwachung&#39; (Seite WMI-Optionen)
  Auf der Seite **WMI-Optionen** des Dialogfelds **Editor für den Task „WMI-Ereignisüberwachung“** können Sie die Quelle der WQL-Abfrage (Windows Management Instrumentation Query Language) und das Verhalten angeben, mit dem der Task „WMI-Ereignisüberwachung“ auf WMI-Ereignisse (Microsoft Windows Instrumentation) antwortet.  
  
 Informationen, um sich mit diesem Thema vertraut zu machen, finden Sie unter [WMI Event Watcher Task](../../integration-services/control-flow/wmi-event-watcher-task.md). Weitere Informationen zur WMI Query Language finden Sie im WMI-Thema [Querying with WQL](http://go.microsoft.com/fwlink/?LinkId=79045) (Abfragen mit WQL), in der MSDN Library.  
  
## Statische Optionen  
 **WMIConnectionName**  
 Wählen Sie einen WMI-Verbindungs-Manager aus der Liste aus, oder klicken Sie auf \<**Neue WMI-Verbindung...**>, um einen neuen Verbindungs-Manager zu erstellen.  
  
 **Verwandte Themen:** [WMI-Verbindungs-Manager](../../integration-services/connection-manager/wmi-connection-manager.md), [WMI-Verbindungs-Manager-Editor](../../integration-services/connection-manager/wmi-connection-manager-editor.md)  
  
 **WQLQuerySourceType**  
 Wählen Sie den Quelltyp der WQL-Abfrage aus, die von dem Task ausgeführt wird. Diese Eigenschaft besitzt die in der folgenden Tabelle aufgeführten Optionen.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Direct input**|Legen Sie die Quelle für eine WQL-Abfrage fest. Bei Auswahl dieses Wertes wird die dynamische Option **WQLQuerySource**angezeigt.|  
|**File connection**|Wählen Sie eine Datei aus, in der die WQL-Abfrage enthalten ist. Bei Auswahl dieses Wertes wird die dynamische Option **WQLQuerySource**angezeigt.|  
|**Variable**|Legen Sie die Quelle für eine Variable fest, die die WQL-Abfrage definiert. Bei Auswahl dieses Wertes wird die dynamische Option **WQLQuerySource**angezeigt.|  
  
 **ActionAtEvent**  
 Geben Sie an, ob das WMI-Ereignis das Ereignis protokolliert und eine [!INCLUDE[ssIS](../../includes/ssis-md.md)]-Aktion initiiert oder nur das Ereignis protokolliert.  
  
 **AfterEvent**  
 Gibt an, ob der Task nach dem Empfangen des WMI-Ereignisses erfolgreich ausgeführt wird oder fehlschlägt, oder ob die Überwachung des Auftretens dieses Ereignisses durch den Task fortgesetzt wird.  
  
 **ActionAtTimeout**  
 Gibt an, ob ein WMI-Abfragetimeout durch den Task protokolliert und als Antwort ein [!INCLUDE[ssIS](../../includes/ssis-md.md)]-Ereignis ausgelöst wird, oder ob nur der Timeout protokolliert wird.  
  
 **AfterTimeout**  
 Gibt an, ob der Task als Antwort auf einen Timeout erfolgreich ausgeführt wird oder fehlschlägt, oder ob der Task die Überwachung fortsetzt, bis ein weiterer Timeout auftritt.  
  
 **NumberOfEvents**  
 Gibt die Anzahl der zu überwachenden Ereignisse an.  
  
 **Timeout**  
 Gibt die Zeit in Sekunden an, in der auf das Auftreten des Ereignisses gewartet wird. Der Wert 0 bedeutet, dass kein Timeout aktiviert ist.  
  
## WQLQuerySource (dynamische Optionen)  
  
### WQLQuerySource = Direct input  
 **WQLQuerySource**  
 Stellen Sie eine Abfrage bereit, oder klicken Sie auf die Schaltfläche mit den Auslassungspunkten (…), und geben Sie im Dialogfeld **WQL-Abfrage** eine Abfrage ein.  
  
### WQLQuerySource = File connection  
 **WQLQuerySource**  
 Wählen Sie einen Dateiverbindungs-Manager aus der Liste aus, oder klicken Sie auf \<**Neue Verbindung...**>, um einen neuen Verbindungs-Manager zu erstellen.  
  
 **Verwandte Themen:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
### WQLQuerySource = Variable  
 **WQLQuerySource**  
 Wählen Sie eine Variable aus der Liste aus, oder klicken Sie auf \<**Neue Variable…**>, um eine neue Variable zu erstellen.  
  
 **Verwandte Themen:** [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Hinzufügen von Variablen](../Topic/Add%20Variable.md)  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor für den Task „WMI-Ereignisüberwachung“ &#40;Seite „Allgemein“&#41;](../../integration-services/control-flow/wmi-event-watcher-task-editor-general-page.md)   
 [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)   
 [WMI-Datenleser (Task)](../../integration-services/control-flow/wmi-data-reader-task.md)  
  
  