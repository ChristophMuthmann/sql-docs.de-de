---
title: "Sichern und Wiederherstellen von SQL Server-Datenbanken | Microsoft Docs"
ms.custom: ""
ms.date: "07/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Notfallwiederherstellung [SQL Server], siehe Wiederherstellen [SQL Server]"
  - "Sicherungen [SQL Server]"
  - "Wiederherstellen von Datenbanken [SQL Server]"
  - "Datensicherung [SQL Server], siehe Sichern [SQL Server]"
  - "Datenbanken [SQL Server], Wiederherstellen"
  - "Sichern von Datenbanken [SQL Server]"
  - "Wiederherstellung [SQL Server], siehe Wiederherstellen [SQL Server]"
  - "Notfallwiederherstellung [SQL Server], siehe Sichern [SQL Server]"
  - "Sichern [SQL Server]"
  - "Datenbankmodul [SQL Server], Sicherungen"
  - "Datenbanken [SQL Server], Sicherungen"
ms.assetid: 570a21b3-ad29-44a9-aa70-deb2fbd34f27
caps.latest.revision: 91
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 91
---
# Sichern und Wiederherstellen von SQL Server-Datenbanken
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  In diesem Thema werden die Vorteile der Sicherung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbanken und grundlegende Begriffe zu Sicherung und Wiederherstellung erläutert. Darüber hinaus bietet das Thema eine Einführung in Sicherungs- und Wiederherstellungsstrategien für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und Sicherheitsüberlegungen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sicherungen und -Wiederherstellungen. 
  
> **Suchen Sie nach Schritt-für-Schritt-Anweisungen?** Dieses Thema enthält **keine spezifischen Schritte zum Ausführen von Sicherungen!** Wenn Sie sofort zum eigentlichen Sicherungsvorgang gelangen möchten, scrollen Sie auf dieser Seite nach unten bis zum Abschnitt mit den Links, die nach Sicherungsaufgaben und nach der Verwendung von SSMS oder T-SQL gegliedert sind.  
  
 Durch die Sicherungs- und Wiederherstellungskomponente von SQL Server wird eine wichtige Vorrichtung zum Schutz wichtiger Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbanken bereitgestellt. Um das Risiko schwerwiegenden Datenverlusts zu verringern, müssen Sie die Datenbanken regelmäßig sichern, um Änderungen an den Daten beizubehalten. Eine sorgfältig geplante Sicherungs- und Wiederherstellungsstrategie schützt Datenbanken vor Datenverlust, der durch die verschiedensten Fehler verursacht werden kann. Testen Sie Ihre Strategie, indem Sie einen Sicherungssatz wiederherstellen und dann die Datenbank wiederherstellen, um im Notfall effektiv reagieren zu können.  
  
 Neben dem lokalen Speicher für das Speichern der Sicherung unterstützt SQL Server auch das Sichern und Wiederherstellen mit dem Windows Azure-BLOB-Speicherdienst. Weitere Informationen finden Sie unter [SQL Server-Sicherung und -Wiederherstellung mit dem Microsoft Azure Blob Storage Service](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md). Für Datenbankdateien, die mit dem Microsoft Azure Blob-Speicherdienst gespeichert wurden, bietet [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] die Option, Azure-Momentaufnahmen für nahezu sofortige Sicherungen und schnellere Wiederherstellungen zu nutzen. Weitere Informationen finden Sie unter [Dateimomentaufnahme-Sicherungen für Datenbankdateien in Azure](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  
  
##  Warum Sichern (back up)?  
-   Sie können sich vor schwerwiegendem Datenverlust schützen, indem Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbanken sichern, Testwiederherstellungsprozeduren für die Sicherungen ausführen und Kopien der Sicherungen an einem sicheren Ort außerhalb Ihrer Geschäftsräume aufbewahren. **Das Sichern ist die einzige Möglichkeit, Ihre Daten zu schützen.**

     Mithilfe gültiger Datenbanksicherungen können Sie die Daten nach vielen Fehlern wiederherstellen, z. B.:  
  
    -   Medienfehler  
  
    -   Benutzerfehler (z. B. versehentliches Löschen einer Tabelle)  
  
    -   Hardwarefehler (z. B. ein beschädigter Datenträger oder der endgültige Verlust eines Servers)  
  
    -   Naturkatastrophen. Mit der SQL Server-Sicherung im Windows Azure-BLOB-Speicherdienst können Sie eine externe Sicherung in einer anderen Region als an Ihrem lokalen Standort erstellen. Diese wird dann verwendet, wenn der lokale Standort durch eine Naturkatastrophe in Mitleidenschaft gezogen wird.  
  
-   Darüber hinaus sind Sicherungen einer Datenbank hilfreich für Routineverwaltungsaufgaben, wie z. B. Kopieren einer Datenbank zwischen Servern, Einrichten von [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] oder Datenbankspiegelung und Archivierung.  
  
##  Glossarbegriffe für die Sicherung
 **Sichern** [Verb]  
 Kopiert die Daten oder Protokolldatensätze aus einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank oder aus deren Transaktionsprotokoll auf ein Sicherungsmedium, z. B. einen Datenträger, um eine Datensicherung oder Protokollsicherung zu erstellen.  
  
 **Sicherung** [Substantiv]  
 Eine Datenkopie, die zum Wiederherstellen der Daten nach einem Fehler verwendet werden kann. Sicherungen einer Datenbank können auch verwendet werden, um eine Kopie der Datenbank an einem neuen Speicherort wiederherzustellen.  
  
**Sicherungsgerät**  
 Ein Datenträger oder Bandgerät, auf den bzw. das SQL Server-Sicherungen geschrieben werden und von dem sie wiederhergestellt werden können. SQL Server-Sicherungen können auch in einen Windows Azure-BLOB-Speicherdienst geschrieben werden. Das **URL** -Format wird verwendet, um das Ziel und den Namen der Sicherungsdatei anzugeben. Weitere Informationen finden Sie unter [SQL Server-Sicherung und -Wiederherstellung mit dem Microsoft Azure Blob Storage Service](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
**Sicherungsmedien**  
 Bänder oder Datenträgerdateien, auf die Sicherungen geschrieben wurden.  
  
**Datensicherung**  
 Eine Sicherung von Daten einer vollständigen Datenbank (Datenbanksicherung), einer partiellen Datenbank (partielle Sicherung) oder einem Satz von Datendateien oder Dateigruppen (Dateisicherung).  
  
**Datenbanksicherung**  
 Eine Sicherung einer Datenbank. Vollständige Datenbanksicherungen stellen die gesamte Datenbank zum Zeitpunkt dar, an dem die Sicherung abgeschlossen wurde. Differenzielle Datenbanksicherungen enthalten nur Änderungen, die seit der letzten vollständigen Datenbanksicherung an der Datenbank vorgenommen wurden.  
  
**Differenzielle Sicherung**  
 Eine Datensicherung, die auf der letzten vollständigen Sicherung einer vollständigen oder partiellen Datenbank oder einem Satz von Datendateien oder Dateigruppen (differenzielle Basis) basiert und nur die Daten enthält, die sich gegenüber der Basis geändert haben.  
  
**Vollständige Sicherung**  
 Eine Datensicherung, die alle Daten in einer bestimmten Datenbank oder einem Satz von Dateigruppen oder Dateien enthält. Außerdem muss die Sicherung genügend Protokolle enthalten, um die Wiederherstellung dieser Daten zu ermöglichen.  
  
**Protokollsicherung**  
 Eine Sicherung von Transaktionsprotokollen, die alle Protokolldatensätze enthält, die nicht in einer vorherigen Protokollsicherung gesichert wurden. (Vollständiges Wiederherstellungsmodell)  
  
**Wiederherstellen**  
 Wiederherstellen eines stabilen und konsistenten Datenbankzustands.  
  
**recovery**  
 Eine Phase beim Starten der Datenbank oder einer Wiederherstellung, in der ein transaktionskonsistenter Zustand der Datenbank hergestellt wird.  
  
**Wiederherstellungsmodell**  
 Eine Datenbankeigenschaft, die die Pflege der Transaktionsprotokolle auf einer Datenbank steuert. Es stehen drei Wiederherstellungsmodelle zur Verfügung: einfach, vollständig und massenprotokolliert. Das Wiederherstellungsmodell der Datenbank bestimmt die Sicherungs- und Wiederherstellungsanforderungen.  
  
**Wiederherstellungsprozess**  
 Ein aus mehreren Phasen bestehender Prozess, in dem alle Daten und Protokollseiten aus einer angegebenen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sicherung in eine angegebene Datenbank kopiert werden und ein Rollforward für alle Transaktionen ausgeführt wird, die in der Sicherung protokolliert sind. Dies wird erreicht, indem die Daten durch die Übernahme protokollierter Änderungen aktualisiert werden.  
  
 ##  Sicherungs- und Wiederherstellungsstrategien  
 Das Sichern und Wiederherstellen von Daten muss jedoch auf die entsprechende Umgebung und auf die verfügbaren Ressourcen abgestimmt werden. Die zuverlässige Verwendung von Sicherungen und Wiederherstellungen erfordert daher eine Sicherungs- und Wiederherstellungsstrategie. Eine sorgfältig geplante Sicherungs- und Wiederherstellungsstrategie maximiert Datenverfügbarkeit und minimiert Datenverluste, wobei die besonderen Anforderungen des entsprechenden Unternehmens berücksichtigt werden.  
  
#### Wichtig! 
**Platzieren Sie die Datenbank und die Sicherungen auf separaten Medien. Andernfalls stehen Ihre Sicherungen nicht mehr zur Verfügung, wenn auf dem Medium mit den Datenbankdateien Fehler auftreten. Wenn Sie die Daten und die Sicherungen auf separaten Medien speichern, wird auch die E/A-Leistung für das Schreiben von Sicherungen sowie für die produktive Nutzung der Datenbank optimiert.**  
  
 Eine Sicherungs- und Wiederherstellungsstrategie enthält einen Sicherungsteil und einen Wiederherstellungsteil. Der Sicherungsteil der Strategie definiert den Typ und die Häufigkeit der Sicherungen, die Art und die Geschwindigkeit der dafür benötigten Hardware, die vorgesehene Testmethode für die Sicherungen sowie Aufbewahrungsort und -methode von Sicherungsmedien (einschließlich Sicherheitsüberlegungen). Der Wiederherstellungsteil der Strategie definiert, wer für die Ausführung der Wiederherstellungen verantwortlich ist und wie Wiederherstellungen ausgeführt werden sollen, um die jeweiligen Ziele hinsichtlich der Verfügbarkeit der Datenbank und Minimierung von Datenverlusten zu erreichen. Es empfiehlt sich, Sicherungs- und Wiederherstellungsprozeduren zu dokumentieren und eine Kopie der Dokumentation im Ausführungsbuch aufzubewahren.  
  
 Das Entwerfen einer effektiven Sicherungs- und Wiederherstellungsstrategie erfordert sorgfältiges Planen, Implementieren und Testen. Die Testphase ist erforderlich. Sie verfügen erst dann über eine Sicherungsstrategie, wenn Sie die Sicherungen, die in Ihrer Wiederherstellungsstrategie enthalten sind, in allen Kombinationen erfolgreich wiederhergestellt haben. Sie müssen eine Vielzahl von Faktoren berücksichtigen: Dabei handelt es sich z. B. um:  
  
-   Die Produktionsziele des Unternehmens im Verhältnis zur Datenbank, besonders die Anforderungen an Verfügbarkeit und Schutz vor Datenverlusten.  
  
-   Die Art Ihrer einzelnen Datenbanken, beispielsweise Größe, Verwendungsmuster, Art des Inhalts und Anforderungen im Hinblick auf Daten.  
  
-   Einschränkungen hinsichtlich der Ressourcen, wie z. B. Hardware, Mitarbeiter, Platz zum Aufbewahren von Sicherungsmedien und physische Sicherheit der aufbewahrten Medien.  

### Auswirkung des Wiederherstellungsmodells auf das Sichern und Wiederherstellen  
 Sicherungs- und Wiederherstellungsvorgänge werden im Kontext eines Wiederherstellungsmodells durchgeführt. Bei einem Wiederherstellungsmodell handelt es sich um eine Datenbankeigenschaft, mit der die Verwaltung des Transaktionsprotokolls gesteuert wird. Das Wiederherstellungsmodell einer Datenbank bestimmt, welche Sicherungsarten und Wiederherstellungsszenarien für die Datenbank unterstützt werden. Meistens wird für Datenbanken entweder das einfache Wiederherstellungsmodell oder das vollständige Wiederherstellungsmodell verwendet. Mit dem vollständigen Wiederherstellungsmodell können Sie vor dem Ausführen von Massenvorgängen ergänzend das massenprotokollierte Wiederherstellungsmodell verwenden. Eine Einführung zu diesen Wiederherstellungsmodellen und deren Auswirkung auf die Verwaltung des Transaktionsprotokolls finden Sie unter [Das Transaktionsprotokoll [SQL Server]](https://msdn.microsoft.com/library/ms190925(SQL.130).aspx).  
  
 Die Wahl des für Ihre Datenbank am besten geeigneten Wiederherstellungsmodells hängt von Ihren Geschäftsanforderungen ab. Verwenden Sie das einfache Wiederherstellungsmodell, wenn Sie die Verwaltung des Transaktionsprotokolls vermeiden und den Sicherungs- und Wiederherstellungsprozess so einfach wie möglich gestalten möchten. Wenn das Risiko eines Arbeitsdatenverlusts so klein wie möglich sein soll und Sie bereit sind, dafür einen höheren Verwaltungsaufwand in Kauf zu nehmen, verwenden Sie das vollständige Wiederherstellungsmodell. Informationen zur Auswirkung von Wiederherstellungsmodellen auf Sicherungs- und Wiederherstellungsvorgänge finden Sie unter [Übersicht über Sicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md).  
  
### Entwerfen Ihrer Sicherungsstrategie  
 Nachdem Sie ein Wiederherstellungsmodell ausgewählt haben, das Ihre Geschäftsanforderungen für eine bestimmte Datenbank erfüllt, müssen Sie eine entsprechende Sicherungsstrategie planen und implementieren. Die optimale Sicherungsstrategie hängt von verschiedenen Faktoren ab, wobei den folgenden eine besondere Bedeutung zukommt:  
  
-   Wie viele Stunden täglich müssen Anwendungen auf die Datenbank zugreifen können?  
  
     Wenn es vorhersagbare Zeiten mit wenig Datenverkehr gibt, sollten Sie vollständige Datenbanksicherungen für diesen Zeitraum planen.  
  
-   Wie häufig werden Änderungen und Updates im Allgemeinen vorgenommen?  
  
     Berücksichtigen Sie bei häufigen Änderungen Folgendes:  
  
    -   Bei Verwendung des einfachen Wiederherstellungsmodells sollten Sie zwischen vollständigen Datenbanksicherungen differenzielle Sicherungen planen. Bei einer differenziellen Sicherung werden nur die Änderungen seit der letzten vollständigen Datenbanksicherung erfasst.  
  
    -   Bei Verwendung des vollständigen Wiederherstellungsmodells sollten Sie häufige Protokollsicherungen planen. Wenn Sie zwischen vollständigen Sicherungen differenzielle Sicherungen planen, kann dies die Wiederherstellungszeit verkürzen, da Sie nach dem Wiederherstellen der Daten nur eine geringe Anzahl von Protokollsicherungen wiederherstellen müssen.  
  
-   Werden Änderungen eher in einem kleinen oder in einem großen Bereich der Datenbank vorgenommen?  
  
     Bei einer großen Datenbank, in der sich die Änderungen auf einen Teil der Dateien oder Dateigruppen konzentrieren, können Teilsicherungen und/oder Dateisicherungen sinnvoll sein. Weitere Informationen finden Sie unter [Teilsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/partial-backups-sql-server.md) und [Vollständige Dateisicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md).  
  
-   Wie viel Speicherplatz nimmt eine vollständige Datenbanksicherung auf dem Datenträger in Anspruch?  
  
 ### Schätzen der Größe einer vollständigen Datenbanksicherung  
 Vor dem Implementieren einer Sicherungs- und Wiederherstellungsstrategie sollten Sie schätzen, wie viel Speicherplatz eine vollständige Datenbanksicherung auf dem Datenträger belegen wird. Beim Sicherungsvorgang werden die in der Datenbank enthaltenen Daten in die Sicherungsdatei kopiert. Die Sicherung enthält nur die in der Datenbank vorhandenen Daten, nicht etwa ungenutzten Speicherplatz. Daher ist die Sicherung normalerweise kleiner als die Datenbank selbst. Ein Schätzwert der Größe einer vollständigen Datenbanksicherung kann mithilfe der gespeicherten Systemprozedur **sp_spaceused** ermittelt werden. Weitere Informationen finden Sie unter [sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md).  
  
### Planen von Sicherungen  
 Da ein Sicherungsvorgang nur minimale Auswirkungen auf ausgeführte Transaktionen hat, können Sicherungsvorgänge auch während der normalen Vorgänge ausgeführt werden. Sie können eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sicherung mit minimalen Auswirkungen auf die produktive Arbeitslast ausführen.  
   
>  Informationen zu Parallelitätseinschränkungen während der Sicherung finden Sie unter [Übersicht über Sicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md).  
  
 Nachdem Sie entschieden haben, welche Arten von Sicherungen Sie benötigen und wie oft Sie diese jeweils durchführen müssen, empfiehlt es sich, im Rahmen eines Datenbankwartungsplans für die Datenbank die regelmäßige Durchführung dieser Sicherungen zu planen. Informationen zu Wartungsplänen für Datenbank- und Protokollsicherungen und zu deren Erstellung finden Sie unter [Use the Maintenance Plan Wizard](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md).  
  
### Testen von Sicherungen  
 Sie verfügen erst dann über eine Wiederherstellungsstrategie, wenn Sie die Sicherungen getestet haben. Es ist entscheidend, dass Sie Ihre Sicherungsstrategie für jede Ihrer Datenbanken gründlich testen, indem Sie eine Kopie der Datenbank auf einem Testsystem wiederherstellen. Sie müssen die Wiederherstellung jedes Sicherungstyps testen, den Sie zu verwenden beabsichtigen.  
  
 Es empfiehlt sich, für jede Datenbank ein Betriebshandbuch zu führen. In diesem Betriebshandbuch sollten der Aufbewahrungsort der Sicherungen, ggf. die Namen der Sicherungsmedien sowie Angaben zum Zeitaufwand für die Wiederherstellung der Testsicherungen vermerkt sein.  
  
## Weitere Informationen zu Sicherungstasks  
-   [Erstellen eines Wartungsplans](../../relational-databases/maintenance-plans/create-a-maintenance-plan.md)  
  
-   [Erstellen eines Auftrags](../../ssms/agent/create-a-job.md)  
  
-   [Planen eines Auftrags](../../ssms/agent/schedule-a-job.md)  
  
## Arbeiten mit Sicherungsgeräten und Sicherungsmedien  
-   [Definieren eines logischen Sicherungsmediums für eine Datenträgerdatei &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)  
  
-   [Definieren eines logischen Sicherungsmediums für ein Bandlaufwerk &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
-   [Angeben eines Datenträgers oder ein Bands als Sicherungsziel &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
-   [Löschen eines Sicherungsmediums &#40;SQL Server&#41;](../../relational-databases/backup-restore/delete-a-backup-device-sql-server.md)  
  
-   [Festlegen des Ablaufdatums für eine Sicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/set-the-expiration-date-on-a-backup-sql-server.md)  
  
-   [Anzeigen der Inhalte eines Sicherungsbands oder einer -datei &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [Anzeigen der Daten und Protokolldateien in einem Sicherungssatz &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-data-and-log-files-in-a-backup-set-sql-server.md)  
  
-   [Anzeigen der Eigenschaften und des Inhalts eines logischen Sicherungsmediums &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [Wiederherstellung einer Sicherung von einem Medium &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-backup-from-a-device-sql-server.md)  
  
## Erstellen von Sicherungen  
**HINWEIS!** Verwenden Sie für Teilsicherungen oder Kopiesicherungen die [!INCLUDE[tsql](../../includes/tsql-md.md)][BACKUP](../../t-sql/statements/backup-transact-sql.md)-Anweisung mit der Option PARTIAL bzw. COPY_ONLY.  
  
 ### Verwenden von SSMS   
-   [Erstellen einer vollständigen Datenbanksicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [Sichern eines Transaktionsprotokolls &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   [Sichern von Dateien und Dateigruppen &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)  
  
-   [Erstellen einer differenziellen Datenbanksicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
 ### Verwenden von T-SQL  
-   [Einschränken der CPU-Nutzung durch die Sicherungskomprimierung mithilfe der Ressourcenkontrolle &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)  
  
-   [Sichern des Transaktionsprotokolls bei beschädigter Datenbank &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)  
  
-   [Aktivieren oder deaktivieren von Sicherungsprüfsummen während der Sicherung oder Wiederherstellung &#40;SQL Server&#41;](../../relational-databases/backup-restore/enable-or-disable-backup-checksums-during-backup-or-restore-sql-server.md)  
  
-   [Angeben, ob ein Sicherungs- oder Wiederherstellungsvorgang fortgesetzt wird, nachdem ein Fehler festgestellt wurde &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify if backup or restore continues or stops after error.md)  
  
## Wiederherstellen von Datensicherungen 
### Verwenden von SSMS 
-   [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
-   [Wiederherstellen einer Datenbank an einem neuen Speicherort &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)  
  
-   [Wiederherstellen einer differenziellen Datenbanksicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-differential-database-backup-sql-server.md)  
  
-   [Wiederherstellen von Dateien und Dateigruppen &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)  
  
### Verwenden von T-SQL
-   [Wiederherstellen einer Datenbanksicherung unter dem einfachen Wiederherstellungsmodell &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)  
  
-   [Wiederherstellen einer Datenbank bis zum Fehlerzeitpunkt im vollständigen Wiederherstellungsmodell &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore database to point of failure - full recovery.md)  
  
-   [Wiederherstellen von Dateien und Dateigruppen über vorhandene Dateien &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-over-existing-files-sql-server.md)  
  
-   [Wiederherstellen von Dateien an einem neuen Speicherort &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-to-a-new-location-sql-server.md)  
  
-   [Wiederherstellen der master-Datenbank &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-the-master-database-transact-sql.md)  

## Wiederherstellen von Transaktionsprotokollen (vollständiges Wiederherstellungsmodell)
### Verwenden von SSMS  
-   [Wiederherstellen einer Datenbank bis zu einer markierten Transaktion &#40;SQL Server Management Studio&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)  
  
-   [Wiederherstellen einer Transaktionsprotokollsicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
-   [Wiederherstellen einer SQL Server-Datenbank zu einem Zeitpunkt &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
 ### Verwenden von T-SQL 
-   [Wiederherstellen einer SQL Server-Datenbank zu einem Zeitpunkt &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
 
-   [Erneutes Starten eines unterbrochenen Wiederherstellungsvorgangs &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restart-an-interrupted-restore-operation-transact-sql.md)  
  
-   [Wiederherstellen einer Datenbank ohne Wiederherstellung von Daten &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md)  
 
## Weitere Informationen und Ressourcen
 [Übersicht über Sicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [Übersicht über Wiederherstellungsvorgänge &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../Topic/RESTORE%20\(Transact-SQL\).md)   
 [Sichern und Wiederherstellen von Analysis Services-Datenbanken](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)   
 [Sichern und Wiederherstellen von Volltextkatalogen und Indizes](../../relational-databases/search/back-up-and-restore-full-text-catalogs-and-indexes.md)   
 [Sichern und Wiederherstellen von replizierten Datenbanken](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 [Das Transaktionsprotokoll &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [Wiederherstellungsmodelle &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)   
 [Mediensätze, Medienfamilien und Sicherungssätze &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)  
  
  