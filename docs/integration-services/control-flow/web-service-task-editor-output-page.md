---
title: Web Service Task-Editor (Seite "Fehlerausgabe") | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.webservicestask.output.f1
helpviewer_keywords:
- Web Service Task Editor
ms.assetid: 73c83969-7b0e-479d-a436-0a46b2068d01
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f4bd03a4844548b7dfbc976224c09c47f0ab2a4f
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="web-service-task-editor-output-page"></a>Editor für den Task 'Webdienst' (Seite Ausgabe)
  Verwenden Sie die Seite **Ausgabe** des Dialogfelds **Editor für den Task 'Webdienst'** , um anzugeben, wo das durch die Webmethode zurückgegebene Ergebnis gespeichert werden soll.  
  
 Weitere Informationen zu diesem Task finden Sie unter [Webdienst (Task)](../../integration-services/control-flow/web-service-task.md).  
  
## <a name="static-options"></a>Statische Optionen  
 **OutputType**  
 Wählt den Speichertyp, der beim Speichern der Ergebnisse verwendet werden soll. Diese Eigenschaft besitzt die in der folgenden Tabelle aufgeführten Optionen.  
  
|Wert|Description|  
|-----------|-----------------|  
|**File Connection**|Speichert die Ergebnisse in einer Datei. Wenn Sie diesen Wert auswählen, wird die dynamische Option **Datei**angezeigt.|  
|**Variable**|Speichert die Ergebnisse in einer Variablen. Wenn Sie diesen Wert auswählen, wird die dynamische Option **Variable**angezeigt.|  
  
## <a name="outputtype-dynamic-options"></a>OutputType (dynamische Optionen)  
  
### <a name="outputtype--file-connection"></a>OutputType = File Connection  
 **File**  
 Wählen Sie einen Dateiverbindungs-Manager in der Liste aus, oder klicken Sie auf \< **neue Verbindung...** > um einen neuen Verbindungs-Manager zu erstellen.  
  
 **Verwandte Themen:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
### <a name="outputtype--variable"></a>OutputType = Variable  
 **Variable**  
 Wählen Sie eine Variable in der Liste aus, oder klicken Sie auf \< **neue Variable...** > um eine neue Variable zu erstellen.  
  
 **Verwandte Themen:** [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Hinzufügen von Variablen](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Meldungsreferenz von Integration Services-Fehler](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor für den Task Webdienst &#40; Seite "Allgemein" &#41;](../../integration-services/control-flow/web-service-task-editor-general-page.md)   
 [Web-Service-Task-Editor &#40; Eingabe Seite &#41;](../../integration-services/control-flow/web-service-task-editor-input-page.md)   
 [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)  
  
  
