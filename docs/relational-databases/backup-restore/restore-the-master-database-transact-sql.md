---
title: Wiederherstellen der Hauptdatenbank (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- master database [SQL Server], restoring
ms.assetid: c83d802c-e84e-4458-b3ca-173d9ba32f73
caps.latest.revision: 42
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 36558a8f79b9ad229a90970b5df514a399b68c66
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="restore-the-master-database-transact-sql"></a>Wiederherstellen der master-Datenbank (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  In diesem Thema erfahren Sie, wie Sie die **master** -Datenbank von einer vollständigen Datenbanksicherung wiederherstellen.  
  
### <a name="to-restore-the-master-database"></a>So stellen Sie die master-Datenbank wieder her  
  
1.  Starten Sie die Serverinstanz im Einzelbenutzermodus.  
  
     Informationen zum Angeben des Startparameters für Einzelbenutzer (**-m**) finden Sie unter [Konfigurieren von Serverstartoptionen &#40;SQL Server-Konfigurations-Manager&#41;](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md).  
  
2.  Verwenden Sie zum Wiederherstellen einer vollständigen Sicherung der **master**-Datenbank die folgende [RESTORE DATABASE](../../t-sql/statements/restore-statements-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung:  
  
     `RESTORE DATABASE master FROM`  *&lt;Sicherungsgerät&gt;*  `WITH REPLACE`  
  
     Die REPLACE-Option weist [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] an, die angegebene Datenbank wiederherzustellen, selbst wenn eine Datenbank mit dem gleichen Namen bereits vorhanden ist. Die vorhandene Datenbank wird ggf. gelöscht. Für den Einzelbenutzermodus empfiehlt sich die Eingabe der RESTORE DATABASE-Anweisung im [Hilfsprogramm sqlcmd](../../tools/sqlcmd-utility.md). Weitere Informationen finden Sie unter [Verwenden des Hilfsprogramms sqlcmd](../../relational-databases/scripting/sqlcmd-use-the-utility.md).  
  
    > [!IMPORTANT]  
    >  Nach der Wiederherstellung von **master** wird die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] heruntergefahren, und der **sqlcmd** -Prozess wird beendet. Vor dem Neustarten der Serverinstanz muss der Einzelbenutzer-Startparameter entfernt werden. Weitere Informationen finden Sie unter [Konfigurieren von Serverstartoptionen &#40;SQL Server-Konfigurations-Manager&#41;](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md).  
  
3.  Starten Sie die Serverinstanz neu, und setzen Sie andere Wiederherstellungsschritte, z. B. das Wiederherstellen von anderen Datenbanken, das Anfügen von Datenbanken und das Korrigieren von Benutzerkonflikten, fort.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird die `master` -Datenbank auf der Standardserverinstanz wiederhergestellt. In diesem Beispiel wird vorausgesetzt, dass die Serverinstanz bereits im Einzelbenutzermodus ausgeführt wird. Im Beispiel wird `sqlcmd` gestartet, und es wird eine `RESTORE DATABASE` -Anweisung ausgeführt, mit der eine vollständige Datenbanksicherung der `master` -Datenbank vom Datenträgermedium wiederhergestellt wird: `Z:\SQLServerBackups\master.bak`.  
  
> [!NOTE]  
>  Bei einer benannten Instanz muss mit dem **sqlcmd**-Befehl die Option **-S***\<Computername>*\\*\<Instanzname>* angegeben werden.  
  
```  
  
      C:\> sqlcmd  
1> RESTORE DATABASE master FROM DISK = 'Z:\SQLServerBackups\master.bak' WITH REPLACE;  
2> GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Vollständige Datenbankwiederherstellungen &#40;einfaches Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)   
 [Vollständige Datenbankwiederherstellungen &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)   
 [Problembehandlung bei verwaisten Benutzern &#40;SQL Server&#41;](../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md)   
 [Anfügen und Trennen von Datenbanken &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [Neuerstellen von Systemdatenbanken](../../relational-databases/databases/rebuild-system-databases.md)   
 [Startoptionen für den Datenbankmoduldienst](../../database-engine/configure-windows/database-engine-service-startup-options.md)   
 [SQL Server-Konfigurations-Manager](../../relational-databases/sql-server-configuration-manager.md)   
 [Sichern und Wiederherstellen von Systemdatenbanken &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Starten von SQL Server im Einzelbenutzermodus](../../database-engine/configure-windows/start-sql-server-in-single-user-mode.md)  
  
  
