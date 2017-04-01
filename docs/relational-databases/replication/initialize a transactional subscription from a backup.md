---
title: "Initialisieren eines Transaktionsabonnements von einer Sicherung (Replikationsprogrammierung mit Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/29/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "Manuelle Abonnementinitialisierung [SQL Server-Replikation]"
  - "Abonnements [SQL Server-Replikation], initialisieren"
  - "Initialisieren von Abonnements [SQL Server-Replikation], ohne Momentaufnahmen"
  - "Transaktionsreplikation, Sicherung und Wiederherstellung"
  - "Sicherung [SQL Server-Replikation], Transaktionsreplikation"
ms.assetid: d0637fc4-27cc-4046-98ea-dc86b7a3bd75
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Initialisieren eines Transaktionsabonnements von einer Sicherung (Replikationsprogrammierung mit Transact-SQL)
  Obwohl ein Abonnement für eine Transaktionsveröffentlichung in der Regel mit einer Momentaufnahme initialisiert wird, kann ein Abonnement auch mit gespeicherten Replikationsprozeduren von einer Sicherung initialisiert werden. Weitere Informationen finden Sie unter [eine Transaktionsabonnements ohne Momentaufnahme initialisieren](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
### So initialisieren Sie einen Transaktionsabonnenten von einer Sicherung  
  
1.  Für eine vorhandene Veröffentlichung, stellen Sie sicher, dass die Veröffentlichung, die Möglichkeit unterstützt, die durch Ausführen von einer Sicherung initialisieren [Sp_helppublication & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md) auf dem Verleger für die Veröffentlichungsdatenbank. Beachten Sie den Wert der **Allow_initialize_from_backup** im Ergebnis festlegen.  
  
    -   Wenn der Wert **1**ist, unterstützt die Veröffentlichung diese Funktionalität.  
  
    -   Wenn der Wert **0**, führen Sie [Sp_changepublication & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) auf dem Verleger für die Veröffentlichungsdatenbank. Geben Sie den Wert **Allow_initialize_from_backup** für **@property** und einem Wert von **true** für **@value**.  
  
2.  Führen Sie für die neue Publikation [Sp_addpublication & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) auf dem Verleger für die Veröffentlichungsdatenbank. Geben Sie den Wert **true** für **Allow_initialize_from_backup**. Weitere Informationen finden Sie unter [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md).  
  
    > [!WARNING]  
    >  Um zu vermeiden, fehlende Abonnentendaten, bei Verwendung **Sp_addpublication** mit `@allow_initialize_from_backup = N'true'`, verwenden Sie immer `@immediate_sync = N'true'`.  
  
3.  Erstellen Sie eine Sicherung der Datenbank für die Veröffentlichung mit der [BACKUP & #40; Transact-SQL & #41;](../../t-sql/statements/backup-transact-sql.md) -Anweisung.  
  
4.  Wiederherstellen der Sicherung auf dem Abonnenten mithilfe der [RESTORE & #40; Transact-SQL & #41;](../Topic/RESTORE%20\(Transact-SQL\).md) -Anweisung.  
  
5.  Führen Sie die gespeicherte Prozedur auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addsubscription & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Geben Sie die folgenden Parameter an:  
  
    -   **@sync_type** -Wert **Initialisieren mit Sicherung**.  
  
    -   **@backupdevicetype** -der Typ des Sicherungsmediums: **logische** (Standard), **Datenträger**, oder **Band**.  
  
    -   **@backupdevicename** -das logische oder physische Sicherungsmedium für die Wiederherstellung verwenden.  
  
         Geben Sie den Namen des Sicherungsmediums angegeben, wenn für ein logisches Gerät **Sp_addumpdevice** wurde verwendet, um das Gerät zu erstellen.  
  
         Geben Sie für ein physisches Gerät einen vollständigen Pfad und einen Dateinamen an, z. B. `DISK = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\BACKUP\Mybackup.dat'` oder `TAPE = '\\.\TAPE0'`.  
  
    -   (Optional) **@password** -Kennwort, das bereitgestellt wurde, als der Sicherungssatz erstellt wurde.  
  
    -   (Optional) **@mediapassword** -Kennwort, das bereitgestellt wurde, als der Mediensatz formatiert wurde.  
  
    -   (Optional) **@fileidhint** -Bezeichner für den Sicherungssatz wiederhergestellt werden soll. **1** gibt z. B. den ersten Sicherungssatz auf dem Sicherungsmedium an und **2** den zweiten Sicherungssatz.  
  
    -   (Optional für Bandmedien) **@unload** -Geben Sie den Wert **1** (Standard), wenn das Band aus dem Laufwerk entfernt werden soll, nachdem die Wiederherstellung abgeschlossen ist und **0** wenn es nicht entladen werden soll.  
  
6.  (Optional) Führen Sie ein Pullabonnement [Sp_addpullsubscription & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md) und [Sp_addpullsubscription_agent & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md) auf dem Abonnenten für die Abonnementdatenbank. Weitere Informationen finden Sie unter [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
7.  (Optional) Starten Sie den Verteilungs-Agent. Weitere Informationen finden Sie unter [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) oder [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
## Siehe auch  
 [Kopieren von Datenbanken durch Sichern und Wiederherstellen](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)   
 [Sichern und Wiederherstellen von SQL Server-Datenbanken](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
  