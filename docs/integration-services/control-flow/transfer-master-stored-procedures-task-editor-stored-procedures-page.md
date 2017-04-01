---
title: "Editor f&#252;r den Task &#39;In &#39;master&#39; gespeicherte Prozeduren &#252;bertragen&#39; (Seite Gespeicherte Prozeduren) | Microsoft Docs"
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
  - "sql13.dts.designer.transferstoredprocedurestask.storedprocedures.f1"
helpviewer_keywords: 
  - "Editor für den Task In master gespeicherte Prozeduren übertragen"
ms.assetid: 5fcf171e-cc0b-4c24-8eb5-3a4b4775e64a
caps.latest.revision: 20
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 20
---
# Editor f&#252;r den Task &#39;In &#39;master&#39; gespeicherte Prozeduren &#252;bertragen&#39; (Seite Gespeicherte Prozeduren)
  Verwenden Sie die Seite **Gespeicherte Prozeduren** im Dialogfeld **Editor für den Task „In 'master' gespeicherte Prozeduren übertragen“**, um die Eigenschaften für das Kopieren einer oder mehrerer benutzerdefinierter gespeicherter Prozeduren aus der **master**-Datenbank einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in die **master**-Datenbank einer anderen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zu kopieren. Weitere Informationen zu diesem Task finden Sie unter [Transfer Master Stored Procedures Task](../../integration-services/control-flow/transfer-master-stored-procedures-task.md).  
  
> [!NOTE]  
>  Dieser Task überträgt lediglich die benutzerdefinierten gespeicherten Prozeduren des **dbo**-Besitzers aus einer **master**-Datenbank auf dem Quellserver in eine **master**-Datenbank auf dem Zielserver. Benutzer müssen die CREATE PROCEDURE-Berechtigung für die **master** -Datenbank des Zielservers besitzen oder Mitglieder der festen Serverrolle **sysadmin** auf dem Zielserver sein, um dort gespeicherte Prozeduren erstellen zu können.  
  
## enthalten  
 **SourceConnection**  
 Wählen Sie in der Liste einen SMO-Verbindungs-Manager aus, oder klicken Sie auf **\<Neue Verbindung...>**, um eine neue Verbindung mit dem Quellserver zu erstellen.  
  
 **DestinationConnection**  
 Wählen Sie in der Liste einen SMO-Verbindungs-Manager aus, oder klicken Sie auf **\<Neue Verbindung...>**, um eine neue Verbindung mit dem Zielserver zu erstellen.  
  
 **IfObjectExists**  
 Wählen Sie aus, wie der Task benutzerdefinierte gespeicherte Prozeduren behandeln soll, die in der **master**-Datenbank auf dem Zielserver bereits mit demselben Namen vorhanden sind.  
  
 Für diese Eigenschaft sind die in der folgenden Tabelle aufgeführten Optionen verfügbar:  
  
|Wert|Description|  
|-----------|-----------------|  
|**FailTask**|Der Task schlägt fehl, wenn in der **master** -Datenbank auf dem Zielserver bereits gespeicherte Prozeduren mit demselben Namen vorhanden sind.|  
|**Overwrite**|Der Task überschreibt bereits vorhandene gespeicherte Prozeduren mit demselben Namen in der **master** -Datenbank auf dem Zielserver.|  
|**Skip**|Der Task lässt bereits vorhandene gespeicherte Prozeduren mit demselben Namen in der **master** -Datenbank auf dem Zielserver aus.|  
  
 **TransferAllStoredProcedures**  
 Wählen Sie aus, ob alle benutzerdefinierten gespeicherten Prozeduren in der **master**-Datenbank auf dem Quellserver auf den Zielserver kopiert werden sollen.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Wahr**|Kopiert alle benutzerdefinierten gespeicherten Prozeduren in der **master**-Datenbank.|  
|**False**|Kopiert nur die angegebenen gespeicherten Prozeduren.|  
  
 **StoredProceduresList**  
 Wählen Sie aus, welche benutzerdefinierten gespeicherten Prozeduren in der **master**-Datenbank auf dem Quellserver in die **master**-Datenbank auf dem Zielserver kopiert werden sollen. Diese Option ist nur verfügbar, wenn **TransferAllStoredProcedures** auf **FALSE**festgelegt ist.  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Integration Services-Tasks](../../integration-services/control-flow/integration-services-tasks.md)   
 [Editor für den Task „In 'master' gespeicherte Prozeduren übertragen“ &#40;Seite „Allgemein“&#41;](../../integration-services/control-flow/transfer-master-stored-procedures-task-editor-general-page.md)   
 [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)   
 [SMO-Verbindungs-Manager](../../integration-services/connection-manager/smo-connection-manager.md)  
  
  