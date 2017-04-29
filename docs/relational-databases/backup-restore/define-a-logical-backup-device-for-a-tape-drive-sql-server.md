---
title: "Definieren eines logischen Sicherungsmediums für ein Bandlaufwerk (SQL Server) | Microsoft-Dokumentation"
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
- backup devices [SQL Server], defining
- backup devices [SQL Server], tapes
- backing up databases [SQL Server], tapes
- database backups [SQL Server], tapes
- tape backup devices, creating
ms.assetid: 66f36e1d-0287-4fac-8a51-71f9f0d7ad5b
caps.latest.revision: 38
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c0584680550617726042122f2d18dc7e967d88dc
ms.lasthandoff: 04/11/2017

---
# <a name="define-a-logical-backup-device-for-a-tape-drive-sql-server"></a>Definieren eines logischen Sicherungsmediums für ein Bandlaufwerk (SQL Server)
  In diesem Thema wird beschrieben, wie Sie ein logisches Sicherungsmedium für ein Bandlaufwerk in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]definieren. Ein logisches Medium ist ein benutzerdefinierter Name, der auf ein bestimmtes, physisches Sicherungsmedium (Datenträgerdatei oder Bandlaufwerk) verweist.  Die Initialisierung des physischen Mediums erfolgt später, wenn eine Sicherung auf das Sicherungsmedium geschrieben wird.  
  
> [!NOTE]  
>  Die Unterstützung für Bandsicherungsgeräte wird in zukünftigen Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]entfernt. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   **So definieren Sie ein logisches Sicherungsmedium für ein Bandlaufwerk mit**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Das Bandlaufwerk bzw. die -laufwerke müssen vom Betriebssystem Microsoft Windows unterstützt werden.  
  
-   Das Bandmedium muss physisch mit dem Computer verbunden sein, auf dem eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ausgeführt wird. Das Sichern auf Remotebandmedien wird nicht unterstützt.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Serverrolle **diskadmin** .  
  
 Erfordert die Berechtigung zum Schreiben auf den Datenträger.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-define-a-logical-backup-device-for-a-tape-drive"></a>So definieren Sie ein logisches Sicherungsmedium für ein Bandlaufwerk  
  
1.  Klicken Sie im Objekt-Explorer nach dem Herstellen einer Verbindung mit der entsprechenden Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]auf den Servernamen, um die Serverstruktur zu erweitern.  
  
2.  Erweitern Sie **Serverobjekte**, und klicken Sie dann mit der rechten Maustaste auf **Sicherungsmedien**.  
  
3.  Klicken Sie auf **Neues Sicherungsmedium**, um das Dialogfeld **Sicherungsmedium** zu öffnen.  
  
4.  Geben Sie einen Mediennamen ein.  
  
5.  Klicken Sie für das Ziel auf **Band** , und wählen Sie ein Bandlaufwerk aus, das noch keinem anderen Sicherungsmedium zugeordnet ist. Falls keine Bandlaufwerke verfügbar sind, ist die Option **Band** deaktiviert.  
  
6.  Klicken Sie auf **OK**, um das neue Medium zu definieren.  
  
 Damit eine Sicherung auf dieses neue Medium erstellt werden kann, fügen Sie es dem Feld **Sichern auf:** im Dialogfeld **Datenbank sichern** (Seite **Allgemein**) hinzu. Weitere Informationen finden Sie unter [Erstellen einer vollständigen Datenbanksicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md).  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-define-a-logical-backup-device-for-a-tape-drive"></a>So definieren Sie ein logisches Sicherungsmedium für ein Bandlaufwerk  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird gezeigt, wie Sie [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md) verwenden müssen, um ein logisches Sicherungsmedium für ein Band zu definieren. Im folgenden Beispiel wird das Bandsicherungsmedium `tapedump1`mit dem physischen Namen `\\.\tape0`hinzugefügt.  
  
```tsql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_addumpdevice 'tape', 'tapedump1', '\\.\tape0' ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [sys.backup_devices &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [sp_dropdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdevice-transact-sql.md)   
 [Sicherungsmedien &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [Definieren eines logischen Sicherungsmediums für eine Datenträgerdatei &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)   
 [Anzeigen der Eigenschaften und des Inhalts eines logischen Sicherungsmediums &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
  
