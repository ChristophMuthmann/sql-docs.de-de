---
title: Teilsicherungen (SQL Server) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- full backups [SQL Server]
- partial backups [SQL Server]
- READ_WRITE_FILEGROUPS option
- database backups [SQL Server], about backing up databases
ms.assetid: fe6b6bb1-38d0-46c4-bab8-31df14e8999c
caps.latest.revision: "46"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 9b69a8178c78bf6cb14956ff58b0877a681e82d7
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="partial-backups-sql-server"></a>Teilsicherungen (SQL Server)
  Alle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Wiederherstellungsmodelle unterstützen Teilsicherungen, deshalb ist dieses Thema für alle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbanken relevant. Teilsicherungen wurden jedoch für die Verwendung mit dem einfachen Sicherungsmodell konzipiert, und zwar mit der Absicht, die Flexibilität bei der Sicherung sehr großer Datenbanken mit einer oder mehreren schreibgeschützten Dateigruppen zu verbessern.  
  
 Teilsicherungen erweisen sich besonders dann als nützlich, wenn Sie bestimmte schreibgeschützte Dateigruppen aus der Sicherung ausschließen möchten. Eine *Teilsicherung* ähnelt einer vollständigen Datenbanksicherung. Sie enthält jedoch nicht alle Dateigruppen. Stattdessen enthält eine Teilsicherung für eine Datenbank mit Lese-/Schreibzugriff alle Daten in der primären Dateigruppe, alle Lese-/Schreibdateigruppen sowie alle optional angegebenen schreibgeschützten Dateien. Eine Teilsicherung einer schreibgeschützten Datenbank enthält nur die primäre Dateigruppe.  
  
> [!NOTE]  
>  Wenn eine schreibgeschützte Datenbank nach einer Teilsicherung in eine Datenbank mit Lese-/Schreibzugriff geändert wird, können sekundäre Dateigruppen mit Lese-/Schreibzugriff vorhanden sein, die nicht in der Teilsicherung enthalten sind. Wenn Sie in diesem Fall versuchen, eine differenzielle Teilsicherung zu erstellen, tritt bei der Sicherung ein Fehler auf. Bevor Sie eine differenzielle Teilsicherung der Datenbank erstellen können, müssen Sie eine weitere Teilsicherung erstellen. Die neue Teilsicherung enthält alle sekundären Dateigruppen mit Lese-/Schreibzugriff und kann als Basis für differenzielle Teilsicherungen dienen.  
  
 Dateisicherungen von schreibgeschützten Dateigruppen können mit Teilsicherungen kombiniert werden. Informationen zu Dateisicherungen finden Sie unter [Vollständige Dateisicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md).  
  
 Eine Teilsicherung kann als *differenzielle Basis* für differenzielle Teilsicherungen verwendet werden. Weitere Informationen finden Sie unter [Differenzielle Sicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md).  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
> [!NOTE]  
>  Teilsicherungen werden nicht von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder vom Wartungsplanungs-Assistenten unterstützt.  
  
 **So erstellen Sie eine Teilsicherung**  
  
-   [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md) (READ_WRITE_FILEGROUPS; FILEGROUP-Option nach Bedarf)  
  
 **So verwenden Sie eine Teilsicherung in einer Wiederherstellungssequenz**  
  
-   [Beispiel: Schrittweise Wiederherstellung einer Datenbank &#40;einfaches Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [Beispiel: Schrittweise Wiederherstellung nur bestimmter Dateigruppen &#40;einfaches Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über Sicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [Dateiwiederherstellungen &#40;einfaches Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)   
 [Schrittweise Wiederherstellungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
