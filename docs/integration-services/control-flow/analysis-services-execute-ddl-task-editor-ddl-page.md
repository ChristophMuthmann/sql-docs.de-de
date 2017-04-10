---
title: "Editor f&#252;r den Analysis Services-Task &#39;DDL ausf&#252;hren&#39; (Seite DDL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.asexecuteddltask.ddl.f1"
helpviewer_keywords: 
  - "Editor für den Analysis Services-Task DDL ausführen"
ms.assetid: f21bf8d0-ec5f-4c18-9de0-8875addb927b
caps.latest.revision: 30
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 30
---
# Editor f&#252;r den Analysis Services-Task &#39;DDL ausf&#252;hren&#39; (Seite DDL)
  Auf der Seite **DDL** des Dialogfelds **Editor für den Analysis Services-Task „DDL ausführen“** können Sie eine Verbindung mit einem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Projekt oder einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Datenbank angeben sowie Informationen zur Quelle der DDL-Anweisungen (Data Definition Language) angeben.  
  
 Informationen, um sich mit diesem Thema vertraut zu machen, finden Sie unter [Analysis Services Execute DDL Task](../../integration-services/control-flow/analysis-services-execute-ddl-task.md).  
  
## Statische Optionen  
 **Verbindung**  
 Wählen Sie ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Projekt oder einen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Verbindungs-Manager aus der Liste aus, oder klicken Sie auf \<**Neue Verbindung...**>, und erstellen Sie im Dialogfeld **Analysis Services-Verbindungs-Manager hinzufügen** eine neue Verbindung.  
  
 **Verwandte Themen:** [Referenz zur Benutzeroberfläche des Dialogfelds Analysis Services-Verbindungs-Manager hinzufügen](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md), [Analysis Services-Verbindungs-Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md)  
  
 **SourceType**  
 Geben Sie den Quelltyp der DDL-Anweisung an. Für diese Eigenschaft sind die in der folgenden Tabelle aufgeführten Optionen verfügbar:  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**Direct Input**|Legen Sie die Quelle der im Textfeld **SourceDirect** gespeicherten DDL-Anweisung fest. Wenn Sie diesen Wert auswählen, werden im folgenden Abschnitt die dynamischen Optionen angezeigt.|  
|**File Connection**|Legen Sie die Quelle für eine Datei fest, in der die DDL-Anweisung enthalten ist. Wenn Sie diesen Wert auswählen, werden im folgenden Abschnitt die dynamischen Optionen angezeigt.|  
|**Variable**|Legen Sie die Quelle für eine Variable fest. Wenn Sie diesen Wert auswählen, werden im folgenden Abschnitt die dynamischen Optionen angezeigt.|  
  
## Dynamische Optionen  
  
### SourceType = Direkteingabe  
 **Quelle**  
 Geben Sie die DDL-Anweisungen ein, oder klicken Sie auf die Schaltfläche mit den drei Punkten **(…)**, und geben Sie dann die Anweisungen im Dialogfeld **DDL-Anweisungen** ein.  
  
### SourceType = File Connection  
 **Quelle**  
 Wählen Sie eine Dateiverbindung aus der Liste aus, oder klicken Sie auf \<**Neue Verbindung...**>, und erstellen Sie im Dialogfeld **Dateiverbindungs-Manager** eine neue Verbindung.  
  
 **Verwandte Themen:** [Dateiverbindungs-Manager](../../integration-services/connection-manager/file-connection-manager.md)  
  
### SourceType = Variable  
 **Quelle**  
 Wählen Sie eine Variable aus der Liste aus, oder klicken Sie auf \<**Neue Variable...**>, und erstellen Sie im Dialogfeld **Variable hinzufügen** eine neue Variable.  
  
 **Verwandte Themen:** [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md)  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor für den Analysis Services-Task „DDL ausführen“ &#40;Seite „Allgemein“&#41;](../../integration-services/control-flow/analysis-services-execute-ddl-task-editor-general-page.md)   
 [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)   
 [Ablaufsteuerung](../../integration-services/control-flow/control-flow.md)   
 [Analysis Services Scripting Language &#40;ASSL für XMLA&#41;](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)   
 [XML for Analysis-Referenz &#40;XMLA&#41;](../../analysis-services/xmla/xml-for-analysis-xmla-reference.md)  
  
  