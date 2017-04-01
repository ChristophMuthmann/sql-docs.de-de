---
title: "L&#246;schen eines Sicherungsmediums (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Datenbanksicherungen [SQL Server], Löschen von Medien"
  - "Sicherungsmedien [SQL Server], löschen"
  - "Löschen von Sicherungsmedien"
  - "Entfernen von Sicherungsmedien"
  - "Sichern von Datenbanken [SQL Server], Sicherungsmedien"
ms.assetid: 7be62480-ed6a-4262-a071-1feba73b1c02
caps.latest.revision: 30
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 30
---
# L&#246;schen eines Sicherungsmediums (SQL Server)
  In diesem Thema wird beschrieben, wie Sie ein Sicherungsmedium in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]löschen können.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Sicherheit](#Security)  
  
-   **So löschen Sie ein Sicherungsmedium mit**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Serverrolle **diskadmin** .  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### So löschen Sie ein Sicherungsmedium  
  
1.  Klicken Sie im Objekt-Explorer nach dem Herstellen einer Verbindung mit der entsprechenden Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]auf den Servernamen, um die Serverstruktur zu erweitern.  
  
2.  Erweitern Sie **Serverobjekte**und anschließend **Sicherungsmedien**.  
  
3.  Klicken Sie mit der rechten Maustaste auf das gewünschte Medium, und klicken Sie dann auf **Löschen**.  
  
4.  Überprüfen Sie im Dialogfeld **Objekt löschen** , ob in der Spalte **Objektname** der richtige Medienname angezeigt wird.  
  
5.  Klicken Sie auf **OK**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### So löschen Sie ein Sicherungsmedium  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, und fügen Sie es in das Abfragefenster ein. In diesem Beispiel wird gezeigt, wie [sp_dropdevice](../../relational-databases/system-stored-procedures/sp-dropdevice-transact-sql.md) verwendet werden muss, um ein Sicherungsmedium zu löschen. Führen Sie das erste Beispiel aus, um das `mybackupdisk` -Sicherungsmedium und den physischen Namen `c:\backup\backup1.bak`zu erstellen. Führen Sie **sp_dropdevice** aus, um das `mybackupdisk`-Sicherungsmedium zu löschen. Der physische Namen wird vom `delfile`-Parameter gelöscht.  
  
```tsql  
--Define a backup device and physical name.   
USE AdventureWorks2012 ;  
GO  
EXEC sp_addumpdevice 'disk', 'mybackupdisk', 'c:\backup\backup1.bak' ;  
GO  
--Delete the backup device and the physical name.  
USE AdventureWorks2012 ;  
GO  
EXEC sp_dropdevice ' mybackupdisk ', 'delfile' ;  
GO  
  
```  
  
## Siehe auch  
 [Anzeigen der Eigenschaften und des Inhalts eines logischen Sicherungsmediums &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)   
 [sys.backup_devices &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Sicherungsmedien &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)  
  
  