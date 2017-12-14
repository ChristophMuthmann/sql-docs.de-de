---
title: Wiederherstellen einer Datenbank zu einer Datenbank-Momentaufnahme | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- database snapshots [SQL Server], reverting to
- reverting databases
ms.assetid: 8f74dd31-c9ca-4537-8760-0c7648f0787d
caps.latest.revision: "58"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 6ebcff5d0d885fe580af9ac0b14d81e7b4ad2746
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="revert-a-database-to-a-database-snapshot"></a>Wiederherstellen einer Datenbank zu einer Datenbank-Momentaufnahme
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Wenn Daten in einer Onlinedatenbank beschädigt werden, empfiehlt es sich gelegentlich, die Datenbank aus einer Datenbank-Momentaufnahme eines Zeitpunkts vor der Beschädigung wiederherzustellen, anstatt die Datenbank aus einer Sicherungskopie wiederherzustellen. Durch das Wiederherstellen einer Datenbank kann beispielsweise ein kürzlich zurückliegender, schwerwiegender Benutzerfehler (z. B. eine gelöschte Tabelle) rückgängig gemacht werden. Alle nach Erstellung der Momentaufnahme vorgenommenen Änderungen gehen jedoch verloren.  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Erforderliche Komponenten](#Prerequisites)  
  
     [Sicherheit](#Security)  
  
-   **Wiederherstellen einer Datenbank aus einer Datenbankmomentaufnahme mit:**  [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
 Die Wiederherstellung wird unter folgenden Bedingungen nicht unterstützt:  
  
-   Die Datenbank darf derzeit nur über eine Datenbank-Momentaufnahme verfügen, mit der die Wiederherstellung ausgeführt werden soll.  
  
-   Die Datenbank enthält schreibgeschützte oder komprimierte Dateigruppen.  
  
-   Alle Dateien sind nun offline, waren jedoch beim Erstellen der Momentaufnahme online.  
  
 Beachten Sie folgende Einschränkungen, bevor Sie eine Wiederherstellung aus einer Datenbank-Momentaufnahme ausführen:  
  
-   Die Wiederherstellung bezieht sich nicht auf die Wiederherstellung von Medien. . Eine Datenbank-Momentaufnahme ist eine unvollständige Kopie der Datenbankdateien. Wenn also die Datenbank oder die Datenbank-Momentaufnahme beschädigt wurde, ist die Wiederherstellung aus einer Momentaufnahme wahrscheinlich unmöglich. Zudem ist es eher unwahrscheinlich, dass das Problem durch eine Wiederherstellung im Falle einer Beschädigung behoben wird, selbst wenn eine Wiederherstellung möglich ist. Regelmäßige Sicherungen und Tests des Wiederherstellungsplans sind deshalb für den Schutz einer Datenbank unverzichtbar. Weitere Informationen finden Sie unter [Back Up and Restore of SQL Server Databases](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md).  
  
    > [!NOTE]  
    >  Wenn Sie die Quelldatenbank zu dem Zeitpunkt wiederherstellen müssen, an dem Sie eine Datenbank-Momentaufnahme erstellt haben, nutzen Sie das Modell der vollständigen Wiederherstellung, und implementieren Sie eine Sicherungsrichtlinie, die Ihnen dies ermöglicht.  
  
-   Die ursprüngliche Quelldatenbank wird von der wiederhergestellten Datenbank überschrieben, sodass sämtliche Aktualisierungen der Datenbank seit der Erstellung der Momentaufnahme verloren gehen.  
  
-   Die bisherige Protokolldatei wird bei der Wiederherstellung ebenfalls überschrieben, und das Protokoll wird neu erstellt. Daher ist kein Rollforward der wiederhergestellten Datenbank bis zum Zeitpunkt des Benutzerfehlers möglich. Es empfiehlt sich somit, dass Sie das Protokoll vor dem Wiederherstellen einer Datenbank sichern.  
  
    > [!NOTE]  
    >  Es ist zwar nicht möglich, das ursprüngliche Protokoll wiederherzustellen und damit ein Rollforward der Datenbank auszuführen. Die Angaben in der ursprünglichen Protokolldatei können jedoch beim Rekonstruieren verlorener Daten helfen.  
  
-   Durch Zurückkehren wird die Protokollsicherungskette unterbrochen. Bevor Sie also eine Protokollsicherung der Datenbank anfertigen können, muss daher eine vollständige Datenbank- oder Dateisicherung erfolgen. Wir empfehlen eine vollständige Datenbanksicherung.  
  
-   Während des Zurückkehrens sind sowohl die Momentaufnahme als auch die Quelldatenbank nicht verfügbar. Die Quelldatenbank und die Momentaufnahme sind jeweils gekennzeichnet, dass derzeit eine Wiederherstellung ausgeführt wird. Tritt ein Fehler beim Zurückkehren auf, wird beim Neustart der Datenbank versucht, das Zurückkehren abzuschließen.  
  
-   Die Metadaten einer Datenbank nach dem Zurückkehren entsprechen den Metadaten zum Zeitpunkt der Momentaufnahme.  
  
-   Durch das Wiederherstellen werden alle Volltextkataloge gelöscht.  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
 Stellen Sie sicher, dass die Quelldatenbank und die Datenbank-Momentaufnahme die folgenden Voraussetzungen erfüllen:  
  
-   Vergewissern Sie sich, dass die Datenbank nicht beschädigt wurde.  
  
    > [!NOTE]  
    >  Wenn die Datenbank beschädigt wurde, müssen Sie sie aus einer Sicherungskopie wiederherstellen. Weitere Informationen finden Sie unter [Vollständige Datenbankwiederherstellungen &#40;einfaches Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md) oder [Vollständige Datenbankwiederherstellungen &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md).  
  
-   Ermitteln Sie eine aktuelle Momentaufnahme, die vor Auftreten des Fehlers erstellt wurde. Weitere Informationen finden Sie unter [Anzeigen einer Datenbankmomentaufnahme &#40;SQL Server&#41;](../../relational-databases/databases/view-a-database-snapshot-sql-server.md).  
  
-   Löschen Sie alle anderen Momentaufnahmen, die derzeit für die Datenbank vorhanden sind. Weitere Informationen finden Sie unter [Löschen einer Datenbankmomentaufnahme &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md).  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Alle Benutzer, die über RESTORE DATABASE-Berechtigungen für die Quelldatenbank verfügen, können diese in dem Zustand zum Zeitpunkt der Erstellung der Datenbank-Momentaufnahme wiederherstellen.  
  
##  <a name="TsqlProcedure"></a> So stellen Sie eine Datenbank aus einer Datenbank-Momentaufnahme wieder her (Transact-SQL)  
 **So stellen Sie eine Datenbank aus zu einer Datenbank-Momentaufnahme wieder her**  
  
> [!NOTE]  
>  Ein Beispiel für diese Prozedur finden Sie in [Beispiele (Transact-SQL)](#TsqlExample)an späterer Stelle in diesem Abschnitt.  
  
1.  Ermitteln Sie die Datenbank-Momentaufnahme, aus der Sie die Datenbank wiederherstellen möchten. Sie können die Momentaufnahmen für eine Datenbank in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] anzeigen (weitere Informationen finden Sie unter [Anzeigen einer Datenbankmomentaufnahme &#40;SQL Server&#41;](../../relational-databases/databases/view-a-database-snapshot-sql-server.md)). Zudem können Sie die Quelldatenbank einer Sicht anhand der **source_database_id** -Spalte der [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) -Katalogsicht identifizieren.  
  
2.  Löschen Sie alle anderen Datenbankmomentaufnahmen.  
  
     Informationen zum Löschen von Momentaufnahmen finden Sie unter [Löschen einer Datenbankmomentaufnahme &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md). Verwendet die Datenbank das vollständige Wiederherstellungsmodell sollten Sie das Protokoll vor dem Wiederherstellen sichern. Weitere Informationen finden Sie unter [Sichern eines Transaktionsprotokolls &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md) oder [Sichern des Transaktionsprotokolls bei beschädigter Datenbank &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md).  
  
3.  Führen Sie den Wiederherstellungsvorgang aus.  
  
     Für einen Wiederherstellungsvorgang sind RESTORE DATABASE-Berechtigungen für die Quelldatenbank erforderlich. Verwenden Sie zum Wiederherstellen der Datenbank die folgende Transact-SQL-Anweisung:  
  
     RESTORE DATABASE *database_name* FROM DATABASE_SNAPSHOT **=***database_snapshot_name*  
  
     Dabei ist *database_name* die Quelldatenbank und *database_snapshot_name* der Name der Momentaufnahmen, aus dem die Datenbank wiederhergestellt werden soll. Beachten Sie, dass Sie in dieser Anweisung einen Momentaufnahmenamen statt eines Sicherungsmediums angeben müssen.  
  
     Weitere Informationen finden Sie unter [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md).  
  
    > [!NOTE]  
    >  Während des Wiederherstellungsvorgangs stehen weder die Momentaufnahme noch die Quelldatenbank zur Verfügung. Die Quelldatenbank und die Momentaufnahme sind als von einem Wiederherstellungsvorgang betroffen gekennzeichnet. Falls während der Wiederherstellung ein Fehler auftritt, wird beim nächsten Start der Datenbank versucht, die Wiederherstellung abzuschließen.  
  
4.  Hat sich seit der Erstellung der Datenbankmomentaufnahme der Datenbankbesitzer geändert, ist es möglicherweise sinnvoll, den Datenbankbesitzer der wiederhergestellten Datenbank zu aktualisieren.  
  
    > [!NOTE]  
    >  In der wiederhergestellten Datenbank bleiben die Berechtigungen und die Konfiguration (wie z. B. Datenbankbesitzer und Wiederherstellungsmodell) der Datenbankmomentaufnahme erhalten.  
  
5.  Starten Sie die Datenbank.  
  
6.  Sie haben die Option, die wiederhergestellte Datenbank zu sichern; dies empfiehlt sich besonders, wenn das vollständige (oder das massenprotokollierte) Wiederherstellungsmodell für die Datenbank verwendet wird. Weitere Informationen zum Sichern einer Datenbank finden Sie unter [Erstellen einer vollständigen Datenbanksicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md).  
  
###  <a name="TsqlExample"></a> Beispiele (Transact-SQL)  
 Dieser Abschnitt enthält die folgenden Beispiele für das Wiederherstellen einer Datenbank aus einer Datenbank-Momentaufnahme:  
  
-   A. [Wiederherstellen einer Momentaufnahme für die AdventureWorks-Datenbank](#Reverting_AW)  
  
-   B. [Wiederherstellen einer Momentaufnahme für die Sales-Datenbank](#Reverting_Sales)  
  
####  <a name="Reverting_AW"></a> A. Wiederherstellen einer Momentaufnahme für die AdventureWorks-Datenbank  
 In diesem Beispiel wird davon ausgegangen, dass derzeit in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank nur eine Momentaufnahme vorhanden ist. Das Beispiel, mit dem die Momentaufnahme erstellt wird, zu dem die Datenbank hier wiederhergestellt wird, finden Sie unter [Erstellen einer Datenbankmomentaufnahme &#40;Transact-SQL&#41;](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md).  
  
```  
USE master;  
-- Reverting AdventureWorks to AdventureWorks_dbss1800  
RESTORE DATABASE AdventureWorks from   
DATABASE_SNAPSHOT = 'AdventureWorks_dbss1800';  
GO  
```  
  
####  <a name="Reverting_Sales"></a> B. Wiederherstellen einer Momentaufnahme für die Sales-Datenbank  
 In diesem Beispiel wird davon ausgegangen, dass derzeit zwei Momentaufnahmen für die **Sales** -Datenbank vorhanden sind: **sales_snapshot0600** und **sales_snapshot1200**. Durch dieses Beispiel wird die ältere Momentaufnahme gelöscht und die Datenbank mithilfe der aktuelleren Momentaufnahme wiederhergestellt.  
  
 Den Code zum Erstellen der Beispieldatenbank und der Momentaufnahmen, für die dieses Beispiel gilt, finden Sie wie folgt:  
  
-   Informationen zur **Sales**-Datenbank und zur **sales_snapshot0600**-Momentaufnahme finden Sie in „Erstellen einer Datenbank mit Dateigruppen“ und „Erstellen einer Datenbankmomentaufnahme“ in [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md).  
  
-   Informationen zur **sales_snapshot1200** -Momentaufnahme finden Sie unter „Erstellen einer Momentaufnahme für die Sales-Datenbank“ in [Erstellen einer Datenbankmomentaufnahme &#40;Transact-SQL&#41;](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md).  
  
```  
--Test to see if sales_snapshot0600 exists and if it   
-- does, delete it.  
IF EXISTS (SELECT dbid FROM sys.databases  
    WHERE NAME='sales_snapshot0600')  
    DROP DATABASE SalesSnapshot0600;  
GO  
-- Reverting Sales to sales_snapshot1200  
USE master;  
RESTORE DATABASE Sales FROM DATABASE_SNAPSHOT = 'sales_snapshot1200';  
GO  
```  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
-   [Erstellen einer Datenbankmomentaufnahme &#40;Transact-SQL&#41;](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md)  
  
-   [Anzeigen einer Datenbankmomentaufnahme &#40;SQL Server&#41;](../../relational-databases/databases/view-a-database-snapshot-sql-server.md)  
  
-   [Löschen einer Datenbankmomentaufnahme &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankmomentaufnahmen &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [Datenbankspiegelung und Datenbankmomentaufnahmen &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-database-snapshots-sql-server.md)  
  
  
