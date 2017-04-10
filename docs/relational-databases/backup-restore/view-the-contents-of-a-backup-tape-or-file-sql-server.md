---
title: "Anzeigen der Inhalte eines Sicherungsbands oder einer -datei (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Sicherungsmedien [SQL Server], Bänder"
  - "Anzeigen des Sicherungsinhalts"
  - "Anzeigen des Sicherungsinhalts"
  - "Bandsicherungsgeräte, Anzeigen des Inhalts"
  - "Datenbanksicherungen [SQL Server], Anzeigen des Inhalts"
  - "Sichern von Datenbanken [SQL Server], Anzeigen des Inhalts"
ms.assetid: cd6674a2-ca55-4b5a-a971-878ba001821e
caps.latest.revision: 31
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 31
---
# Anzeigen der Inhalte eines Sicherungsbands oder einer -datei (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  In diesem Thema wird beschrieben, wie Sie den Inhalt eines Sicherungsbands oder einer -datei in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]anzeigen können.  
  
> [!NOTE]  
>  Die Unterstützung für Bandsicherungsmedien wird in zukünftigen Versionen von SQL Server entfernt. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Sicherheit](#Security)  
  
-   **So zeigen Sie den Inhalt eines Sicherungsbands oder einer -datei an mit**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Security"></a> Sicherheit  
 Weitere Informationen zur Sicherheit finden Sie unter [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../Topic/RESTORE%20HEADERONLY%20\(Transact-SQL\).md).  
  
####  <a name="Permissions"></a> Berechtigungen  
 In [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und höheren Versionen benötigen Sie die CREATE DATABASE-Berechtigung, um Informationen zu Sicherungssätzen oder Sicherungsmedien abzurufen. Weitere Informationen finden Sie unter [GRANT (Datenbankberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md).  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### So zeigen Sie den Inhalt eines Sicherungsbands oder einer Sicherungsdatei an  
  
1.  Klicken Sie im Objekt-Explorer nach dem Herstellen einer Verbindung mit der entsprechenden Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]auf den Servernamen, um die Serverstruktur zu erweitern.  
  
2.  Erweitern Sie **Datenbanken**, und wählen Sie je nach Datenbank eine Benutzerdatenbank aus, oder erweitern Sie **Systemdatenbanken** , und wählen Sie eine Systemdatenbank aus.  
  
3.  Klicken Sie mit der rechten Maustaste auf die Datenbank, die Sie sichern möchten, zeigen Sie auf **Tasks**, und klicken Sie dann auf **Sichern**. Das Dialogfeld **Datenbank sichern** wird angezeigt.  
  
4.  Klicken Sie auf der Seite **Allgemein** im Abschnitt **Ziel** auf **Datenträger** oder auf **Band**. Suchen Sie im Listenfeld **Sichern auf** nach der gewünschten Datenträgerdatei oder dem gewünschten Band.  
  
     Falls die Datenträgerdatei oder das Band nicht im Listenfeld angezeigt wird, klicken Sie auf **Hinzufügen**. Wählen Sie einen Dateinamen oder ein Bandlaufwerk aus. Klicken Sie auf **OK**, um ihn bzw. es dem Listenfeld **Sichern auf** hinzuzufügen.  
  
5.  Wählen Sie im Listenfeld **Sichern auf** den Pfad des Datenträgers oder Bandlaufwerkes aus, den/das Sie anzeigen möchten, und klicken Sie auf **Inhalt**. Das Dialogfeld **Medieninhalt** wird geöffnet.  
  
6.  Im rechten Fensterbereich werden Informationen zum Mediensatz und zu den Sicherungssätzen auf dem ausgewählten Band oder in der ausgewählten Datei angezeigt.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### So zeigen Sie den Inhalt eines Sicherungsbands oder einer Sicherungsdatei an  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Verwenden Sie die [](../Topic/RESTORE%20HEADERONLY%20\(Transact-SQL\).md) RESTORE HEADERONLY-Anweisung. In diesem Beispiel werden Informationen über die Datei `AdventureWorks2012-FullBackup.bak` zurückgegeben:  
  
```tsql  
USE AdventureWorks2012;  
RESTORE HEADERONLY   
FROM DISK = N'C:\AdventureWorks2012-FullBackup.bak' ;  
GO  
```  
  
## Siehe auch  
 [backupfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupfile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [backupmediaset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [backupmediafamily &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [Sicherungsmedien &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [Definieren eines logischen Sicherungsmediums für eine Datenträgerdatei &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)   
 [Definieren eines logischen Sicherungsmediums für ein Bandlaufwerk &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
  