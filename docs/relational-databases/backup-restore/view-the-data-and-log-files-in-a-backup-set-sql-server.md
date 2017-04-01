---
title: "Anzeigen der Daten und Protokolldateien in einem Sicherungssatz (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/15/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Datenbanksicherungen [SQL Server], Anzeigen von Sicherungssätzen"
  - "Ansehen von Sicherungssatzinformationen"
  - "Sicherungssätze [SQL Server], Anzeigen von Dateien in"
  - "Anzeigen von Sicherungssatzinformationen"
  - "Transaktionsprotokollsicherung [SQL Server], Anzeigen von Sicherungssätzen"
  - "Sichern [SQL Server], Anzeigen von Sicherungssätzen"
ms.assetid: abb6420c-f809-426e-aeb4-d0a74989cf39
caps.latest.revision: 23
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 23
---
# Anzeigen der Daten und Protokolldateien in einem Sicherungssatz (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  In diesem Thema wird beschrieben, wie Sie Daten und Protokolldateien in einem Sicherungssatz in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]anzeigen können.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Sicherheit](#Security)  
  
-   **So zeigen Sie die Daten und Protokolldateien in einem Sicherungssatz an mit**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Security"></a> Sicherheit  
 Weitere Informationen zur Sicherheit finden Sie unter [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../Topic/RESTORE%20FILELISTONLY%20\(Transact-SQL\).md).  
  
####  <a name="Permissions"></a> Berechtigungen  
 In [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und höheren Versionen benötigen Sie die CREATE DATABASE-Berechtigung, um Informationen zu Sicherungssätzen oder Sicherungsmedien abzurufen. Weitere Informationen finden Sie unter [GRANT (Datenbankberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md).  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### So zeigen Sie die Daten und Protokolldateien in einem Sicherungssatz an  
  
1.  Klicken Sie im Objekt-Explorer nach dem Herstellen einer Verbindung mit der entsprechenden Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]auf den Servernamen, um die Serverstruktur zu erweitern.  
  
2.  Erweitern Sie **Datenbanken**, und wählen Sie je nach Datenbank eine Benutzerdatenbank aus, oder erweitern Sie **Systemdatenbanken** , und wählen Sie eine Systemdatenbank aus.  
  
3.  Klicken Sie mit der rechten Maustaste auf die Datenbank, und klicken Sie dann auf **Eigenschaften**. Das Dialogfeld **Datenbankeigenschaften** wird geöffnet.  
  
4.  Klicken Sie im Fensterbereich **Seite auswählen** auf **Dateien**.  
  
5.  Suchen Sie im Bereich **Datenbankdateien** nach einer Liste der Daten- und Protokolldateien und deren Eigenschaften.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### So zeigen Sie die Daten und Protokolldateien in einem Sicherungssatz an  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Verwenden Sie die [RESTORE FILELISTONLY](../Topic/RESTORE%20FILELISTONLY%20\(Transact-SQL\).md) -Anweisung. In diesem Beispiel werden Informationen zum sekundären Sicherungsmedium (`FILE=2`) auf dem `AdventureWorksBackups`-Sicherungsmedium zurückgegeben:  
  
```tsql  
USE AdventureWorks2012 ;  
RESTORE FILELISTONLY FROM AdventureWorksBackups   
   WITH FILE=2;  
GO  
```  
  
## Siehe auch  
 [backupfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupfile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [backupmediaset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [backupmediafamily &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [Sicherungsmedien &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)  
  
  