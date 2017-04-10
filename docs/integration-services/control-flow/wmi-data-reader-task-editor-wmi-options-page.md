---
title: "Editor f&#252;r den Task &#39;WMI-Datenleser&#39; (Seite WMI-Optionen) | Microsoft Docs"
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
  - "sql13.dts.designer.wmidatareadertask.wmiquery.f1"
helpviewer_keywords: 
  - "Editor für den Task WMI-Datenleser"
ms.assetid: 4b8d4716-882d-41b0-b77e-e0e2741a2cd5
caps.latest.revision: 40
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 40
---
# Editor f&#252;r den Task &#39;WMI-Datenleser&#39; (Seite WMI-Optionen)
  Auf der Seite **WMI-Optionen** des Dialogfelds **Editor für den Task „WMI-Datenleser“** können Sie die Quelle der WQL-Abfrage (Windows Management Instrumentation Query Language) und das Ziel des Abfrageergebnisses angeben.  
  
 Informationen, um sich mit diesem Thema vertraut zu machen, finden Sie unter [WMI Data Reader Task](../../integration-services/control-flow/wmi-data-reader-task.md). Weitere Informationen zur WMI Query Language (WQL) finden Sie im Thema zur Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI), [Querying with WQL](http://go.microsoft.com/fwlink/?LinkId=79045) (Abfragen mit WQL), in der MSDN Library.  
  
## Statische Optionen  
 **WMIConnectionName**  
 Wählen Sie einen vorhandenen WMI-Verbindungs-Manager aus der Liste aus, oder klicken Sie auf \<**Neue WMI-Verbindung...**>, um einen neuen Verbindungs-Manager zu erstellen.  
  
 **Verwandte Themen:** [WMI-Verbindungs-Manager](../../integration-services/connection-manager/wmi-connection-manager.md), [WMI-Verbindungs-Manager-Editor](../../integration-services/connection-manager/wmi-connection-manager-editor.md)  
  
 **WQLQuerySourceType**  
 Wählen Sie den Quelltyp der WQL-Abfrage aus, die von dem Task ausgeführt wird. Diese Eigenschaft besitzt die in der folgenden Tabelle aufgeführten Optionen.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Direct input**|Legen Sie die Quelle für eine WQL-Abfrage fest. Bei Auswahl dieses Werts wird die dynamische Option **WQLQuerySourceType**angezeigt.|  
|**File connection**|Wählen Sie eine Datei aus, in der die WQL-Abfrage enthalten ist. Bei Auswahl dieses Werts wird die dynamische Option **WQLQuerySourceType**angezeigt.|  
|**Variable**|Legen Sie die Quelle für eine Variable fest, die die WQL-Abfrage definiert. Bei Auswahl dieses Werts wird die dynamische Option **WQLQuerySourceType**angezeigt.|  
  
 **OutputType**  
 Geben Sie an, ob es sich bei der Ausgabe um eine Datentabelle, einen Eigenschaftswert oder einen Eigenschaftsnamen und -wert handeln soll.  
  
 **OverwriteDestination**  
 Gibt an, ob die ursprünglichen Daten in der Zieldatei oder -variablen beibehalten, überschrieben oder an diese angefügt werden sollen.  
  
 **DestinationType**  
 Wählen Sie den Zieltyp der WQL-Abfrage aus, die von dem Task ausgeführt wird. Diese Eigenschaft besitzt die in der folgenden Tabelle aufgeführten Optionen.  
  
|Wert|Description|  
|-----------|-----------------|  
|**File connection**|Wählen Sie eine Datei aus, um die Ergebnisse der WQL-Abfrage darin zu speichern. Bei Auswahl dieses Werts wird die dynamische Option **DestinationType**angezeigt.|  
|**Variable**|Legen Sie die Variable fest, um die Ergebnisse der WQL-Abfrage darin zu speichern. Bei Auswahl dieses Werts wird die dynamische Option **DestinationType**angezeigt.|  
  
## Dynamische Optionen von WQLQuerySourceType  
  
### WQLQuerySourceType = Direct input  
 **WQLQuerySource**  
 Stellen Sie eine Abfrage bereit, oder klicken Sie auf die Schaltfläche mit den Auslassungspunkten, und geben Sie eine Abfrage mithilfe des Dialogfelds **WQL-Abfrage** ein.  
  
### WQLQuerySourceType = File connection  
 **WQLQuerySource**  
 Wählen Sie einen Dateiverbindungs-Manager aus der Liste aus, oder klicken Sie auf \<**Neue Verbindung...**>, um einen neuen Verbindungs-Manager zu erstellen.  
  
 **Verwandte Themen:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
### WQLQuerySourceType = Variable  
 **WQLQuerySource**  
 Wählen Sie eine Variable aus der Liste aus, oder klicken Sie auf \<**Neue Variable…**>, um eine neue Variable zu erstellen.  
  
 **Verwandte Themen:** [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Hinzufügen von Variablen](../Topic/Add%20Variable.md)  
  
## Dynamische Optionen von DestinationType  
  
### DestinationType = File connection  
 **Ziel**  
 Wählen Sie einen Dateiverbindungs-Manager aus der Liste aus, oder klicken Sie auf \<**Neue Verbindung...**>, um einen neuen Verbindungs-Manager zu erstellen.  
  
 **Verwandte Themen:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
### DestinationType = Variable  
 **Ziel**  
 Wählen Sie eine Variable aus der Liste aus, oder klicken Sie auf \<**Neue Variable…**>, um eine neue Variable zu erstellen.  
  
 **Verwandte Themen:** [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Hinzufügen von Variablen](../Topic/Add%20Variable.md)  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor für den Task „WMI-Datenleser“ &#40;Seite Allgemein&#41;](../../integration-services/control-flow/wmi-data-reader-task-editor-general-page.md)   
 [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)   
 [WMI-Ereignisüberwachung (Task)](../../integration-services/control-flow/wmi-event-watcher-task.md)  
  
  