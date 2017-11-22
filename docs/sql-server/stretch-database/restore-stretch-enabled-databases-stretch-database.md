---
title: Wiederherstellen von Stretch-aktivierten Datenbanken (Stretch Database) | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/06/2016
ms.prod: stretch-database
ms.prod_service: sql-non-specified
ms.service: database-engine
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-stretch
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cebc1f6d-d5ea-460d-ae60-d047d29c2723
caps.latest.revision: "15"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b6f86b3d181ee105d3b7aaab7967ac9bada448b5
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="restore-stretch-enabled-databases-stretch-database"></a>Wiederherstellen von Stretch-aktivierten Datenbanken (Stretch Database)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Das Wiederherstellen einer gesicherten Datenbank ist nach vielen Arten von Fehlern, Ausfällen und Notfällen unerlässlich.
  
  Weitere Informationen finden Sie unter [Sichern von Stretch-aktivierten Datenbanken](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md).

> [!TIP]
> Backup ist nur ein Teil einer umfassenden Lösung für Hochverfügbarkeit und Geschäftskontinuität. Weitere Informationen zu Hochverfügbarkeit finden Sie unter [Lösungen mit Hochverfügbarkeit](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md).

## <a name="restore-your-sql-server-data"></a>Wiederherstellen der SQL Server-Daten
Nach einem Hardwareausfall oder einer Beschädigung stellen Sie die Stretch-aktivierte SQL Server-Datenbank aus einer Sicherung wieder her. Dafür können Sie die derzeit verwendeten und üblichen SQL Server-Wiederherstellungsmethoden verwenden. Weitere Informationen finden Sie unter [Übersicht über Wiederherstellungsvorgänge](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md).

Nach der Wiederherstellung der SQL Server-Datenbank müssen Sie die gespeicherte Prozedur **sys.sp_rda_reauthorize_db** ausführen, um die Verbindung zwischen der Stretch-aktivierten SQL Server-Datenbank und der Azure-Remotedatenbank erneut herzustellen. Weitere Informationen finden Sie unter [Wiederherstellen der Verbindung zwischen der SQL Server-Datenbank und der Azure-Remotedatenbank](#reconnect).

## <a name="restore-your-remote-azure-data"></a>Wiederherstellen der Azure-Remotedaten

### <a name="recover-a-live-azure-database"></a>Wiederherstellen einer Azure-Livedatenbank
Der SQL Server Stretch Database-Dienst in Azure verwendet Azure Storage-Momentaufnahmen, um mindestens alle acht Stunden eine Momentaufnahme aller Livedaten zu erstellen. Diese Momentaufnahmen werden sieben Tage lang aufbewahrt. Dadurch können Sie Ihre Daten von mindestens 21 Wiederherstellungspunkten in den letzten sieben Tagen wiederherstellen – bis zum Zeitpunkt der Erstellung der letzten Momentaufnahme.

Um eine Azure-Livedatenbank im Azure-Portal in einem Zustand wiederherzustellen, den sie zu einem früheren Zeitpunkt hatte, führen Sie folgende Schritte aus:

1. Melden Sie sich beim [Azure-Portal][]an.
2. Wählen Sie auf der linken Seite des Fensters **DURCHSUCHEN** , und wählen Sie dann **SQL-Datenbanken**aus.
3. Navigieren Sie zu Ihrer Datenbank, und wählen Sie sie aus.
4. Klicken Sie oben im Blatt für die Datenbank auf **Wiederherstellen**.
5. Geben Sie einen neuen **Datenbanknamen**an, wählen Sie einen **Wiederherstellungspunkt** aus, und klicken Sie dann auf **Erstellen**.
6. Der Wiederherstellungsvorgang für die Datenbank beginnt und kann mithilfe von **BENACHRICHTIGUNGEN**überwacht werden.

### <a name="recover-a-deleted-azure-database"></a>Wiederherstellen einer gelöschten Azure-Datenbank
Der SQL Server Stretch Database-Dienst in Azure erstellt vor dem Löschen einer Datenbank eine Datenbank-Momentaufnahme und bewahrt diese sieben Tage lang auf. Danach werden keine Momentaufnahmen der Livedatenbank mehr aufbewahrt. Dadurch können Sie eine gelöschte Datenbank in dem Zustand wiederherstellen, den sie zum Zeitpunkt des Löschens hatte.

Um eine gelöschte Azure-Datenbank im Azure-Portal in dem Zustand wiederherzustellen, den sie zum Zeitpunkt des Löschens hatte, führen Sie folgende Schritte aus:

1. Melden Sie sich beim [Azure-Portal][]an.
2. Wählen Sie auf der linken Seite des Fensters **DURCHSUCHEN** , und wählen Sie dann **Server mit SQL Server**aus.
3. Navigieren Sie zu Ihrem Server, und wählen Sie ihn aus.
4. Scrollen Sie auf dem Blatt für Ihren Server nach unten zu den Vorgängen, und klicken Sie auf die Kachel **Gelöschte Datenbanken** .
5. Wählen Sie die gelöschte Datenbank aus, die Sie wiederherstellen möchten.
5. Geben Sie einen neuen **Datenbanknamen** an, und klicken Sie auf **Erstellen**.
6. Der Wiederherstellungsvorgang für die Datenbank beginnt und kann mithilfe von **BENACHRICHTIGUNGEN**überwacht werden.

## <a name="reconnect"></a>Wiederherstellen der Verbindung zwischen der SQL Server-Datenbank und der Azure-Remotedatenbank

1.  Wenn Sie eine Verbindung mit einer wiederhergestellten Azure-Datenbank herstellen möchten, die einen anderen Namen hat oder sich in einer anderen Region befindet, müssen Sie die gespeicherte Prozedur [sys.sp_rda_deauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md) ausführen, um die Verbindung mit der vorherigen Azure-Datenbank zu trennen.  
  
2.  Führen Sie die gespeicherte Prozedur [sys.sp_rda_reauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) aus, um die lokale Stretch-aktivierte Datenbank erneut mit Azure zu verbinden.  
  
    -   Geben Sie die vorhandenen datenbankbezogenen Anmeldeinformationen als sysname- oder varchar (128)-Wert an. (Verwenden Sie nicht varchar(max).) Sie können den Anmeldeinformationsnamen in der Sicht **sys.database_scoped_credentials** nachschlagen.  
  
    -   Geben Sie an, ob eine Kopie der Remotedaten erstellt und eine Verbindung mit der Kopie hergestellt werden soll (empfohlen).  
  
    ```sql  
    USE <Stretch-enabled database name>;
    GO
    EXEC sp_rda_reauthorize_db
        @credential = N'<existing_database_scoped_credential_name>',
        @with_copy = 1 ;  
    GO  
    ```  
    
  ## <a name="see-also"></a>Siehe auch  
 [Sichern von Stretch-aktivierten Datenbanken](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md)  
 [Verwalten und Problembehandlung von Stretch Database](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)   
 [sys.sp_rda_reauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) 
 [sys.sp_rda_deauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)  
 [Sichern und Wiederherstellen von SQL Server-Datenbanken](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
 
 [Azure-Portal]: https://portal.azure.com/
 
