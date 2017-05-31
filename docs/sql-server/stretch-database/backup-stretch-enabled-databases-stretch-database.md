---
title: Sichern von Stretch-aktivierten Datenbanken (Stretch-Datenbank) | Microsoft-Dokumentation
ms.custom:
- SQL2016_New_Updated
ms.date: 06/14/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Stretch Database, backing up
- backups (Stretch Database)
ms.assetid: 18f0dff0-d8ce-4bee-a935-76ed6dfb3208
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b68a341cc6fb8e01d93b19eb0d7a6a69213af3ba
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="backup-stretch-enabled-databases-stretch-database"></a>Sichern von Datenbanken, für die die Funktion „Stretch-Datenbank“ aktiviert wurde (Stretch-Datenbank)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

 Datenbanksicherungen erleichtern de Wiederherstellung nach verschiedensten Fehlern und Notfällen.  
  
 -   Daher sollten Sie die SQL Server-Datenbanken mit aktivierter Stretch-Datenbank-Funktion sichern.  
      
 -   Microsoft Azure sichert automatisch die Remotedaten, die Stretch-Datenbank von SQL Server zu Azure migriert hat.  

> [!TIP]
> Die Sicherung ist nur ein Teil einer umfassenden Lösung für hohe Verfügbarkeit und Geschäftskontinuität. Weitere Informationen zu hoher Verfügbarkeit finden Sie unter [Lösungen mit hoher Verfügbarkeit](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md).
   
## <a name="back-up-your-sql-server-data"></a>Sichern Ihrer SQL Server-Daten  
  
Zum Sichern Ihrer SQL Server-Datenbanken, für die Stretch-Datenbank aktiviert wurde, können Sie weiterhin die SQL Server-Sicherungsmethoden verwenden, die Sie derzeit verwenden. Weitere Informationen finden Sie unter [Sichern und Wiederherstellen von SQL Server-Datenbanken](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md).
  
 Sicherungen von SQL Server-Datenbanken mit aktivierter Stretch-Datenbank-Funktion enthalten nur lokale Daten und nur Daten, die zu dem Zeitpunkt der Sicherung migriert werden dürfen. (Zur Migration berechtigte Daten sind Daten, die noch nicht migriert wurden. Sie werden jedoch basierend auf den Migrationseinstellungen der Tabellen zu Azure migriert.) Dies wird als **flaches** Sichern bezeichnet und berücksichtigt nicht Ihre bereits zu Azure migrierten Daten.  
  
## <a name="back-up-your-remote-azure-data"></a>Sichern Ihrer Azure-Remotedaten   
  
Microsoft Azure sichert automatisch die Remotedaten, die Stretch-Datenbank von SQL Server zu Azure migriert hat.    
### <a name="azure-reduces-the-risk-of-data-loss-with-automatic-backup"></a>Azure reduziert das Risiko eines Datenverlusts durch das automatische Sichern  
Der SQL Server-Stretch-Datenbankdienst in Azure schützt Ihre Remotedatenbanken durch automatische Speichermomentaufnahmen, die mindestens alle acht Stunden aufgenommen werden. Jede Momentaufnahme wird sieben Tage lang beibehalten, um den größtmöglichen Bereich von möglichen Wiederherstellungspunkten für Sie bereitzustellen.  
  
### <a name="azure-reduces-the-risk-of-data-loss-with-geo-redundancy"></a>Azure reduziert das Risiko eines Datenverlusts durch Georedundanz  
Datenbanksicherungen in Azure werden im georedundanten Azure-Speicher (Read-Access Geo Redundant-Speicher; RA-GRS) gespeichert und sind daher standardmäßig georedundant. Georedundanter Speicher repliziert Ihre Daten in eine sekundäre Region, die Hunderte von Meilen von der primären Region entfernt ist. In primären und sekundären Regionen werden Ihre Daten jeweils dreimal in separaten Fehler- und Upgradedomänen repliziert. Dadurch wird sichergestellt, dass Ihre Daten erhalten bleiben, sogar im Falle eines vollständigen, regionalen Stromausfalls oder eines Notfalls, der eine ganze Region unzugänglich macht.

### <a name="stretchRPO"></a>Stretch-Datenbank reduziert das Risiko eines Verlusts Ihrer Azure-Daten, indem migrierte Zeilen vorübergehend beibehalten werden.
Nachdem Stretch-Datenbank geeignete Zeilen aus SQL Server zu Azure migriert hat, behält es diese Zeilen für mindestens 8 Stunden in der Stagingtabelle bei. Wenn Sie eine Sicherung Ihrer Azure-Datenbank wiederherstellen, nutzt Stretch-Datenbank die Zeilen in der Stagingtabelle, um SQL Server- und Azure-Datenbanken abzustimmen.

Nach der Wiederherstellung einer Ihrer Azure-Datenbanksicherungen müssen Sie die gespeicherte Prozedur [sys.sp_rda_reauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) ausführen, um eine SQL Server-Datenbank, für die Stretch-Datenbank aktiviert wurde, wieder mit der Azure-Remotedatenbank zu verbinden. Beim Ausführen von **sys.sp_rda_reauthorize_db**stimmt Stretch-Datenbank automatisch die SQL Server- mit den Azure-Datenbanken ab.

Führen Sie zum Erhöhen der Stundenzahl, in der Stretch-Datenbank migrierte Daten vorübergehend in der Stagingtabelle beibehält, die gespeicherte Prozedur [sys.sp_rda_set_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md) aus, und geben Sie eine größere Zahl als 8 Stunden an. Bedenken Sie bei der Entscheidung, wie viele Daten beibehalten werden sollen, die folgenden Faktoren:
-   Die Häufigkeit der automatischen Azure-Sicherungen (mindestens alle 8 Stunden)
-   Die erforderliche Zeit, um ein Problem zu erkennen und zu entscheiden, ob eine Sicherung wiederhergestellt werden soll
-   Die Dauer des Azure-Wiederherstellungsvorgangs

> [!NOTE]
> Eine Erhöhung der Datenmenge, die Stretch-Datenbank vorübergehend in der Stagingtabelle beibehält, erhöht die Menge des auf dem SQL Server erforderlichen Speicherplatzes.

Führen Sie zum Überprüfen der Stundenzahl, in der Stretch-Datenbank Daten vorübergehend in der Stagingtabelle beibehält, die gespeicherte Prozedur [sys.sp_rda_get_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md)aus.

## <a name="see-also"></a>Siehe auch  
[Restore Stretch-enabled databases (Wiederherstellen von für die Streckung aktivierten Datenbanken)](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)  
 [Verwalten und Problembehandlung von Stretch-Datenbank](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)   
   
  
  

