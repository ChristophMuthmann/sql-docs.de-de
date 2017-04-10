---
title: "Editor f&#252;r den Task Fehlermeldungen &#252;bertragen (Seite Meldungen) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.transfererrormessagestask.errormessages.F1"
helpviewer_keywords: 
  - "Editor für den Task Fehlermeldungen übertragen"
ms.assetid: cb2226a0-3037-4fdf-966f-81eabc0da9cf
caps.latest.revision: 22
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 22
---
# Editor f&#252;r den Task Fehlermeldungen &#252;bertragen (Seite Meldungen)
  Verwenden Sie die Seite **Meldungen** im Dialogfeld **Editor für den Task „Fehlermeldungen übertragen“**, um die Eigenschaften für das Kopieren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlermeldungen von einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in eine andere anzugeben. Weitere Informationen zu diesem Task finden Sie unter [Transfer Error Messages Task](../../integration-services/control-flow/transfer-error-messages-task.md).  
  
## enthalten  
 **SourceConnection**  
 Wählen Sie in der Liste einen SMO-Verbindungs-Manager aus, oder klicken Sie auf **\<Neue Verbindung...>**, um eine neue Verbindung mit dem Quellserver zu erstellen.  
  
 **DestinationConnection**  
 Wählen Sie in der Liste einen SMO-Verbindungs-Manager aus, oder klicken Sie auf **\<Neue Verbindung...>**, um eine neue Verbindung mit dem Zielserver zu erstellen.  
  
 **IfObjectExists**  
 Wählen Sie aus, ob der Task vorhandene benutzerdefinierte Fehlermeldungen überschreiben, vorhandene Meldungen auslassen oder einen Fehler erzeugen soll, wenn auf dem Zielserver bereits Meldungen desselben Namens vorhanden sind.  
  
 **TransferAllErrorMessages**  
 Wählen Sie aus, ob der Task alle oder nur die angegebenen benutzerdefinierten Meldungen vom Quell- auf den Zielserver kopieren soll.  
  
 Für diese Eigenschaft sind die in der folgenden Tabelle aufgeführten Optionen verfügbar:  
  
|Wert|Description|  
|-----------|-----------------|  
|**Wahr**|Alle benutzerdefinierten Meldungen kopieren.|  
|**False**|Nur die angegebenen benutzerdefinierten Meldungen kopieren.|  
  
 **ErrorMessagesList**  
 Klicken Sie auf die Schaltfläche zum Durchsuchen **(…)**, um die zu kopierenden Fehlermeldungen auszuwählen.  
  
> [!NOTE]  
>  Sie müssen **SourceConnection** angeben, bevor Sie eine zu kopierende Fehlermeldung auswählen können.  
  
 **ErrorMessageLanguagesList**  
 Klicken Sie auf die Schaltfläche zum Durchsuchen **(…)**, um die Sprachen auszuwählen, für die benutzerdefinierte Fehlermeldungen auf den Zielserver kopiert werden. Auf dem Zielserver muss eine Version der Meldung in us_english (Codepage 1033) vorhanden sein, bevor Sie andere Sprachversionen auf den Server übertragen können.  
  
> [!NOTE]  
>  Sie müssen **SourceConnection** angeben, bevor Sie eine zu kopierende Fehlermeldung auswählen können.  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Integration Services-Tasks](../../integration-services/control-flow/integration-services-tasks.md)   
 [Editor für den Task „Fehlermeldungen übertragen“ &#40;Seite „Allgemein“&#41;](../../integration-services/control-flow/transfer-error-messages-task-editor-general-page.md)   
 [SMO-Verbindungs-Manager](../../integration-services/connection-manager/smo-connection-manager.md)   
 [Editor für den Task „Fehlermeldungen übertragen“ &#40;Seite „Allgemein“&#41;](../../integration-services/control-flow/transfer-error-messages-task-editor-general-page.md)   
 [SMO-Verbindungs-Manager](../../integration-services/connection-manager/smo-connection-manager.md)  
  
  