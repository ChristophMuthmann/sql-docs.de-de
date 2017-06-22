---
title: Wiederherstellen einer Datenbanksicherung unter dem einfachen Wiederherstellungsmodell (Transact-SQL) | Microsoft-Dokumentation
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
- full backups [SQL Server]
- database restores [SQL Server], full backups
- backing up databases [SQL Server], full backups
- database backups [SQL Server], full backups
- restoring databases [SQL Server], full backups
ms.assetid: a928fa36-e285-476f-9a7b-6840a8bb7283
caps.latest.revision: 39
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4896b42ecb2cf372930f4691f20fe4b4e006f3e4
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="restore-a-database-backup-under-the-simple-recovery-model-transact-sql"></a>Wiederherstellen einer Datenbanksicherung unter dem einfachen Wiederherstellungsmodell (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  In diesem Thema wird erläutert, wie eine vollständige Datenbanksicherung wiederhergestellt wird.  
  
> [!IMPORTANT]  
>  Nur der Systemadministrator, der die vollständige Datenbanksicherung wiederherstellt, darf die wiederherzustellende Datenbank aktuell verwenden.  
  
## <a name="prerequisites-and-recommendations"></a>Voraussetzungen und Empfehlungen  
  
-   Um eine verschlüsselte Datenbank wiederherstellen zu können, muss das Zertifikat oder der asymmetrische Schlüssel verfügbar sein, das oder der zum Verschlüsseln der Datenbank verwendet wurde. Ohne das Zertifikat oder den asymmetrischen Schlüssel kann die Datenbank nicht wiederhergestellt werden. Darum muss das Zertifikat, das zur Verschlüsselung des Verschlüsselungsschlüssels für die Datenbank verwendet wurde, so lange beibehalten werden, wie die Sicherung benötigt wird. Weitere Informationen finden Sie unter [SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).  
  
-   Aus Sicherheitsgründen empfiehlt es sich nicht, Datenbanken aus unbekannten oder nicht vertrauenswürdigen Quellen anzufügen oder wiederherzustellen. Solche Datenbanken können bösartigen Code enthalten, der möglicherweise unbeabsichtigten [!INCLUDE[tsql](../../includes/tsql-md.md)] -Code ausführt oder Fehler verursacht, indem er das Schema oder die physische Datenbankstruktur ändert. Bevor Sie eine Datenbank aus einer unbekannten oder nicht vertrauenswürdigen Quelle verwenden, führen Sie auf einem Nichtproduktionsserver [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) für die Datenbank aus. Überprüfen Sie außerdem den Code in der Datenbank, z.B. gespeicherte Prozeduren oder anderen benutzerdefinierten Code.  
  
## <a name="database-compatibility-level-after-upgrade"></a>Datenbank-Kompatibilitätsgrad nach dem Upgrade  
 Der Kompatibilitätsgrad der Datenbanken **tempdb**, **model**, **msdb** und **Resource** wird nach dem Upgrade auf [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] festgelegt. Die **master** -Systemdatenbank behält den Kompatibilitätsgrad bei, der vor dem Upgrade bestand, sofern dieser nicht unter 100 lag. War der Kompatibilitätsgrad von **master** vor dem Upgrade geringer als 100, wird er nach dem Upgrade auf 100 festgelegt.  
  
 War der Kompatibilitätsgrad einer Benutzerdatenbank vor dem Upgrade 100 oder höher, wird er nach dem Upgrade beibehalten. War der Kompatibilitätsgrad der aktualisierten Datenbank vor dem Upgrade 90, wird er auf 100 gesetzt, was dem niedrigsten unterstützten Kompatibilitätsgrad in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]entspricht.  
  
> [!NOTE]  
>  Neue Benutzerdatenbanken erben den Kompatibilitätsgrad der **model** -Datenbank.  
  
## <a name="procedures"></a>Vorgehensweisen  
  
#### <a name="to-restore-a-full-database-backup"></a>So stellen Sie eine vollständige Datenbanksicherung wieder her  
  
1.  Führen Sie die RESTORE DATABASE-Anweisung aus, um die vollständige Datenbanksicherung wiederherzustellen, und geben Sie dabei Folgendes an:  
  
    -   Den Namen der wiederherzustellenden Datenbank.  
  
    -   Das Sicherungsmedium, von dem die vollständige Datenbanksicherung wiederhergestellt wird  
  
    -   Die NORECOVERY-Klausel, wenn nach dem Wiederherstellen der vollständigen Datenbanksicherung eine Transaktionsprotokollsicherung oder eine differenzielle Datenbanksicherung angewendet werden soll.  
  
    > [!IMPORTANT]  
    >  Um eine verschlüsselte Datenbank wiederherstellen zu können, muss das Zertifikat oder der asymmetrische Schlüssel verfügbar sein, das oder der zum Verschlüsseln der Datenbank verwendet wurde. Ohne das Zertifikat oder den asymmetrischen Schlüssel kann die Datenbank nicht wiederhergestellt werden. Darum muss das Zertifikat, das zur Verschlüsselung des Verschlüsselungsschlüssels für die Datenbank verwendet wurde, so lange beibehalten werden, wie die Sicherung benötigt wird. Weitere Informationen finden Sie unter [SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).  
  
2.  Geben Sie wahlweise Folgendes an:  
  
    -   Die FILE-Klausel, um den Sicherungssatz auf dem wiederherzustellenden Sicherungsmedium zu identifizieren.  
  
> [!NOTE]  
>  Wenn Sie eine Datenbank einer früheren Version nach [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]wiederherstellen, wird die Datenbank automatisch aktualisiert. In der Regel ist die Datenbank sofort verfügbar. Wenn eine [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] -Datenbank aber Volltextindizes aufweist, werden diese beim Upgrade entweder importiert, zurückgesetzt oder neu erstellt, je nach der Einstellung der Servereigenschaft  **upgrade_option** . Wenn die Upgradeoption auf „Importieren“ (**upgrade_option** = 2) oder „Neu erstellen“ (**upgrade_option** = 0) festgelegt ist, sind die Volltextindizes während des Upgrades nicht verfügbar. Je nach Menge der indizierten Daten kann der Importvorgang mehrere Stunden dauern; die Neuerstellung sogar bis zu zehnmal länger. Wenn die Upgradeoption auf Importieren festgelegt ist und kein Volltextkatalog verfügbar ist, werden die zugehörigen Volltextindizes neu erstellt. Verwenden Sie **sp_fulltext_service** , um die Einstellung der Servereigenschaft [upgrade_option](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)zu ändern.  
  
## <a name="example"></a>Beispiel  
  
### <a name="description"></a>Beschreibung  
 In diesem Beispiel wird die vollständige Datenbanksicherung der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank von Band wiederhergestellt:  
  
### <a name="example"></a>Beispiel  
  
```  
USE master;  
GO  
RESTORE DATABASE AdventureWorks2012  
   FROM TAPE = '\\.\Tape0';  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Vollständige Datenbankwiederherstellungen &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)   
 [Vollständige Datenbankwiederherstellungen &#40;einfaches Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)   
 [Vollständige Datenbanksicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-database-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Sicherungsverlauf und Headerinformationen &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)   
 [Neuerstellen von Systemdatenbanken](../../relational-databases/databases/rebuild-system-databases.md)  
  
  
