---
title: "Transaktionen-Ereigniskategorie | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SQL Server-Ereignisklassen, Transaktionen (Ereigniskategorie)"
  - "Ereignisklassen [SQL Server], Transaktionen (Ereigniskategorie)"
  - "Transaktionen-Ereigniskategorie [SQL Server]"
ms.assetid: bfc75c5b-7115-49d8-9148-a0c84ee66a9a
caps.latest.revision: 28
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 28
---
# Transaktionen-Ereigniskategorie
  Die **Transaktionen** -Ereigniskategorie kann zum Überwachen des Status von Transaktionen verwendet werden. Die Ereignisklassennamen mit dem Präfix **TM:** werden zum Nachverfolgen von transaktionsbezogenen Vorgängen verwendet, die über die Schnittstelle zur Transaktionsverwaltung gesendet werden.  
  
## In diesem Abschnitt  
  
|Thema|Beschreibung|  
|-----------|-----------------|  
|[DTCTransaction (Ereignisklasse)](../../relational-databases/event-classes/dtctransaction-event-class.md)|Verfolgt Transaktionen nach, die vom [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator (MS DTC) koordiniert werden. Hierbei handelt es sich um Transaktionen, die zwischen mindestens zwei Datenbanken oder Instanzen von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] verteilt werden.|  
|[SQLTransaction-Ereignisklasse](../../relational-databases/event-classes/sqltransaction-event-class.md)|Verfolgt die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen BEGIN TRAN, COMMIT TRAN, SAVE TRAN und ROLLBACK TRAN nach.|  
|[TM: Begin Tran Completed (Ereignisklasse)](../../relational-databases/event-classes/tm-begin-tran-completed-event-class.md)|Gibt an, dass eine BEGIN TRANSACTION-Anforderung abgeschlossen wurde.|  
|[TM: Begin Tran Starting (Ereignisklasse)](../../relational-databases/event-classes/tm-begin-tran-starting-event-class.md)|Gibt an, dass eine BEGIN TRANSACTION-Anforderung gestartet wird.|  
|[TM: Commit Tran Completed-Ereignisklasse](../../relational-databases/event-classes/tm-commit-tran-completed-event-class.md)|Gibt an, dass eine COMMIT TRANSACTION-Anforderung abgeschlossen wurde.|  
|[TM: Commit Tran Starting (Ereignisklasse)](../../relational-databases/event-classes/tm-commit-tran-starting-event-class.md)|Gibt an, dass eine COMMIT TRANSACTION-Anforderung gestartet wird.|  
|[TM: Promote Tran Completed (Ereignisklasse)](../../relational-databases/event-classes/tm-promote-tran-completed-event-class.md)|Gibt an, dass eine PROMOTE TRANSACTION-Anforderung abgeschlossen wurde.|  
|[TM: Promote Tran Starting (Ereignisklasse)](../../relational-databases/event-classes/tm-promote-tran-starting-event-class.md)|Gibt an, dass eine PROMOTE TRANSACTION-Anforderung gestartet wird.|  
|[TM: Rollback Tran Completed (Ereignisklasse)](../../relational-databases/event-classes/tm-rollback-tran-completed-event-class.md)|Gibt an, dass eine ROLLBACK TRANSACTION-Anforderung abgeschlossen wurde.|  
|[TM: Rollback Tran Starting (Ereignisklasse)](../../relational-databases/event-classes/tm-rollback-tran-starting-event-class.md)|Gibt an, dass eine ROLLBACK TRANSACTION-Anforderung gestartet wird.|  
|[TM: Save Tran Completed-Ereignisklasse](../../relational-databases/event-classes/tm-save-tran-completed-event-class.md)|Gibt an, dass eine SAVE TRANSACTION-Anforderung abgeschlossen wurde.|  
|[TM: Save Tran Starting (Ereignisklasse)](../../relational-databases/event-classes/tm-save-tran-starting-event-class.md)|Gibt an, dass eine SAVE TRANSACTION-Anforderung gestartet wird.|  
|[TransactionLog-Ereignisklasse](../../relational-databases/event-classes/transactionlog-event-class.md)|Verfolgt nach, wenn Transaktionen in das Transaktionsprotokoll einer Datenbank geschrieben werden.|  
  
  