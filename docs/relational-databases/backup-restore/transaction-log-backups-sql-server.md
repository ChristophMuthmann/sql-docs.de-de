---
title: Transaktionsprotokollsicherungen (SQL Server) | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/05/2018
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
- backing up [SQL Server], transaction logs
- transaction log backups [SQL Server], creating
- log backups [SQL Server]
- transaction log backups [SQL Server], sequencing
ms.assetid: f4a44a35-0f44-4a42-91d5-d73ac658a3b0
caps.latest.revision: "52"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 8a3cf97eb9e60f25c57b1a81d9c71b730c0cd168
ms.sourcegitcommit: fbbb050f43ecb780281b370ec73fdcd472eb0ecc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/06/2018
---
# <a name="transaction-log-backups-sql-server"></a>Transaktionsprotokollsicherungen (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Dieses Thema ist nur für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbanken relevant, die das vollständige oder das massenprotokollierte Wiederherstellungsmodell verwenden. In diesem Thema wird das Sichern des Transaktionsprotokolls einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank erläutert.  
  
 Vor dem Erstellen von Protokollsicherungen muss bereits mindestens eine vollständige Sicherung durchgeführt worden sein. Danach kann das Transaktionsprotokoll jederzeit gesichert werden, es sei denn, das Protokoll wurde gerade gesichert. 
 
Es empfiehlt sich, Protokollsicherungen häufig auszuführen, damit auf diese Weise die Gefahr von Datenverlusten verringert und das Abschneiden des Transaktionsprotokolls angewendet werden kann. 
 
In der Regel erstellt ein Datenbankadministrator von Zeit zu Zeit eine vollständige Datenbanksicherung, z. B. einmal pro Woche, sowie optional in kürzeren Abständen eine Reihe von differenziellen Datenbanksicherungen, z. B. täglich. Unabhängig von den Datenbanksicherungen sichert der Datenbankadministrator das Transaktionsprotokoll sehr häufig. Der optimale Abstand zwischen Sicherungen ist abhängig von Faktoren wie der Wichtigkeit der Daten, der Größe der Datenbank und der Arbeitsauslastung des Servers. Weitere Informationen zur Implementierung einer guten Strategie finden Sie in diesem Thema unter [Empfehlungen](#Recommendations). 
   
##  <a name="LogBackupSequence"></a> Funktionsweise einer Protokollsicherungssequenz  
 Die Sequenz der Transaktionsprotokollsicherungen ( *Protokollkette* ) ist unabhängig von den Datensicherungen. Stellen Sie sich z. B. folgende Ereignissequenz vor.  
  
|Uhrzeit|Ereignis|  
|----------|-----------|  
|08:00 Uhr|Sichern der Datenbank.|  
|12:00 Uhr|Sichern des Transaktionsprotokolls.|  
|16:00 Uhr|Sichern des Transaktionsprotokolls.|  
|18:00 Uhr|Sichern der Datenbank.|  
|20:00 Uhr|Sichern des Transaktionsprotokolls.|  
  
 Die um 20:00 Uhr erstellte Transaktionsprotokollsicherung enthält Transaktionsprotokolldatensätze von 16:00 Uhr bis 20:00 Uhr, die den Zeitpunkt der Erstellung der vollständigen Datenbanksicherung um 18:00 Uhr umfassen. Die Transaktionsprotokollsicherungen wurden von der anfänglichen vollständigen Datenbanksicherung, die um 20:00 Uhr erstellt wurde, bis zur letzten Sicherung des Transaktionsprotokolls, die um 20:00 Uhr erstellt wurde, durchgehend durchgeführt. Informationen zum Anwenden dieser Protokollsicherungen finden Sie im Beispiel unter [Anwenden von Transaktionsprotokollsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md).  
  
##  <a name="Recommendations"></a> Empfehlungen  
  
-   Wenn ein Transaktionsprotokoll beschädigt wird, gehen die Änderungen seit der letzten gültigen Sicherung verloren. Daher empfehlen wir dringend, Protokolldateien auf einem fehlertoleranten Datenträger zu speichern.  
  
-   Wenn eine Datenbank beschädigt ist oder in Kürze wiederhergestellt werden soll, ist es ratsam, eine [Sicherung des Protokollfragments](../../relational-databases/backup-restore/tail-log-backups-sql-server.md) zu erstellen, damit Sie den aktuellen Stand der Datenbank wiederherstellen können.  
  
-   Standardmäßig wird bei jedem erfolgreichen Sicherungsvorgang dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlerprotokoll und dem Systemereignisprotokoll ein Eintrag hinzugefügt. Wenn Sie das Protokoll regelmäßig sichern, kann die Anzahl dieser Erfolgsmeldungen schnell ansteigen, d. h., es entstehen sehr große Fehlerprotokolle, die das Suchen nach anderen Meldungen erschweren können. In solchen Fällen können Sie diese Protokolleinträge mithilfe des Ablaufverfolgungsflags 3226 unterdrücken, wenn keines der Skripts von diesen Einträgen abhängig ist. Weitere Informationen finden Sie unter [Ablaufverfolgungsflags &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).  

-   Führen Sie entsprechend Ihren Geschäftsanforderungen ausreichend häufige Protokollsicherungen aus. Die Häufigkeit sollte sich danach richten, inwiefern Sie Datenverlust (beispielsweise durch einen beschädigten Protokollspeicher) tolerieren können. 
   -   Beim Festlegen einer geeigneten Häufigkeit gilt es, einen Kompromiss aus Ihrer Toleranz gegenüber der Gefahr von Datenverlust und Ihrer Fähigkeit zum Speichern, Verwalten und zum möglichen Wiederherstellen von Protokollsicherungen zu finden. Denken Sie bei der Implementierung Ihrer Wiederherstellungsstrategie an die erforderliche [RTO](http://wikipedia.org/wiki/Recovery_time_objective) und [RPO](http://wikipedia.org/wiki/Recovery_point_objective) und insbesondere an den Zeitplan für die Protokollsicherung.
   -   Es kann ausreichen, alle 15 bis 30 Minuten eine Protokollsicherung auszuführen. Wenn es für Ihr Geschäft erforderlich ist, die Gefahr des Datenverlusts zu minimieren, können Sie Protokollsicherungen häufiger ausführen. Häufigere Protokollsicherungen bieten zusätzlich den Vorteil, dass das Protokoll häufiger abgeschnitten wird, wodurch kleinere Protokolldateien entstehen.  
  
> [!IMPORTANT]
> Um die Anzahl der zum Wiederherstellen benötigten Protokollsicherungen zu begrenzen, ist es wichtig, Daten regelmäßig zu sichern. Beispielsweise können Sie eine wöchentliche vollständige Datenbanksicherung und tägliche differenzielle Datenbanksicherungen planen.  
> Nicht vergessen: Denken Sie bei der Implementierung Ihrer Wiederherstellungsstrategie an die erforderliche [RTO](http://wikipedia.org/wiki/Recovery_time_objective) und [RPO](http://wikipedia.org/wiki/Recovery_point_objective) und insbesondere an den Zeitplan für die vollständige differenzielle Datenbanksicherung.
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
 **So erstellen Sie eine Transaktionsprotokollsicherung**  
  
-   [Sichern eines Transaktionsprotokolls &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Backup.SqlBackup%2A> (SMO)  
  
 Informationen zum Planen von Sicherungsaufträgen finden Sie unter [Use the Maintenance Plan Wizard](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md).  
  

## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Das Transaktionsprotokoll &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [Transaktionsprotokollsicherungen – Handbuch zur Architektur und Verwaltung von Transaktionsprotokollen in SQL Server](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Backups)     
 [Sichern und Wiederherstellen von SQL Server-Datenbanken](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Protokollfragmentsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)   
 [Anwenden von Transaktionsprotokollsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)  
  
  
