---
title: Initialisieren eines Transaktionsabonnements von einer Sicherung | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: TSQL
helpviewer_keywords:
- manual subscription initialization [SQL Server replication]
- subscriptions [SQL Server replication], initializing
- initializing subscriptions [SQL Server replication], without snapshots
- transactional replication, backup and restore
- backups [SQL Server replication], transactional replication
ms.assetid: d0637fc4-27cc-4046-98ea-dc86b7a3bd75
caps.latest.revision: "36"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a596c496c34937a6237ed059032a8b2a43d04ea0
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="initialize-a-transactional-subscription-from-a-backup"></a>Initialisieren eines Transaktionsabonnements von einer Sicherung
  Obwohl ein Abonnement für eine Transaktionsveröffentlichung in der Regel mit einer Momentaufnahme initialisiert wird, kann ein Abonnement auch mit gespeicherten Replikationsprozeduren von einer Sicherung initialisiert werden. Weitere Informationen finden Sie unter [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)initialisiert wird.  
  
### <a name="to-initialize-a-transactional-subscriber-from-a-backup"></a>So initialisieren Sie einen Transaktionsabonnenten von einer Sicherung  
  
1.  Stellen Sie bei einer bestehenden Veröffentlichung sicher, dass die Veröffentlichung die Fähigkeit unterstützt, von einer Sicherung initialisieren zu können. Führen Sie dazu [sp_helppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md) auf dem Verleger für die Veröffentlichungsdatenbank aus. Notieren Sie den Wert von **allow_initialize_from_backup** im Resultset.  
  
    -   Wenn der Wert **1**ist, unterstützt die Veröffentlichung diese Funktionalität.  
  
    -   Ist der Wert **0**, führen Sie [sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) auf dem Verleger für die Veröffentlichungsdatenbank aus. Geben Sie den Wert **allow_initialize_from_backup** für **@property** und den Wert **true** für **@value**.  
  
2.  Führen Sie für eine neue Veröffentlichung [sp_addpublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) auf dem Verleger für die Veröffentlichungsdatenbank aus. Geben Sie den Wert **true** für **allow_initialize_from_backup**an. Weitere Informationen finden Sie unter [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md).  
  
    > [!WARNING]  
    >  Um fehlende Abonnentendaten zu vermeiden, wenn Sie **sp_addpublication** mit `@allow_initialize_from_backup = N'true'`verwenden, sollten Sie immer `@immediate_sync = N'true'`verwenden.  
  
3.  Erstellen Sie mit der [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)-Anweisung eine Sicherung der Veröffentlichungsdatenbank.  
  
4.  Stellen Sie die Sicherung auf dem Abonnenten mit der [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)-Anweisung wieder her.  
  
5.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank die gespeicherte Prozedur [sp_addsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) aus. Geben Sie die folgenden Parameter an:  
  
    -   **@sync_type** &ndash; der Wert **initialize with backup**.  
  
    -   **@backupdevicetype** &ndash; der Typ des Sicherungsmediums: **logical** (Standard), **disk**oder **tape**.  
  
    -   **@backupdevicename** &ndash; das logische oder physische Sicherungsmedium, das für den Wiederherstellungsvorgang verwendet wird.  
  
         Für ein logisches Gerät geben Sie den Namen des Sicherungsmediums an, der beim Erstellen des Geräts mit **sp_addumpdevice** festgelegt wurde.  
  
         Geben Sie für ein physisches Gerät einen vollständigen Pfad und einen Dateinamen an, z. B. `DISK = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\BACKUP\Mybackup.dat'` oder `TAPE = '\\.\TAPE0'`.  
  
    -   (Optional) **@password** &ndash; ein Kennwort, das bereitgestellt wurde, als der Sicherungssatz erstellt wurde.  
  
    -   (Optional) **@mediapassword** &ndash; ein Kennwort, das bereitgestellt wurde, als der Mediensatz formatiert wurde.  
  
    -   (Optional) **@fileidhint** &ndash; Bezeichner für den Sicherungssatz, der wiederhergestellt werden soll. **1** gibt z. B. den ersten Sicherungssatz auf dem Sicherungsmedium an und **2** den zweiten Sicherungssatz.  
  
    -   (Optional für Bandmedien) **@unload** &ndash; Geben Sie den Wert **1** (Standardwert) an, wenn das Band nach Abschluss der Wiederherstellung aus dem Laufwerk ausgegeben werden soll, und **0** , wenn es nicht ausgegeben werden soll.  
  
6.  (Optional) Führen Sie für ein Pullabonnement [sp_addpullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md) und [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md) im Abonnenten für die Abonnementdatenbank aus. Weitere Informationen finden Sie unter [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
7.  (Optional) Starten Sie den Verteilungs-Agent. Weitere Informationen finden Sie unter [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) oder [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Kopieren von Datenbanken durch Sichern und Wiederherstellen](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)   
 [Sichern und Wiederherstellen von SQL Server-Datenbanken](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
  
