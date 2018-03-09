---
title: Schrittweise Wiederherstellungen [SQL Server] | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- partial updates [SQL Server]
- staged restores [SQL Server]
- piecemeal restores [SQL Server]
- restoring [SQL Server], piecemeal restore scenario
ms.assetid: 208f55e0-0762-4cfb-85c4-d36a76ea0f5b
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 82b43b985c462d5748079a8e9b6eea84a7fe2a53
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="piecemeal-restores-sql-server"></a>Schrittweise Wiederherstellungen [SQL Server]
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Dieses Thema ist nur für Datenbanken in der Enterprise Edition von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] relevant, die mehrere Dateien oder Dateigruppen enthalten, und unter dem einfachen Modell nur für schreibgeschützte Dateigruppen.  
  
 Weitere Informationen zur schrittweisen Wiederherstellung und speicheroptimierten Tabellen finden Sie unter [Schrittweise Wiederherstellung von Datenbanken mit speicheroptimierten Tabellen](../../relational-databases/in-memory-oltp/piecemeal-restore-of-databases-with-memory-optimized-tables.md).  
  
 *Schritt-für-Schritt-Wiederherstellung* : Ermöglicht die Wiederherstellung von Datenbanken mit mehreren Dateigruppen in einzelnen Phasen. Die schrittweise Wiederherstellung umfasst eine Reihe von Wiederherstellungssequenzen, wobei mit der primären Dateigruppe und in einigen Fällen mit einer oder mehreren sekundären Dateigruppen begonnen wird. Bei der schrittweisen Wiederherstellung finden Überprüfungen statt, um sicherzustellen, dass die Datenbank am Ende konsistent ist. Nach Abschluss der Wiederherstellungssequenz können wiederhergestellte Dateien sofort online geschaltet werden, sofern diese Dateien gültig und mit der Datenbank konsistent sind.  
  
 Die schrittweise Wiederherstellung ist für sämtliche Wiederherstellungsmodelle möglich, zeichnet sich jedoch durch höhere Flexibilität in Bezug auf die vollständigen und massenprotokollierten Modelle als in Bezug auf das einfache Modell aus.  
  
 Jede schrittweise Wiederherstellung beginnt mit einer anfänglichen Wiederherstellungssequenz, die als *Teilwiederherstellungssequenz*bezeichnet wird. Mit der Teilwiederherstellungssequenz wird mindestens die primäre Dateigruppe wiederhergestellt und beim einfachen Wiederherstellungsmodell alle Dateigruppen mit Lese-/Schreibzugriff. Während der schrittweisen Wiederherstellungssequenz muss die gesamte Datenbank offline geschaltet werden. Danach ist die Datenbank online, und die wiederhergestellten Dateigruppen sind verfügbar. Alle nicht wiederhergestellten Dateigruppen bleiben jedoch offline, und es ist kein Zugriff möglich. Alle Offlinedateigruppen können jedoch später durch eine Dateiwiederherstellung wiederhergestellt und online geschaltet werden.  
  
 Unabhängig davon, welches Wiederherstellungsmodell von der Datenbank verwendet wird, beginnt die Teilwiederherstellungssequenz mit einer RESTORE DATABASE-Anweisung, mit der eine vollständige Sicherung wiederhergestellt und die PARTIAL-Option angegeben wird. Mit der Option PARTIAL wird stets eine neue schrittweise Wiederherstellung gestartet. Deshalb müssen Sie PARTIAL nur einmal in der Anfangsanweisung der Teilwiederherstellungssequenz angeben. Wenn die Teilwiederherstellungssequenz abgeschlossen und die Datenbank online geschaltet wird, wird den übrigen Dateien der Status "Wiederherstellung ausstehend" zugewiesen, da ihre Wiederherstellung verschoben wurde.  
  
 Anschließend schließt eine schrittweise Wiederherstellung normalerweise eine oder mehrere Wiederherstellungssequenzen ein, die als *Dateigruppen-Wiederherstellungssequenzen*bezeichnet werden. Sie können mit der Ausführung einer bestimmten Dateigruppen-Wiederherstellungssequenz so lange warten, wie Sie möchten. Mit jeder Dateigruppenwiederherstellungssequenz wird mindestens eine Offlinedateigruppe bis zu einem mit der Datenbank konsistenten Zeitpunkt wiederhergestellt. Zeitpunkt und Anzahl der Dateigruppen-Wiederherstellungssequenzen richten sich nach Ihrem Wiederherstellungsziel, nach der Anzahl der wiederherzustellenden Offlinedateigruppen und danach, wie viele Sie davon pro Dateigruppen-Wiederherstellungssequenz wiederherstellen.  
  
 Die genauen Anforderungen zum Ausführen einer schrittweisen Wiederherstellung richten sich nach dem Wiederherstellungsmodell der Datenbank. Weitere Informationen finden Sie unter "Schrittweise Wiederherstellung mit dem einfachen Wiederherstellungsmodell" und "Schrittweise Wiederherstellung mit dem vollständigen Wiederherstellungsmodell" weiter unten in diesem Thema.  
  
## <a name="piecemeal-restore-scenarios"></a>Szenarien für die schrittweise Wiederherstellung  
 Alle Editionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützen schrittweise Offlinewiederherstellungen. In der Enterprise Edition kann eine schrittweise Wiederherstellung entweder online oder offline erfolgen. Die Folgen der schrittweisen Offline- und der schrittweisen Onlinewiederherstellung werden anhand der folgenden Szenarien deutlich:  
  
-   Szenario für schrittweise Offlinewiederherstellung  
  
     Bei einer schrittweisen Offlinewiederherstellung ist die Datenbank nach der Teilwiederherstellungssequenz offline. Dateigruppen, die noch nicht wiederhergestellt wurden, bleiben offline. Sie können jedoch nach Bedarf wiederhergestellt werden, nachdem die Datenbank offline geschaltet wurde.  
  
-   Szenario für schrittweise Onlinewiederherstellung  
  
     Bei einer schrittweisen Onlinewiederherstellung ist die Datenbank nach der Teilwiederherstellungssequenz online, und die primäre Dateigruppe und wiederhergestellte sekundäre Dateigruppen sind verfügbar. Dateigruppen, die noch nicht wiederhergestellt wurden, bleiben offline. Sie können jedoch bei Bedarf wiederhergestellt werden, während die Datenbank online bleibt.  
  
     Schrittweise Onlinewiederherstellungen können zurückgestellte Transaktionen umfassen. Wenn nur eine Teilmenge von Dateigruppen wiederhergestellt wurde, können Transaktionen in der Datenbank, die von Onlinedateigruppen abhängig sind, eventuell zurückgestellt werden. Dies entspricht den Erwartungen, da die gesamte Datenbank konsistent sein muss. Weitere Informationen finden Sie unter [Markierte Transaktionen &#40;SQL Server&#41;](../../relational-databases/backup-restore/deferred-transactions-sql-server.md)entfernt werden.  
  
-   [!INCLUDE[hek_1](../../includes/hek-1-md.md)] Szenario für die schrittweise Wiederherstellung  
  
     Weitere Informationen zur schrittweisen Wiederherstellung von In-Memory OLTP-Datenbanken finden Sie unter [Schrittweise Sicherung und Wiederherstellung von Datenbanken mit speicheroptimierten Tabellen](../../relational-databases/in-memory-oltp/piecemeal-restore-of-databases-with-memory-optimized-tables.md).  
  
## <a name="restrictions"></a>Restrictions  
 Wenn in einer Teilwiederherstellungssequenz eine [FILESTREAM](../../relational-databases/blob/filestream-sql-server.md) -Dateigruppe ausgeschlossen wird, wird die Wiederherstellung bis zu einem bestimmten Zeitpunkt nicht unterstützt. Sie können das Fortsetzen der Wiederherstellungssequenz erzwingen. Die FILESTREAM-Dateigruppen, die nicht in die RESTORE-Anweisung eingeschlossen werden, können jedoch zu keinem Zeitpunkt wiederhergestellt werden. Wenn Sie eine Wiederherstellung bis zu einem bestimmten Zeitpunkt erzwingen möchten, geben Sie die CONTINUE_AFTER_ERROR-Option zusammen mit der Option STOPAT, STOPATMARK oder STOPBEFOREMARK an. Diese müssen Sie auch in den folgenden RESTORE LOG-Anweisungen angeben. Wenn Sie CONTINUE_AFTER_ERROR angeben, ist die Teilwiederherstellungssequenz erfolgreich, und die FILESTREAM-Dateigruppe wird nicht mehr wiederherstellbar.  
  
## <a name="piecemeal-restore-under-the-simple-recovery-model"></a>Schrittweise Wiederherstellung mit dem einfachen Wiederherstellungsmodell  
 Beim einfachen Wiederherstellungsmodell muss die schrittweise Wiederherstellungssequenz mit einer vollständigen Datenbanksicherung oder mit einer Teilsicherung beginnen. Dann wird als Nächstes die letzte differenzielle Sicherung wiederhergestellt, wenn es sich bei der wiederhergestellten Sicherung um eine differenzielle Basis handelt.  
  
 Wenn Sie während der ersten Teilwiederherstellungssequenz nur eine Teilmenge von Dateigruppen mit Lese-/Schreibzugriff wiederherstellen, werden alle nicht wiederhergestellten Dateigruppen mit der Wiederherstellung der teilweise wiederhergestellten Datenbank als veraltet markiert (defunct-Status). Das Auslassen einer Dateigruppe mit Lese-/Schreibzugriff aus der Teilwiederherstellungssequenz empfiehlt sich nur in folgenden Fällen:  
  
-   Wenn Sie die nicht wiederhergestellten Dateigruppen außer Kraft setzen möchten.  
  
-   Die Wiederherstellungssequenz erreicht einen Wiederherstellungspunkt, ab dem alle nicht wiederhergestellten Dateigruppen schreibgeschützt, gelöscht oder veraltet sind (infolge einer zuvor ausgeführten Wiederherstellungssequenz der schrittweisen Wiederherstellung).  
  
-   Die vollständige Sicherung wurde ausgeführt, während die Datenbank das einfache Wiederherstellungsmodell verwendet hat, der Wiederherstellungspunkt jedoch an einem Zeitpunkt liegt, an dem die Datenbank das vollständige Wiederherstellungsmodell verwendet. Weitere Informationen finden Sie unter "Ausführen einer schrittweisen Wiederherstellung einer Datenbank, deren Wiederherstellungsmodell von einfach in vollständig geändert wurde" weiter unten in diesem Thema.  
  
### <a name="requirements-for-piecemeal-restore-under-the-simple-recovery-model"></a>Anforderungen bei der schrittweisen Wiederherstellung mit dem einfachen Wiederherstellungsmodell  
 Beim einfachen Wiederherstellungsmodell werden in der Anfangsphase die primäre Dateigruppe und alle sekundären Dateigruppen mit Lese-/Schreibzugriff wiederhergestellt. Nach Abschluss der Anfangsphase können wiederhergestellte Dateien sofort online geschaltet werden, sofern diese Dateien gültig und mit der Datenbank konsistent sind.  
  
 Anschließend können schreibgeschützte Dateigruppen in einer oder mehreren zusätzlichen Phasen wiederhergestellt werden.  
  
 Die schrittweise Wiederherstellung für eine schreibgeschützte sekundäre Dateigruppe ist nur dann verfügbar, wenn folgende Aussagen zutreffen:  
  
-   Sie war zum Zeitpunkt der Sicherung schreibgeschützt.  
  
-   Sie ist schreibgeschützt geblieben (wodurch sie logisch konsistent mit der primären Dateigruppe bleibt).  
  
 Beim Ausführen einer schrittweisen Wiederherstellung müssen die folgenden Richtlinien befolgt werden:  
  
-   Ein vollständiger Sicherungssatz für die schrittweise Wiederherstellung einer Datenbank des einfachen Wiederherstellungsmodells muss Folgendes enthalten:  
  
    -   Eine Teilsicherung oder eine vollständige Datenbanksicherung, die neben der primären Dateigruppe auch sämtliche Dateigruppen enthält, die zum Zeitpunkt der Sicherung über Lese-/Schreibzugriff verfügten.  
  
    -   Eine Sicherung der einzelnen schreibgeschützten Dateien.  
  
-   Damit die Sicherung einer schreibgeschützten Datei mit der primären Dateigruppe konsistent ist, muss die sekundäre Dateigruppe ab dem Zeitpunkt der Sicherung bis zum Abschluss der Sicherung der primären Dateigruppe schreibgeschützt sein. Sie können differenzielle Dateisicherungen verwenden, sofern sie vorgenommen wurden, nachdem der Schreibschutz für die Dateigruppe festgelegt wurde.  
  
### <a name="piecemeal-restore-stages-simple-recovery-model"></a>Phasen der schrittweisen Wiederherstellung (einfaches Wiederherstellungsmodell)  
 Das Szenario der schrittweisen Wiederherstellung umfasst folgende Phasen:  
  
-   Anfangsphase (Wiederherstellung der primären Dateigruppe und aller Dateigruppen mit Lese-/Schreibzugriff)  
  
     In der Anfangsphase wird eine Teilwiederherstellung ausgeführt. Durch die Teilwiederherstellungssequenz werden die primäre Dateigruppe, alle sekundären Dateigruppen mit Lese-/Schreibzugriff und (optional) einige schreibgeschützte Dateigruppen wiederhergestellt. Während der Anfangsphase muss die gesamte Datenbank offline geschaltet werden. Nach der Anfangsphase befindet sich die Datenbank im Onlinezustand, und die wiederhergestellten Dateigruppen sind verfügbar. Schreibgeschützte Dateigruppen, die noch nicht wiederhergestellt wurden, bleiben jedoch offline.  
  
     Die erste RESTORE-Anweisung in der Anfangsphase muss folgende Voraussetzungen erfüllen:  
  
    -   Verwenden einer Teilsicherung oder einer vollständigen Datenbanksicherung, die neben der primären Dateigruppe auch sämtliche Dateigruppen enthält, die zum Zeitpunkt der Sicherung Dateigruppen mit Lese-/Schreibzugriff waren. In vielen Fällen beginnt eine Teilwiederherstellungssequenz mit der Wiederherstellung einer Teilsicherung.  
  
    -   Geben Sie die PARTIAL-Option an, mit der der Start einer schrittweisen Wiederherstellung angegeben wird.  
  
    > [!NOTE]  
    >  Die PARTIAL-Option führt Sicherheitsüberprüfungen durch, mit denen sichergestellt wird, dass die resultierende Datenbank als Produktionsdatenbank geeignet ist.  
  
    -   Geben Sie die Option READ_WRITE_FILEGROUPS an, wenn es sich bei der Sicherung um eine vollständige Datenbanksicherung handelt.  
  
-   Während die Datenbank online ist, können Sie mit einer oder mehreren Onlinedateiwiederherstellungen schreibgeschützte Offlinedateien wiederherstellen, die zum Zeitpunkt der Sicherung schreibgeschützt waren. Die zeitliche Planung der Onlinedateiwiederherstellung richtet sich danach, wann die Daten online geschaltet werden sollen.  
  
     Ob Sie Daten in einer Datei wiederherstellen müssen, hängt von folgenden Faktoren ab:  
  
    -   Gültige schreibgeschützte Dateien, die mit der Datenbank konsistent sind, können direkt online geschaltet werden, indem sie ohne Wiederherstellung von Daten wiederhergestellt werden.  
  
    -   Dateien, die beschädigt oder nicht mit der Datenbank konsistent sind, müssen gespeichert werden, bevor sie wiederhergestellt werden.  
  
### <a name="examples"></a>Beispiele  
  
-   [Beispiel: Schrittweise Wiederherstellung einer Datenbank &#40;einfaches Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [Beispiel: Schrittweise Wiederherstellung nur bestimmter Dateigruppen &#40;einfaches Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
## <a name="piecemeal-restore-under-the-full-recovery-model"></a>Schrittweise Wiederherstellung mit dem vollständigen Wiederherstellungsmodell  
 Beim vollständigen oder beim massenprotokollierten Wiederherstellungsmodell ist die schrittweise Wiederherstellung für jede Datenbank verfügbar, die mehrere Dateigruppen enthält, und Sie können eine Datenbank bis zu jedem beliebigen Zeitpunkt wiederherstellen. Die Wiederherstellungssequenzen einer schrittweisen Wiederherstellung verhalten sich folgendermaßen:  
  
-   Teilwiederherstellungssequenz  
  
     Mit der Teilwiederherstellungssequenz werden die primäre Dateigruppe und optional einige sekundäre Dateigruppen wiederhergestellt.  
  
     Die erste RESTORE DATABASE-Anweisung muss folgende Voraussetzungen erfüllen:  
  
    -   Angeben der Option PARTIAL. Damit wird der Start einer schrittweisen Wiederherstellung angegeben.  
  
    -   Sie muss eine vollständige Datenbanksicherung verwenden, die die primäre Dateigruppe enthält. In vielen Fällen beginnt eine Teilwiederherstellungssequenz mit der Wiederherstellung einer Teilsicherung.  
  
    -   Wenn die Wiederherstellung zu einem bestimmten Zeitpunkt erfolgen soll, müssen Sie die Zeit in der Teilwiederherstellungssequenz angeben. In jedem nachfolgenden Schritt der Wiederherstellungssequenz muss derselbe Zeitpunkt angegeben werden.  
  
-   Mit Dateigruppen-Wiederherstellungssequenzen werden zusätzliche Dateigruppen zu einem mit der Datenbank konsistenten Zeitpunkt online geschaltet.  
  
     In der Enterprise Edition kann jede sekundäre Offlinedateigruppe wiederhergestellt werden, während die Datenbank online bleibt. Wenn eine bestimmte schreibgeschützte Datei unbeschädigt und mit der Datenbank konsistent ist, muss die Datei nicht wiederhergestellt werden. Weitere Informationen finden Sie unter [Wiederherstellen einer Datenbank ohne Wiederherstellung von Daten &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md).  
  
### <a name="applying-log-backups"></a>Anwenden von Protokollsicherungen  
 Wenn eine schreibgeschützte Dateigruppe bereits vor der Erstellung der Dateisicherung schreibgeschützt war, ist die Anwendung von Protokollsicherungen auf die Dateigruppe unnötig und wird von der Dateiwiederherstellung ausgelassen. Bei einer Dateigruppe mit Lese-/Schreibzugriff muss eine fortlaufende Kette von Protokollsicherungen auf die letzte vollständige oder differenzielle Wiederherstellung angewendet werden, um die Dateigruppe auf den Stand der aktuellen Protokolldatei zu bringen.  
  
### <a name="examples"></a>Beispiele  
  
-   [Beispiel: Schrittweise Wiederherstellung einer Datenbank &#40;Vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [Beispiel: Schrittweise Wiederherstellung nur bestimmter Dateigruppen &#40;Vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
## <a name="performing-a-piecemeal-restore-of-a-database-whose-recovery-model-has-been-switched-from-simple-to-full"></a>Ausführen einer schrittweisen Wiederherstellung einer Datenbank, deren Wiederherstellungsmodell von einfach in vollständig geändert wurde  
 Sie können eine schrittweise Wiederherstellung einer Datenbank ausführen, bei der nach der vollständigen Teil- oder Datenbanksicherung vom einfachen Wiederherstellungsmodell zum vollständigen Wiederherstellungsmodell gewechselt wurde. Angenommen, Sie führen in einer Datenbank die folgenden Schritte aus:  
  
1.  Erstellen einer Teilsicherung (backup_1) von einer Datenbank mit einfachem Modell.  
  
2.  Nach einer bestimmten Zeit erfolgt eine Änderung auf das vollständige Wiederherstellungsmodell.  
  
3.  Erstellen einer differenziellen Sicherung.  
  
4.  Ausführen von ersten Protokollsicherungen.  
  
 Im Anschluss ist folgende Sequenz gültig:  
  
1.  Eine Teilwiederherstellung, von der einige sekundäre Dateigruppen ausgenommen sind.  
  
2.  Eine differenzielle Wiederherstellung, in deren Anschluss alle weiteren benötigten Wiederherstellungsvorgänge ausgeführt werden.  
  
3.  Eine später ausgeführte Wiederherstellung einer sekundären Dateigruppe mit Lese-/Schreibzugriff WITH NORECOVERY aus der Teilsicherung backup_1.  
  
4.  Die differenzielle Sicherung, die nach allen anderen Sicherungen ausgeführt wird, die in der ursprünglichen schrittweisen Wiederherstellung gespeichert wurden, um die Daten bis zum ursprünglichen Wiederherstellungszeitpunkt wiederherzustellen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Anwenden von Transaktionsprotokollsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Wiederherstellen einer SQL Server-Datenbank zu einem Zeitpunkt &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)   
 [Übersicht über Wiederherstellungsvorgänge &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [Planen und Ausführen von Wiederherstellungssequenzen &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/plan-and-perform-restore-sequences-full-recovery-model.md)  
  
  
