---
title: "Verlaufscleanup (Task) | Microsoft Docs"
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
  - "sql13.dts.designer.historycleanuptask.f1"
helpviewer_keywords: 
  - "Verlaufstabellen [SQL Server]"
  - "Verlaufscleanup (Task) [Integration Services]"
ms.assetid: 5defc5b9-dfd3-4859-a7fe-ac8c2b5480f8
caps.latest.revision: 43
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 43
---
# Verlaufscleanup (Task)
  Der Task Verlaufscleanup löscht Einträge in den folgenden Verlaufstabellen in der msdb-Datenbank von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   backupfile  
  
-   backupfilegroup  
  
-   backupmediafamily  
  
-   backupmediaset  
  
-   backupset  
  
-   restorefile  
  
-   restorefilegroup  
  
-   restorehistory  
  
 Mithilfe des Tasks "Verlaufscleanup" können für ein Paket Vergangenheitsdaten für Sicherungs- und Wiederherstellungsaktivitäten, Aufträge des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents und Datenbankwartungspläne gelöscht werden.  
  
 Dieser Task kapselt die gespeicherte Systemprozedur sp_delete_backuphistory und übergibt das angegebene Datum als Argument an die Prozedur. Weitere Informationen finden Sie unter [sp_delete_backuphistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md).  
  
## Konfiguration der Task "Verlaufscleanup"  
 Dieser Task umfasst eine Eigenschaft zur Angabe des am weitesten zurückliegenden Datums von Daten, die in Verlaufstabellen beibehalten werden. Sie können das Datum anhand der Anzahl von Tagen, Wochen, Monaten oder Jahren ab dem aktuellen Datum angeben. Der Task übersetzt das Intervall dann automatisch in ein Datum.  
  
 Eigenschaften können Sie mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen. Dieser Task ist im **-Designer in der** Toolbox **im Abschnitt** Wartungsplantasks [!INCLUDE[ssIS](../../includes/ssis-md.md)] enthalten.  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [Task „Verlaufscleanup“ &#40;Wartungsplan&#41;](../../relational-databases/maintenance-plans/history-cleanup-task-maintenance-plan.md)  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum Festlegen dieser Eigenschaften im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer zu erhalten:  
  
-   [Festlegen der Eigenschaften eines Tasks oder Containers](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
## Siehe auch  
 [Integration Services-Tasks](../../integration-services/control-flow/integration-services-tasks.md)   
 [Ablaufsteuerung](../../integration-services/control-flow/control-flow.md)  
  
  