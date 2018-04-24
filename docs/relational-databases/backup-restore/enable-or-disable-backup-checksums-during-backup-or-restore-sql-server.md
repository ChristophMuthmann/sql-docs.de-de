---
title: Aktivieren oder Deaktivieren von Sicherungsprüfsummen während der Sicherung oder Wiederherstellung (SQL Server) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: backup-restore
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- backup checksums [SQL Server]
- disabling checksums
- checksums [SQL Server]
ms.assetid: 6786bd1e-ad97-430a-8dfb-d4ba952d6c4d
caps.latest.revision: 31
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0d8a69b2767c19c8facbcf7b1b46239bed09b4d2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="enable-or-disable-backup-checksums-during-backup-or-restore-sql-server"></a>Aktivieren oder deaktivieren von Sicherungsprüfsummen während der Sicherung oder Wiederherstellung (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  In diesem Thema wird beschrieben, wie Sie Sicherungsprüfsummen aktivieren oder deaktivieren, wenn Sie eine Datenbank in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]sichern oder wiederherstellen.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Security](#Security)  
  
-   **So aktivieren oder deaktivieren Sie Sicherungsprüfsummen mit**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 BACKUP  
 Mitglieder der festen Serverrolle **sysadmin** und der festen Datenbankrollen **db_owner** und **db_backupoperator** verfügen standardmäßig über BACKUP DATABASE- und BACKUP LOG-Berechtigungen.  
  
 Besitz- und Berechtigungsprobleme im Zusammenhang mit der physischen Datei des Sicherungsmediums können den Sicherungsvorgang beeinträchtigen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muss über Lese- und Schreibberechtigungen für das Medium verfügen. Das Konto, unter dem der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst ausgeführt wird, muss Schreibberechtigungen haben. Allerdings prüft die gespeicherte Prozedur [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md), die den Systemtabellen einen Eintrag für ein Sicherungsmedium hinzufügt, nicht die Dateizugriffsberechtigungen. Solche Probleme mit der physischen Datei des Sicherungsmediums treten möglicherweise erst auf, wenn auf die physische Ressource zugegriffen wird, um einen Sicherungs- oder Wiederherstellungsvorgang auszuführen.  
  
 RESTORE  
 Ist die wiederherzustellende Datenbank nicht vorhanden, muss der Benutzer über CREATE DATABASE-Berechtigungen verfügen, um RESTORE ausführen zu können. Ist die Datenbank vorhanden, werden RESTORE-Berechtigungen standardmäßig den Mitgliedern der festen Serverrollen **sysadmin** und **dbcreator** sowie dem Besitzer (**dbo**) der Datenbank erteilt (für die Option FROM DATABASE_SNAPSHOT ist die Datenbank immer vorhanden).  
  
 RESTORE-Berechtigungen werden Rollen erteilt, in denen Mitgliedsinformationen immer für den Server verfügbar sind. Da die Mitgliedschaft in einer festen Datenbankrolle nur bei unbeschädigten und zugänglichen Datenbanken geprüft werden kann (was beim Ausführen von RESTORE nicht immer der Fall ist), verfügen Mitglieder der festen Datenbankrolle **db_owner** nicht über RESTORE-Berechtigungen.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
  
#### <a name="to-enable-or-disable-checksums-during-a-backup-operation"></a>So aktivieren oder deaktivieren Sie Prüfsummen bei einem Sicherungsvorgang  
  
1.  Führen Sie die Schritte aus, [um eine Datenbanksicherung zu erstellen](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md).  
  
2.  Klicken Sie auf der Seite **Optionen** im Bereich **Zuverlässigkeit** auf **Vor dem Schreiben auf die Medien Prüfsumme bilden**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-enable-or-disable-backup-checksum-for-a-backup-operation"></a>So aktivieren oder deaktivieren Sie Sicherungsprüfsummen bei einem Sicherungsvorgang  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Geben Sie die Option WITH CHECKSUM an, um die Sicherungsprüfsummen in einer [BACKUP](../../t-sql/statements/backup-transact-sql.md) -Anweisung zu aktivieren. Geben Sie die Option WITH NO_CHECKSUM an, um Sicherungsprüfsummen zu deaktivieren. Dies ist das Standardverhalten, außer bei einer komprimierten Sicherung. Im folgenden Beispiel wird angegeben, dass Prüfsummen ausgeführt werden.  
  
```sql  
BACKUP DATABASE AdventureWorks2012   
 TO DISK = 'Z:\SQLServerBackups\AdvWorksData.bak'  
   WITH CHECKSUM;  
GO  
```  
  
#### <a name="to-enable-or-disable-backup-checksum-for-a-restore-operation"></a>So aktivieren oder deaktivieren Sie Sicherungsprüfsummen bei einem Wiederherstellungsvorgang  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Geben Sie die Option WITH CHECKSUM an, um die Sicherungsprüfsummen in einer [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) -Anweisung zu aktivieren. Dies ist das Standardverhalten bei einer komprimierten Sicherung. Geben Sie die Option WITH NO_CHECKSUM an, um Sicherungsprüfsummen zu deaktivieren. Dies ist das Standardverhalten, außer bei einer komprimierten Sicherung. Im folgenden Beispiel wird angegeben, dass Sicherungsprüfsummen ausgeführt werden.  
  
```sql  
RESTORE DATABASE AdventureWorks2012   
 FROM DISK = 'Z:\SQLServerBackups\AdvWorksData.bak'  
   WITH CHECKSUM;  
GO  
```  
  
> [!WARNING]  
>  Wenn Sie ausdrücklich CHECKSUM für einen Wiederherstellungsvorgang anfordern und die Sicherung Sicherungsprüfsummen enthält, werden sowohl die Sicherungsprüfsummen als auch die Seitenprüfsummen wie beim Standardfall überprüft. Wenn allerdings im Sicherungssatz keine Sicherungsprüfsummen vorhanden sind, wird vom Wiederherstellungsvorgang eine entsprechende Fehlermeldung ausgelöst.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)   
 [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)   
 [RESTORE LABELONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [RESTORE Arguments &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)   
 [Mögliche Medienfehler während der Sicherung und Wiederherstellung &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md)   
 [Angeben, ob ein Sicherungs- oder Wiederherstellungsvorgang fortgesetzt wird, nachdem ein Fehler festgestellt wurde &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-if-backup-or-restore-continues-or-stops-after-error.md)  
  
  
