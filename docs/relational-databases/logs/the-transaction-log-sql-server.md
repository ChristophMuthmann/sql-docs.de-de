---
title: Das Transaktionsprotokoll (SQL Server) | Microsoft-Dokumentation
ms.custom: 
ms.date: 02/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-transaction-log
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transaction logs [SQL Server], about
- databases [SQL Server], transaction logs
- logs [SQL Server], transaction logs
ms.assetid: d7be5ac5-4c8e-4d0a-b114-939eb97dac4d
caps.latest.revision: 65
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d23b661d9fd99090a5140100513886d8351460b9
ms.lasthandoff: 04/11/2017

---
# <a name="the-transaction-log-sql-server"></a>Das Transaktionsprotokoll [SQL Server]
  Jede SQL Server-Datenbank verfügt über ein Transaktionsprotokoll, in dem alle Transaktionen sowie die Datenbankänderungen aufgezeichnet werden, die von den einzelnen Transaktionen vorgenommen werden.
  
Das Transaktionsprotokoll ist eine wichtige Komponente der Datenbank. Wenn ein Systemfehler auftritt, benötigen Sie dieses Protokoll, um Ihre Datenbank wieder in einen konsistenten Zustand zu versetzen. Dieses Protokoll sollten Sie nicht löschen oder verschieben, wenn Sie sich über die Auswirkungen dieses Vorgangs nicht vollständig im Klaren sind. 

  
 > **Zusatzinformationen** Einige bekannte gute Ausgangspunkte für das Anwenden von Transaktionsprotokollen während der Datenbankwiederherstellung werden durch Prüfpunkte vorgegeben. Weitere Informationen finden Sie unter [Datenbankprüfpunkte (SQL Server)](../../relational-databases/logs/database-checkpoints-sql-server.md).  
  
## <a name="operations-supported-by-the-transaction-log"></a>Vom Transaktionsprotokoll unterstützte Operationen  
 Das Transaktionsprotokoll unterstützt die folgenden Vorgänge:  
  
-   Wiederherstellen einzelner Transaktionen.  
  
-   Wiederherstellen aller unvollständigen Transaktionen, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gestartet wird.  
  
-   Ausführen eines Rollforwards für eine wiederhergestellte Datenbank, Datei, Dateigruppe oder Seite bis zu dem Punkt, an dem der Fehler aufgetreten ist.  
  
-   Unterstützen der Transaktionsreplikation.  
  
-   Lösungen zur Unterstützung von hoher Verfügbarkeit und Notfallwiederherstellung: [!INCLUDE[ssHADR](../../includes/sshadr-md.md)], Datenbankspiegelung und Protokollversand.

## <a name="individual-transaction-recovery"></a>Wiederherstellen einzelner Transaktionen
Wenn eine Anwendung eine ROLLBACK-Anweisung ausgibt oder wenn das Datenbankmodul einen Fehler erkennt, z. B. die unterbrochene Verbindung mit einem Client, werden die Protokolldatensätze verwendet, um für die Änderungen, die von unvollständigen Transaktionen vorgenommen wurden, einen Rollback auszuführen. 

## <a name="recovery-of-all-incomplete-transactions-when-includessnoversionincludesssnoversion-mdmd-is-started"></a>Wiederherstellen aller unvollständigen Transaktionen, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gestartet wird
Wenn ein Server ausfällt, bleiben die Datenbanken möglicherweise in einem Status, in dem einige Änderungen nicht vom Puffercache in die Datendateien geschrieben wurden, einige Änderungen von unvollständigen Transaktionen jedoch bereits in den Datendateien vorgenommen wurden. Beim Starten einer Instanz von SQL Server wird eine Wiederherstellung aller Datenbanken ausgeführt. Für jede Änderung, die im Protokoll aufgezeichnet wurde und die möglicherweise nicht in die Datendateien geschrieben wurde, wird ein Rollforward ausgeführt. Für jede unvollständige Transaktion, die im Transaktionsprotokoll erkannt wird, wird anschließend ein Rollback ausgeführt, um sicherzustellen, dass die Integrität der Datenbank aufrechterhalten wird. 

## <a name="rolling-a-restored-database-file-filegroup-or-page-forward-to-the-point-of-failure"></a>Ausführen eines Rollforwards für eine wiederhergestellte Datenbank, Datei, Dateigruppe oder Seite bis zu dem Punkt, an dem der Fehler aufgetreten ist
Nach einem Hardwareverlust oder Datenträgerfehler, der sich auf die Datendateien auswirkt, können Sie die Datenbank so wiederherstellen, wie sie zum Zeitpunkt des Ausfalls vorlag. Sie stellen zuerst die letzte vollständige und die letzte differenzielle Datenbanksicherung und anschließend die nachfolgende Folge von Transaktionsprotokollsicherungen bis zu dem Punkt wieder her, an dem der Fehler aufgetreten ist. 

Beim Wiederherstellen der einzelnen Protokollsicherungen übernimmt das Datenbankmodul erneut sämtliche im Protokoll aufgezeichneten Änderungen, um für alle Transaktionen einen Rollforward auszuführen. Sobald die letzte Protokollsicherung wiederhergestellt ist, verwendet das Datenbankmodul die Protokollinformationen, um für sämtliche Transaktionen einen Rollback auszuführen, die zu diesem Zeitpunkt noch nicht abgeschlossen waren. 

## <a name="supporting-transactional-replication"></a>Unterstützen der Transaktionsreplikation
Der Protokolllese-Agent überwacht das Transaktionsprotokoll jeder für die Transaktionsreplikation konfigurierten Datenbank und kopiert die für die Replikation markierten Transaktionen aus dem Transaktionsprotokoll in die Verteilungsdatenbank. Weitere Informationen finden Sie unter [Funktionsweise der Transaktionsreplikation](http://msdn.microsoft.com/library/ms151706.aspx).

## <a name="supporting-high-availability-and-disaster-recovery-solutions"></a>Unterstützen von Hochverfügbarkeits- und Notfallwiederherstellungslösungen
Standbyserverlösungen, AlwaysOn-Verfügbarkeitsgruppen, Datenbankspiegelung und Protokollversand hängen in großem Umfang vom Transaktionsprotokoll ab. 

In einem Szenario mit Always On-Verfügbarkeitsgruppe wird jede Aktualisierung einer Datenbank (das primäre Replikat) sofort in separaten vollständigen Kopien der Datenbank (die sekundären Replikate) reproduziert. Das primäre Replikat sendet jeden Protokolldatensatz sofort an die sekundären Replikate, in denen dieser eingehende Protokolldatensatz auf Verfügbarkeitsgruppen-Datenbanken angewendet wird, wobei der Protokolldatensatz kontinuierlich weitergegeben wird. Weitere Informationen finden Sie unter [Always On-Failoverclusterinstanzen](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md).

In einem Protokollversendungsszenario sendet der primäre Server das aktive Transaktionsprotokoll der primären Datenbank an ein oder mehrere Ziele. Jeder sekundäre Server stellt das Protokoll in seiner lokalen sekundären Datenbank wieder her. Weitere Informationen finden Sie unter [Informationen zum Protokollversand](../../database-engine/log-shipping/about-log-shipping-sql-server.md). 

In einem Datenbankspiegelungsszenario wird jedes Update einer Datenbank (der Prinzipaldatenbank) sofort in einer separaten vollständigen Kopie der Datenbank (der Spiegeldatenbank) reproduziert. Die Prinzipalserverinstanz sendet jeden Protokolldatensatz sofort an die Spiegelserverinstanz, die die eingehenden Protokolldatensätze auf die Spiegeldatenbank anwendet, um kontinuierlich ein Rollforward dafür auszuführen. Weitere Informationen finden Sie unter [Datenbankspiegelung](../../database-engine/database-mirroring/database-mirroring-sql-server.md).
  

##  <a name="Characteristics"></a>Transaction Log characteristics

Merkmale der [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]-Transaktionsprotokolle: 
-  Das Transaktionsprotokoll wird als eine separate oder mehrere Dateien in der Datenbank implementiert. Der Protokollcache wird getrennt vom Puffercache für Datenseiten verwaltet, woraus sich ein einfacher, schneller und zuverlässiger Code innerhalb des Datenbankmoduls ergibt.
-  Das Format der Protokolldatensätze und -seiten muss nicht dem Format von Datenseiten entsprechen.
-  Das Transaktionsprotokoll kann in Form mehrerer Dateien implementiert werden. Für die Dateien kann automatische Vergrößerung durch Festlegen des FILEGROWTH-Werts für das Protokoll definiert werden. Auf diese Weise nimmt die Wahrscheinlichkeit ab, dass im Transaktionsprotokoll kein Speicherplatz mehr verfügbar ist. Zudem wird der Verwaltungsaufwand verringert. Weitere Informationen finden Sie unter [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md).
-  Der Mechanismus zum erneuten Verwenden des freien Speicherplatzes in den Protokolldateien ist schnell und wirkt sich nur minimal auf den Transaktionsdurchsatz aus.

##  <a name="Truncation"></a> Transaction log truncation  
 Durch das Kürzen des Protokolls wird in der Protokolldatei Speicherplatz freigegeben, der vom Transaktionsprotokoll erneut verwendet werden kann. Sie müssen regelmäßig das Transaktionsprotokoll kürzen, damit es nicht den zugewiesenen Speicherplatz füllt (Was es tun wird!!)! Verschiedene Faktoren können die Protokollkürzung verzögern, daher ist die Überwachung der Protokollgröße wichtig. Einige Vorgänge lassen sich minimal protokollieren, um deren Auswirkung auf die Größe des Transaktionsprotokolls zu reduzieren.  
 
  Durch die Protokollkürzung werden inaktive virtuelle Protokolldateien aus dem logischen Transaktionsprotokoll einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank gelöscht. Zudem wird Speicherplatz im logischen Protokoll zur Wiederverwendung durch das physische Transaktionsprotokoll freigegeben. Wird ein Transaktionsprotokoll nicht gekürzt, füllt sich dadurch der gesamte Speicherplatz des Datenträgers auf, der den zugehörigen physischen Protokolldateien zugeordnet ist.  
  
 Um zu vermeiden, dass nur noch wenig Speicherplatz vorhanden ist, erfolgt die Kürzung automatisch nach den folgenden Ereignissen, sofern die Protokollkürzung nicht aus bestimmten Gründen verzögert wird:  
  
-   Unter dem einfachen Wiederherstellungsmodell, nach einem Prüfpunkt.  
  
-   Unter dem vollständigen oder massenprotokollierten Wiederherstellungsmodell, wenn ein Prüfpunkt seit der vorherigen Sicherung ausgelöst wurde, erfolgt die Kürzung nach einer Protokollsicherung (sofern es sich nicht um eine Kopiesicherung handelt).  
  
 Weitere Informationen finden Sie unter [Faktoren, die die Protokollkürzung verzögern können](#FactorsThatDelayTruncation)weiter unten in diesem Thema.  
  
> **HINWEIS!** Die Protokollkürzung verringert nicht die Größe einer physischen Protokolldatei. Sie müssen zum Reduzieren der physischen Größe einer physischen Protokolldatei die Protokolldatei verkleinern. Informationen zum Verkleinern der Größe der physischen Protokolldatei finden Sie unter [Manage the Size of the Transaction Log File](../../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md).  
  
##  <a name="FactorsThatDelayTruncation"></a> Factors that can delay log truncation  
 Bleiben Protokolldatensätze lange aktiv, verzögert sich die Transaktionsprotokollkürzung. Dabei kann sich das Transaktionsprotokoll auffüllen, wie bereits oben erwähnt wurde.  
  
> **WICHTIG!** Informationen zum Umgang mit einem voll aufgefüllten Transaktionsprotokoll finden Sie unter [Troubleshoot a Full Transaction Log &#40;SQL Server Error 9002&#41;](../../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md).  
  
 Die Protokollkürzung kann tatsächlich aus verschiedenen Gründen verzögert werden. Sie können ermitteln, wodurch die Protokollkürzung verhindert wird, indem Sie die Spalten **log_reuse_wait** und **log_reuse_wait_desc** der Katalogsicht [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) abfragen. In der folgenden Tabelle werden die Werte dieser Spalten beschrieben.  
  
|log_reuse_wait value|log_reuse_wait_desc value|Beschreibung|  
|----------------------------|----------------------------------|-----------------|  
|0|NOTHING|Derzeit ist mindestens eine wiederverwendbare virtuelle Protokolldatei vorhanden.|  
|1|CHECKPOINT|Seit der letzten Protokollkürzung ist kein Prüfpunkt aufgetreten, oder der Kopf des Protokolls wurde noch nicht über eine virtuelle Protokolldatei hinaus verschoben. (Alle Wiederherstellungsmodelle)<br /><br /> Dies ist ein häufiger Grund für das verzögerte Kürzen von Protokollen. Weitere Informationen finden Sie unter [Database Checkpoints &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md).|  
|2|LOG_BACKUP|Eine Protokollsicherung ist erforderlich, bevor das Transaktionsprotokoll gekürzt werden kann. (nur vollständiges bzw. massenprotokolliertes Wiederherstellungsmodell)<br /><br /> Bei Abschluss der nächsten Protokollsicherung wird möglicherweise ein Teil des Protokollspeicherplatzes zur Wiederverwendung freigegeben.|  
|3|ACTIVE_BACKUP_OR_RESTORE|Es findet gerade eine Datensicherung oder eine Wiederherstellung statt (alle Wiederherstellungsmodelle).<br /><br /> Verhindert eine Datensicherung die Protokollkürzung, kann das unmittelbare Problem u. U. durch Abbrechen des Sicherungsvorgangs behoben werden.|  
|4|ACTIVE_TRANSACTION|Eine Transaktion ist aktiv (alle Wiederherstellungsmodelle):<br /><br /> Möglicherweise ist beim Starten der Protokollsicherung eine Transaktion mit langer Ausführungszeit vorhanden. In diesem Fall ist zum Freigeben von Speicherplatz möglicherweise eine weitere Protokollsicherung erforderlich. Hinweis: Transaktionen mit langer Laufzeit verhindern die Protokollkürzung unter allen Wiederherstellungsmodellen, einschließlich des einfachen Wiederherstellungsmodells, unter dem im Allgemeinen das Transaktionsprotokoll an jedem automatischen Prüfpunkt gekürzt wird.<br /><br /> Eine Transaktion wird verzögert. Eine *verzögerte Transaktion* ist tatsächlich eine aktive Transaktion, deren Rollback aufgrund einer nicht verfügbaren Ressource blockiert ist. Weitere Informationen zu den Ursachen für verzögerte Transaktionen und zum Auflösen ihres verzögerten Zustands finden Sie unter [Verzögerte Transaktionen &#40;SQL Server&#41;](../../relational-databases/backup-restore/deferred-transactions-sql-server.md).<br /> <br /> Lang andauernde Transaktionen können auch das Transaktionsprotokoll von „tempdb“ füllen. „tempdb“ wird implizit von Benutzertransaktionen für interne Objekte wie z.B. Arbeitstabellen zum Sortieren, Arbeitsdateien für Hashverfahren, Cursorarbeitstabellen und Zeilenversionsverwaltung verwendet. Selbst wenn die Benutzertransaktion nur das Lesen von Daten umfasst (`SELECT`-Abfragen), werden möglicherweise interne Objekte erstellt und unter Benutzertransaktionen verwendet. Anschließend kann das tempdb-Transaktionsprotokoll gefüllt werden.|  
|5|DATABASE_MIRRORING|Die Datenbankspiegelung wurde angehalten, oder im Modus für hohe Leistung befindet sich die Spiegeldatenbank deutlich hinter der Prinzipaldatenbank. (nur vollständiges Wiederherstellungsmodell)<br /><br /> Weitere Informationen finden Sie unter [Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).|  
|6|REPLICATION|Während der Transaktionsreplikationen wurden für die Veröffentlichungen relevante Transaktionen noch immer nicht für die Verteilungsdatenbank bereitgestellt. (nur vollständiges Wiederherstellungsmodell)<br /><br /> Weitere Informationen zur Transaktionsreplikation finden Sie unter [SQL Server Replication](../../relational-databases/replication/sql-server-replication.md).|  
|7|DATABASE_SNAPSHOT_CREATION|Eine Datenbank-Momentaufnahme wird erstellt. (Alle Wiederherstellungsmodelle)<br /><br /> Dies ist ein häufiger, im Allgemeinen jedoch nur kurz andauernder Grund für ein verzögertes Kürzen eines Protokolls.|  
|8|LOG_SCAN|Ein Protokollscan wird ausgelöst. (Alle Wiederherstellungsmodelle)<br /><br /> Dies ist ein häufiger, im Allgemeinen jedoch nur kurz andauernder Grund für ein verzögertes Kürzen eines Protokolls.|  
|9|AVAILABILITY_REPLICA|Ein sekundäres Replikat einer Verfügbarkeitsgruppe wendet Transaktionsprotokoll-Datensätze dieser Datenbank auf eine zugehörige sekundäre Datenbank an. (vollständiges Wiederherstellungsmodell)<br /><br /> Weitere Informationen finden Sie unter [Übersicht über Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).|  
|10|—|Nur interne Verwendung|  
|11|—|Nur interne Verwendung|  
|12|—|Nur interne Verwendung|  
|13|OLDEST_PAGE|Ist eine Datenbank zur Verwendung von indirekten Prüfpunkten konfiguriert, ist die älteste Seite in der Datenbank u. U. älter als die Prüfpunkt-LSN. In diesem Fall kann die älteste Seite die Protokollkürzung verzögern. (Alle Wiederherstellungsmodelle)<br /><br /> Weitere Informationen zu indirekten Prüfpunkten finden Sie unter [Database Checkpoints &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md).|  
|14|OTHER_TRANSIENT|Dieser Wert wird derzeit nicht verwendet.|  
  
##  <a name="MinimallyLogged"></a> Operations that can be minimally logged  
 Bei der*minimalen Protokollierung* werden nur die Informationen protokolliert, die zum Wiederherstellen der Transaktion ohne Unterstützung der Zeitpunktwiederherstellung erforderlich sind. In diesem Thema werden die Vorgänge aufgeführt, die unter dem massenprotokollierten [Wiederherstellungsmodell](https://msdn.microsoft.com/library/ms189275.aspx) minimal protokolliert werden (sowie unter dem einfachen Wiederherstellungsmodell, es sei denn, es wird eine Sicherung ausgeführt).  
  
> **HINWEIS!** Die minimale Protokollierung wird für speicheroptimierte Tabellen nicht unterstützt.  
  
> **WEITERER HINWEIS!** Unter dem vollständigen [Wiederherstellungsmodell](https://msdn.microsoft.com/library/ms189275.aspx)werden alle Massenvorgänge vollständig protokolliert. Sie können die Protokollierung für eine Reihe von Massenvorgängen jedoch verringern, indem Sie die Datenbank bei Massenvorgängen vorübergehend in das massenprotokollierte Wiederherstellungsmodell schalten. Die minimale Protokollierung ist effizienter als die vollständige Protokollierung und senkt die Wahrscheinlichkeit, dass ein umfangreicher Massenvorgang den verfügbaren Transaktionsprotokoll-Speicherplatz während einer Massentransaktion auffüllt. Wenn die Datenbank bei Aktivierung der minimalen Protokollierung jedoch beschädigt wird oder verloren geht, können Sie die Datenbank nicht bis zu dem Punkt wiederherstellen, an dem der Fehler aufgetreten ist.  
  
 Die folgenden Vorgänge, die unter dem vollständigen Wiederherstellungsmodell vollständig protokolliert werden, werden unter dem einfachen und massenprotokollierten Wiederherstellungsmodell minimal protokolliert:  
  
-   Massenimportvorgänge ([bcp](../../tools/bcp-utility.md), [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) und [INSERT... SELECT](../../t-sql/statements/insert-transact-sql.md)). Weitere Informationen zur minimalen Protokollierung eines Massenimports in eine Tabelle finden Sie unter [Prerequisites for Minimal Logging in Bulk Import](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md).  
  
Wenn die Transaktionsreplikation aktiviert ist, werden BULK INSERT-Vorgänge auch unter dem massenprotokollierten Wiederherstellungsmodell vollständig protokolliert.  
  
-   SELECT [INTO](../../t-sql/queries/select-into-clause-transact-sql.md) -Vorgänge.  
  
Wenn die Transaktionsreplikation aktiviert ist, werden SELECT INTO-Vorgänge auch unter dem massenprotokollierten Wiederherstellungsmodell vollständig protokolliert.  
  
-   Teilupdates von Datentypen für hohe Werte mithilfe der .WRITE-Klausel in der [UPDATE](../../t-sql/queries/update-transact-sql.md) -Anweisung beim Einfügen oder Anfügen neuer Daten. Beachten Sie, dass die minimale Protokollierung nicht verwendet wird, wenn vorhandene Werte aktualisiert werden. Weitere Informationen zu Datentypen für hohe Werte finden Sie unter [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md).  
  
-   [WRITETEXT](../../t-sql/queries/writetext-transact-sql.md) -Anweisung und [UPDATETEXT](../../t-sql/queries/updatetext-transact-sql.md) -Anweisung beim Einfügen oder Anfügen neuer Daten an die Datentypspalten **text**, **ntext**und **image** . Beachten Sie, dass die minimale Protokollierung nicht verwendet wird, wenn vorhandene Werte aktualisiert werden.  
  
    >  Die WRITETEXT- und die UPDATETEXT-Anweisung sind **veraltet**, sollten also in neuen Anwendungen nicht mehr verwendet werden.  
  
-   Wenn für die Datenbank das einfache oder massenprotokollierte Wiederherstellungsmodell festgelegt ist, werden einige Index-DDL-Vorgänge minimal protokolliert, unabhängig davon, ob der Vorgang offline oder online ausgeführt wird. Die minimal protokollierten Indexvorgänge sind nachfolgend aufgeführt:  
  
    -   [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md) -Vorgänge (einschließlich indizierter Sichten).  
  
    -   [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) REBUILD- oder DBCC DBREINDEX-Vorgänge.  
  
        > Die **DBCC DBREINDEX-Anweisung** ist **veraltet**, sollte also in neuen Anwendungen nicht verwendet werden.  
  
    -   Neuerstellungen neuer Heaps mit DROP INDEX (falls zutreffend). (Aufhebungen von Indexseitenzuordnungen während eines [DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md) -Vorgangs werden **immer** vollständig protokolliert.)
  
##  <a name="RelatedTasks"></a> Related tasks  
 **Verwalten des Transaktionsprotokolls**  
  
-   [Verwalten der Größe der Transaktionsprotokolldatei](../../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md)  
  
-   [Problembehandlung bei vollen Transaktionsprotokollen &#40;SQL Server-Fehler 9002&#41;](../../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
 **Sichern des Transaktionsprotokolls (vollständiges Wiederherstellungsmodell)**  
  
-   [Sichern eines Transaktionsprotokolls &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
 **Wiederherstellen des Transaktionsprotokolls (vollständiges Wiederherstellungsmodell)**  
  
-   [Wiederherstellen einer Transaktionsprotokollsicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
## <a name="more-information"></a>Weitere Informationen.  
  [Handbuch zur Architektur und Verwaltung von Transaktionsprotokollen in SQL Server](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md)   
 [Steuern der Transaktionsdauerhaftigkeit](../../relational-databases/logs/control-transaction-durability.md)   
 [Voraussetzungen für die minimale Protokollierung beim Massenimport](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md)   
 [Sichern und Wiederherstellen von SQL Server-Datenbanken](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Datenbankprüfpunkte &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md)   
 [Anzeigen oder Ändern der Eigenschaften einer Datenbank](../../relational-databases/databases/view-or-change-the-properties-of-a-database.md)   
 [Wiederherstellungsmodelle &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)  
  
  

