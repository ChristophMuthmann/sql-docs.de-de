---
title: "Editor f&#252;r den Task &#39;Webdienst&#39; (Seite Ausgabe) | Microsoft Docs"
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
  - "sql13.dts.designer.webservicestask.output.f1"
helpviewer_keywords: 
  - "Editor für den Task Webdienst"
ms.assetid: 73c83969-7b0e-479d-a436-0a46b2068d01
caps.latest.revision: 27
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 27
---
# Editor f&#252;r den Task &#39;Webdienst&#39; (Seite Ausgabe)
  Verwenden Sie die Seite **Ausgabe** des Dialogfelds **Editor für den Task 'Webdienst'** , um anzugeben, wo das durch die Webmethode zurückgegebene Ergebnis gespeichert werden soll.  
  
 Weitere Informationen zu diesem Task finden Sie unter [Webdienst (Task)](../../integration-services/control-flow/web-service-task.md).  
  
## Statische Optionen  
 **OutputType**  
 Wählt den Speichertyp, der beim Speichern der Ergebnisse verwendet werden soll. Diese Eigenschaft besitzt die in der folgenden Tabelle aufgeführten Optionen.  
  
|Wert|Description|  
|-----------|-----------------|  
|**File Connection**|Speichert die Ergebnisse in einer Datei. Wenn Sie diesen Wert auswählen, wird die dynamische Option **Datei**angezeigt.|  
|**Variable**|Speichert die Ergebnisse in einer Variablen. Wenn Sie diesen Wert auswählen, wird die dynamische Option **Variable**angezeigt.|  
  
## OutputType (dynamische Optionen)  
  
### OutputType = File Connection  
 **File**  
 Wählen Sie einen vorhandenen Dateiverbindungs-Manager aus der Liste aus, oder klicken Sie auf \<**Neue Verbindung...**>, um einen neuen Verbindungs-Manager zu erstellen.  
  
 **Verwandte Themen:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
### OutputType = Variable  
 **Variable**  
 Wählen Sie eine Variable aus der Liste aus, oder klicken Sie auf \<**Neue Variable…**>, um eine neue Variable zu erstellen.  
  
 **Verwandte Themen:** [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Hinzufügen von Variablen](../Topic/Add%20Variable.md)  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor für den Task „Webdienst“ &#40;Seite „Allgemein“&#41;](../../integration-services/control-flow/web-service-task-editor-general-page.md)   
 [Editor für den Task „Webdienst“ &#40;Seite „Eingabe“&#41;](../../integration-services/control-flow/web-service-task-editor-input-page.md)   
 [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)  
  
  