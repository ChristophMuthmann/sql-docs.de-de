---
title: Anzeigen der Eigenschaften und des Inhalts eines logischen Sicherungsmediums (SQL Server) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- displaying backup content
- viewing backup content
- database backups [SQL Server], viewing content
- backing up databases [SQL Server], viewing content
- backing up databases [SQL Server], properties
- displaying backup properties
- backup devices [SQL Server], viewing information
- viewing backup properties
- database backups [SQL Server], properties
ms.assetid: 3a309074-e816-454d-b6c3-fcfdde0cbf74
caps.latest.revision: "22"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 332fbe8c9b624e1ca48562236aa09229f21657c8
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="view-the-properties-and-contents-of-a-logical-backup-device-sql-server"></a>Anzeigen der Eigenschaften und des Inhalts eines logischen Sicherungsmediums (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  In diesem Thema wird beschrieben, wie Sie die Eigenschaften und Inhalte von logischen Sicherungsmedien in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]anzeigen können.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Security](#Security)  
  
-   **So zeigen Sie die Eigenschaften und den Inhalt eines logischen Sicherungsmediums an, und zwar mit**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Security"></a> Sicherheit  
 Weitere Informationen zur Sicherheit finden Sie unter [RESTORE LABELONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md).  
  
####  <a name="Permissions"></a> Berechtigungen  
 In [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und höheren Versionen benötigen Sie die CREATE DATABASE-Berechtigung, um Informationen zu Sicherungssätzen oder Sicherungsmedien abzurufen. Weitere Informationen finden Sie unter [GRANT (Datenbankberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md).  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
  
#### <a name="to-view-the-properties-and-contents-of-a-logical-backup-device"></a>So zeigen Sie die Eigenschaften und den Inhalt eines logischen Sicherungsmediums an  
  
1.  Klicken Sie im Objekt-Explorer nach dem Herstellen einer Verbindung mit der entsprechenden Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]auf den Servernamen, um die Serverstruktur zu erweitern.  
  
2.  Erweitern Sie **Serverobjekte**und anschließend **Sicherungsmedien**.  
  
3.  Klicken Sie auf das Gerät, und klicken Sie mit der rechten Maustaste auf **Eigenschaften**. Hierdurch wird das Dialogfeld **Sicherungsmedium** geöffnet.  
  
4.  Auf der Seite **Allgemein** werden der Gerätename und das Ziel angezeigt (entweder ein Bandmedium oder ein Dateipfad).  
  
5.  Klicken Sie im Bereich **Seite auswählen** auf **Medieninhalt**.  
  
6.  Im rechten Vorschaufeld werden folgende Eigenschaftsbereiche angezeigt:  
  
    -   **Medien**  
  
         Mediensequenzinformationen (die Mediensequenznummer, die Sequenznummer der Familie und ggf. der Spiegelungsbezeichner) und das Datum und die Uhrzeit der Medienerstellung.  
  
    -   **Mediensatz**  
  
         Mediensatzinformationen: der Mediensatzname und ggf. die Beschreibung sowie die Anzahl der Familien im Mediensatz.  
  
7.  Das Raster **Sicherungssätze** enthält Informationen zu den Inhalten des Mediensatzes.  
  
> [!NOTE]  
>  Weitere Informationen finden Sie unter [Medieninhalt (Seite)](../../relational-databases/backup-restore/backup-device-media-contents-page.md).  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-view-the-properties-and-contents-of-a-logical-backup-device"></a>So zeigen Sie die Eigenschaften und den Inhalt eines logischen Sicherungsmediums an  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Verwenden Sie die [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md) -Anweisung. In diesem Beispiel werden Informationen zum logischen Sicherungsmedium `AdvWrks2008R2Backup` zurückgegeben:  
  
```sql  
USE AdventureWorks2012 ;  
RESTORE LABELONLY  
   FROM AdvWrks2008R2Backup ;  
GO  
  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [backupfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupfile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [backupmediaset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [backupmediafamily &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [Sicherungsmedien &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)  
  
  
