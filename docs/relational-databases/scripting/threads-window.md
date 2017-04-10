---
title: "Fenster &#39;Threads&#39; | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vs.debug.threads"
helpviewer_keywords: 
  - "Fenster 'Threads' [Transact-SQL]"
ms.assetid: e153f619-0049-4162-9076-c24a454f3278
caps.latest.revision: 13
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Fenster &#39;Threads&#39;
  Im Fenster **Threads** werden Informationen zu dem [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Thread angezeigt, der von der gerade gedebuggten [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Abfrage-Editor-Sitzung verwendet wird. Sie müssen sich im Debugmodus befinden, um die Threadinformationen anzuzeigen.  
  
## Aufgabenliste  
 **So greifen Sie auf das Threadfenster zu**  
  
-   Klicken Sie im Menü **Debuggen** auf **Fenster**und dann auf **Threads**.  
  
## Spalten  
 **ID**  
 Ist eine eindeutig kennzeichnende Zahl, die der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Debugger dem Thread zuweist. Um weitere Informationen zum Thread anzuzeigen, wählen Sie in der dynamischen Verwaltungssicht sys.dm_os_threads eine Zeile aus.  
  
 Wenn die Ausführung nicht im Lightweightpooling-Modus erfolgt, wählen Sie die Zeile aus, in der der Wert in „os_thread_id“ mit dem Wert in der Spalte **ID** übereinstimmt. Wenn die Ausführung im Lightweightpooling-Modus erfolgt, wählen Sie die Zeile aus, in der der Wert in „fiber_context_address“ mit dem Wert in der Spalte **ID** übereinstimmt.  
  
 **Name**  
 Zeigt Informationen über die [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Sitzung im Format **ComputerName/InstanceName [SPID]** an.  
  
 **Computername**  
 Der Name des Computers, auf dem die Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] ausgeführt wird, mit der die Abfrage-Editor-Sitzung verbunden ist.  
  
 **InstanceName**  
 Der Name der Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)], mit der die Abfrage-Editor-Sitzung verbunden ist.  
  
 **[SPID]**  
 Die Prozess-ID der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sitzung, die diese Sitzung eindeutig kennzeichnet. Weitere Informationen über die Sitzung können Sie abrufen, indem Sie in der sys.sysprocesses-Sicht die Zeile auswählen, die in der Spalte spid denselben Wert enthält.  
  
 **Speicherort**  
 Zeigt den Namen der Skriptdatei an, die von der gerade gedebuggten Abfrage-Editor-Sitzung verwendet wird.  
  
 **Priority**  
 Der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Debugger unterstützt diese Funktion nicht.  
  
 **Angehalten**  
 Der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Debugger unterstützt diese Funktion nicht.  
  
## Siehe auch  
 [Transact-SQL-Debugger](../../relational-databases/scripting/transact-sql-debugger.md)   
 [Transact-SQL-Debuggerinformationen](../../relational-databases/scripting/transact-sql-debugger-information.md)   
 [sys.dm_os_threads &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-threads-transact-sql.md)   
 [sys.sysprocesses &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md)  
  
  