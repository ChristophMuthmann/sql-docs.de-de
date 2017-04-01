---
title: "Editor f&#252;r den Task Auftr&#228;ge &#252;bertragen (Seite Auftr&#228;ge) | Microsoft Docs"
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
  - "sql13.dts.designer.transferjobstask.jobs.f1"
helpviewer_keywords: 
  - "Editor für den Task Aufträge übertragen"
ms.assetid: e72b1dc7-8cda-4ee6-abb5-d438370f04df
caps.latest.revision: 24
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 24
---
# Editor f&#252;r den Task Auftr&#228;ge &#252;bertragen (Seite Auftr&#228;ge)
  Auf der Seite **Aufträge** des Dialogfelds **Editor für den Task "Aufträge übertragen"** können Sie die Eigenschaften für das Kopieren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agentaufträgen von einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in eine andere angeben. Weitere Informationen zum Task Aufträge übertragen finden Sie unter [Transfer Jobs Task](../../integration-services/control-flow/transfer-jobs-task.md).  
  
> [!NOTE]  
>  Um auf dem Quellserver auf Aufträge zuzugreifen, müssen Benutzer auf dem Server Mitglied mindestens einer festen Serverrolle **SQLAgentUserRole** sein. Um auf dem Zielserver Aufträge erfolgreich zu erstellen, muss der Benutzer Mitglied der festen Datenbankrolle **sysadmin** oder einer der festen Datenbankrollen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents sein. Weitere Informationen zu den festen Datenbankrollen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agents und zu deren Berechtigungen finden Sie unter [Feste Datenbankrollen des SQL Server-Agents](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
## enthalten  
 **SourceConnection**  
 Wählen Sie in der Liste einen SMO-Verbindungs-Manager aus, oder klicken Sie auf **\<Neue Verbindung...>**, um eine neue Verbindung mit dem Quellserver zu erstellen.  
  
 **DestinationConnection**  
 Wählen Sie in der Liste einen SMO-Verbindungs-Manager aus, oder klicken Sie auf **\<Neue Verbindung...>**, um eine neue Verbindung mit dem Zielserver zu erstellen.  
  
 **TransferAllJobs**  
 Wählen Sie aus, ob der Task alle oder nur angegebene [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agentaufträge vom Quell- auf den Zielserver kopieren soll.  
  
 Für diese Eigenschaft sind die in der folgenden Tabelle aufgeführten Optionen verfügbar:  
  
|Wert|Description|  
|-----------|-----------------|  
|**Wahr**|Kopiert alle Aufträge.|  
|**False**|Kopiert nur angegebene Aufträge.|  
  
 **JobsList**  
 Klicken Sie auf die Schaltfläche zum Durchsuchen **(...)**, um die zu kopierenden Aufträge auszuwählen. Es muss mindestens ein Auftrag ausgewählt werden.  
  
> [!NOTE]  
>  Geben Sie vor der Auswahl der zu kopierenden Aufträge **SourceConnection** an.  
  
 Die Option **JobsList** ist nicht verfügbar, wenn **TransferAllJobs** auf **True**festgelegt ist.  
  
 **IfObjectExists**  
 Wählen Sie aus, wie der Task Aufträge behandeln soll, die auf dem Zielserver bereits mit demselben Namen vorhanden sind.  
  
 Für diese Eigenschaft sind die in der folgenden Tabelle aufgeführten Optionen verfügbar:  
  
|Wert|Description|  
|-----------|-----------------|  
|**FailTask**|Der Task schlägt fehl, wenn auf dem Zielserver bereits Aufträge mit demselben Namen vorhanden sind.|  
|**Overwrite**|Der Task überschreibt auf dem Zielserver Aufträge mit demselben Namen.|  
|**Skip**|Der Task lässt Aufträge aus, die auf dem Zielserver mit demselben Namen vorhanden sind.|  
  
 **EnableJobsAtDestination**  
 Wählen Sie aus, ob die auf den Zielserver kopierten Aufträge aktiviert werden sollen.  
  
 Für diese Eigenschaft sind die in der folgenden Tabelle aufgeführten Optionen verfügbar:  
  
|Wert|Description|  
|-----------|-----------------|  
|**Wahr**|Aktiviert Jobs auf dem Zielserver.|  
|**False**|Deaktiviert Jobs auf dem Zielserver.|  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Integration Services-Tasks](../../integration-services/control-flow/integration-services-tasks.md)   
 [Editor für den Task „Aufträge übertragen“ &#40;Seite „Allgemein“&#41;](../../integration-services/control-flow/transfer-jobs-task-editor-general-page.md)   
 [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)   
 [SMO-Verbindungs-Manager](../../integration-services/connection-manager/smo-connection-manager.md)  
  
  