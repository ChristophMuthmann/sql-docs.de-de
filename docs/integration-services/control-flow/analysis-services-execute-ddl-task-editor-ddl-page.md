---
title: Analysis Services-Task DDL-Task-Editor (Seite DDL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.asexecuteddltask.ddl.f1
helpviewer_keywords:
- Analysis Services Execute DDL Task Editor
ms.assetid: f21bf8d0-ec5f-4c18-9de0-8875addb927b
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4bae07f66d84f8a692ad7b59ef61ee63d4a5fd62
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="analysis-services-execute-ddl-task-editor-ddl-page"></a>Editor für den Analysis Services-Task 'DDL ausführen' (Seite DDL)
  Auf der Seite **DDL** des Dialogfelds **Editor für den Analysis Services-Task „DDL ausführen“** können Sie eine Verbindung mit einem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt oder einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank angeben sowie Informationen zur Quelle der DDL-Anweisungen (Data Definition Language) angeben.  
  
 Informationen, um sich mit diesem Thema vertraut zu machen, finden Sie unter [Analysis Services Execute DDL Task](../../integration-services/control-flow/analysis-services-execute-ddl-task.md).  
  
## <a name="static-options"></a>Statische Optionen  
 **Verbindung**  
 Wählen Sie eine [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Projekt oder eine [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Verbindungs-Manager in der Liste aus, oder klicken Sie \< **neue Verbindung...** > und Verwenden der **Hinzufügen von Analysis Services Connection Manager** (Dialogfeld), um eine neue Verbindung zu erstellen.  
  
 **Verwandte Themen:** [Referenz zur Benutzeroberfläche des Dialogfelds Analysis Services-Verbindungs-Manager hinzufügen](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md), [Analysis Services-Verbindungs-Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md)  
  
 **SourceType**  
 Geben Sie den Quelltyp der DDL-Anweisung an. Für diese Eigenschaft sind die in der folgenden Tabelle aufgeführten Optionen verfügbar:  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**Direct Input**|Legen Sie die Quelle der im Textfeld **SourceDirect** gespeicherten DDL-Anweisung fest. Wenn Sie diesen Wert auswählen, werden im folgenden Abschnitt die dynamischen Optionen angezeigt.|  
|**File Connection**|Legen Sie die Quelle für eine Datei fest, in der die DDL-Anweisung enthalten ist. Wenn Sie diesen Wert auswählen, werden im folgenden Abschnitt die dynamischen Optionen angezeigt.|  
|**Variable**|Legen Sie die Quelle für eine Variable fest. Wenn Sie diesen Wert auswählen, werden im folgenden Abschnitt die dynamischen Optionen angezeigt.|  
  
## <a name="dynamic-options"></a>Dynamische Optionen  
  
### <a name="sourcetype--direct-input"></a>SourceType = Direkteingabe  
 **Quelle**  
 Geben Sie die DDL-Anweisungen ein, oder klicken Sie auf die Schaltfläche mit den drei Punkten **(…)** , und geben Sie dann die Anweisungen im Dialogfeld **DDL-Anweisungen** ein.  
  
### <a name="sourcetype--file-connection"></a>SourceType = File Connection  
 **Quelle**  
 Wählen Sie eine dateiverbindung aus der Liste aus, oder klicken Sie auf \< **neue Verbindung...** > und Verwenden der **Dateiverbindungs-Manager** (Dialogfeld), um eine neue Verbindung zu erstellen.  
  
 **Verwandte Themen:** [Dateiverbindungs-Manager](../../integration-services/connection-manager/file-connection-manager.md)  
  
### <a name="sourcetype--variable"></a>SourceType = Variable  
 **Quelle**  
 Wählen Sie eine Variable in der Liste aus, oder klicken Sie auf \< **neue Variable...** > und Verwenden der **Variable hinzufügen** (Dialogfeld), um eine neue Variable zu erstellen.  
  
 **Verwandte Themen:** [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Analysis Services Execute DDL Task-Editor &#40; Seite "Allgemein" &#41;](../../integration-services/control-flow/analysis-services-execute-ddl-task-editor-general-page.md)   
 [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)   
 [Ablaufsteuerung](../../integration-services/control-flow/control-flow.md)   
 [Analysis Services Scripting Language &#40;ASSL für XMLA&#41;](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)   
 [XML for Analysis &#40; XMLA &#41; Referenz](../../analysis-services/xmla/xml-for-analysis-xmla-reference.md)  
  
  
