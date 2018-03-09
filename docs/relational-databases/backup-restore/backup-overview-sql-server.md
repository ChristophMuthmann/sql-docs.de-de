---
title: "Übersicht zu Sicherungen (SQL Server) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 07/15/2016
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
- tables [SQL Server], backing up data
- backups [SQL Server]
- database backups [SQL Server]
- backup types [SQL Server]
- data backups [SQL Server]
- backing up tables [SQL Server]
- database restores [SQL Server], backups
- backing up [SQL Server], about backing up
- restoring [SQL Server], backup types
- backups [SQL Server], about
- backups [SQL Server], table-level backups unsupported
ms.assetid: 09a6e0c2-d8fd-453f-9aac-4ff24a97dc1f
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 2dbe987e0ac96162423d461c848f59e6a354e27c
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="backup-overview-sql-server"></a>Backup Overview (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Dieses Thema bietet eine Einführung in die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sicherungskomponente. Die Sicherung der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank ist wichtig für den Schutz Ihrer Daten. In dieser Diskussion werden Sicherungstypen und Sicherungseinschränkungen behandelt. Darüber hinaus bietet das Thema eine Einführung in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Sicherungsmedien und -Sicherungsgeräte.  
  
  
## <a name="terms"></a>Begriffe
 
 **Sichern [Verb]**  
 Kopiert die Daten oder Protokolldatensätze aus einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank oder aus deren Transaktionsprotokoll auf ein Sicherungsmedium, z. B. einen Datenträger, um eine Datensicherung oder Protokollsicherung zu erstellen.  
  
**Sicherung [Substantiv]**  
 Eine Kopie der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Daten, die zum Wiederherstellen der Daten nach einem Fehler verwendet werden kann. Eine Sicherung der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Daten wird auf Datenbankebene für Dateien oder Dateigruppen erstellt. Sicherungen auf Tabellenebene können nicht erstellt werden. Zusätzlich zu Datensicherungen ist beim vollständigen Wiederherstellungsmodell die Erstellung von Sicherungen des Transaktionsprotokolls erforderlich.  
  
**[Wiederherstellungsmodell](../../relational-databases/backup-restore/recovery-models-sql-server.md)**  
 Eine Datenbankeigenschaft, die die Pflege der Transaktionsprotokolle auf einer Datenbank steuert. Es stehen drei Wiederherstellungsmodelle zur Verfügung: einfach, vollständig und massenprotokolliert. Das Wiederherstellungsmodell der Datenbank bestimmt die Sicherungs- und Wiederherstellungsanforderungen.  
  
 **[Wiederherstellungsprozess](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)**  
 Ein aus mehreren Phasen bestehender Prozess, in dem alle Daten und Protokollseiten aus einer angegebenen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Sicherung in eine angegebene Datenbank kopiert werden und ein Rollforward für alle Transaktionen ausgeführt wird, die in der Sicherung protokolliert sind. Dies wird erreicht, indem die Daten durch die Übernahme protokollierter Änderungen aktualisiert werden.  
  
 ## <a name="types-of-backups"></a>Sicherungsarten  
  
 **[Kopiesicherung](../../relational-databases/backup-restore/copy-only-backups-sql-server.md)**  
 Eine Sicherung zur besonderen Verwendung, die unabhängig von der normalen Sequenz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Sicherungen erstellt wird.  
  
**Datensicherung**   
 Eine Sicherung von Daten einer vollständigen Datenbank (Datenbanksicherung), einer partiellen Datenbank (partielle Sicherung) oder einem Satz von Datendateien oder Dateigruppen (Dateisicherung).  
  
**[Datenbanksicherung](../../relational-databases/backup-restore/full-database-backups-sql-server.md)**  
 Eine Sicherung einer Datenbank. Vollständige Datenbanksicherungen stellen die gesamte Datenbank zum Zeitpunkt dar, an dem die Sicherung abgeschlossen wurde. Differenzielle Datenbanksicherungen enthalten nur Änderungen, die seit der letzten vollständigen Datenbanksicherung an der Datenbank vorgenommen wurden.  
  
 **[Differenzielle Sicherung](../../relational-databases/backup-restore/full-database-backups-sql-server.md)**  
 Eine Datensicherung, die auf der letzten vollständigen Sicherung einer vollständigen oder partiellen Datenbank oder einem Satz von Datendateien oder Dateigruppen ( *differenzielle Basis*) basiert und nur die Datenblöcke enthält, die sich seit der differenziellen Basis geändert haben.  
  
 Bei einer differenziellen Teilsicherung werden nur die Datenblöcke aufgezeichnet, die seit der vorherigen Teilsicherung geändert wurden, die als Basis der differenziellen Sicherung bezeichnet wird.  
  
**Vollständige Sicherung**  
 Eine Datensicherung, die alle Daten in einer bestimmten Datenbank oder einem Satz von Dateigruppen oder Dateien enthält. Außerdem muss die Sicherung genügend Protokolle enthalten, um die Wiederherstellung dieser Daten zu ermöglichen.  
  
**[Protokollsicherung](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)**  
 Eine Sicherung von Transaktionsprotokollen, die alle Protokolldatensätze enthält, die nicht in einer vorherigen Protokollsicherung gesichert wurden. (Vollständiges Wiederherstellungsmodell)  
  
 **[Dateisicherung](../../relational-databases/backup-restore/full-file-backups-sql-server.md)**  
 Eine Sicherung aller Datenbankdateien oder -dateigruppen.  
  
 **[Teilsicherung](../../relational-databases/backup-restore/partial-backups-sql-server.md)**  
 Enthält Daten aus nur einigen der Dateigruppen in einer Datenbank, einschließlich Daten in der primären Dateigruppe, alle Dateigruppen mit Lese-/Schreibzugriff und aller optional angegebenen schreibgeschützten Dateien.  
  
## <a name="backup-media-terms-and-definitions"></a>Sicherungsmedien – Begriffe und Definitionen  
  
 **[Sicherungsgerät](../../relational-databases/backup-restore/backup-devices-sql-server.md)**  
 Ein Datenträger oder Bandmedium, auf den bzw. das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Sicherungen geschrieben werden und von dem sie wiederhergestellt werden können. SQL Server-Sicherungen können auch in einen Windows Azure-BLOB-Speicherdienst geschrieben werden. Das **URL** -Format wird verwendet, um das Ziel und den Namen der Sicherungsdatei anzugeben. Weitere Informationen finden Sie unter [SQL Server Backup and Restore with Windows Azure Blob Storage Service](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
 **[Sicherungsmedien](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)**  
 Bänder oder Datenträgerdateien, auf die Sicherungen geschrieben wurden.  
  
 **[Sicherungssatz](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)**  
 Der Sicherungsinhalt, der bei einem erfolgreichen Sicherungsvorgang einem Mediensatz hinzugefügt wird.  
  
 **[Medienfamilie](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)**  
 Sicherungen, die auf einem einzelnen, nicht gespiegelten Medium oder auf einem Satz gespiegelter Medien in einem Mediensatz erstellt wurden.  
  
 **[Mediensatz](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)**  
 Eine geordnete Auflistung von Sicherungsmedien, Bändern oder Dateien auf Datenträgern, die in mindestens einem Sicherungsvorgang mithilfe eines festen Typs sowie einer festen Anzahl von Sicherungsmedien beschrieben wurden.  
  
 **[Gespiegelter Mediensatz](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md)**  
 Mehrere Kopien (Spiegel) eines Mediensatzes.  
  
##  <a name="BackupCompression"></a> Sicherungskomprimierung  
 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] können Sicherungen komprimiert werden, und ab [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ist die Wiederherstellung komprimierter Sicherungen möglich. Weitere Informationen finden Sie unter [Sicherungskomprimierung &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-compression-sql-server.md).  
  
##  <a name="Restrictions"></a>  Einschränkungen für Sicherungsvorgänge 
 Eine Sicherung kann erfolgen, während die Datenbank online ist und verwendet wird. Es gelten dabei jedoch folgende Einschränkungen.  
  
### <a name="cannot-back-up-offline-data"></a>Offline-Daten können nicht gesichert werden  
 Wenn im Rahmen eines Sicherungsvorgangs implizit oder explizit auf Offlinedaten verwiesen wird, tritt bei diesem Vorgang ein Fehler auf. Einige typische Fälle:  
  
-   Sie fordern eine vollständige Datenbanksicherung an, wobei eine Dateigruppe der Datenbank offline ist. Da bei der vollständigen Datenbanksicherung implizit alle Dateigruppen berücksichtigt werden, ist der Vorgang fehlerhaft.  
  
     Zum Sichern dieser Datenbank können Sie eine Dateisicherung verwenden und nur die Dateigruppen angeben, die online sind.  
  
-   Sie fordern eine Teilsicherung an, wobei eine Dateigruppe mit Lese-/Schreibzugriff offline ist. Da bei der Teilsicherung alle Dateigruppen mit Lese-/Schreibzugriff berücksichtigt werden müssen, tritt ein Fehler auf.  
  
-   Sie fordern eine Sicherung bestimmter Dateien an, wobei eine Datei nicht online ist. Dabei tritt ein Fehler auf. Wenn Sie Onlinedateien sichern möchten, können Sie die Offlinedatei in der Dateiliste auslassen und den Vorgang wiederholen.  
  
 Im Allgemeinen wird eine Protokollsicherung erfolgreich ausgeführt, selbst wenn eine oder mehrere Datendateien nicht verfügbar sind. Wenn in einer Datei jedoch massenprotokollierte Änderungen enthalten sind, die im massenprotokollierten Wiederherstellungsmodell erfolgt sind, müssen alle Dateien online sein, damit die Sicherung erfolgreich ausgeführt werden kann.  
  
### <a name="concurrency-restrictions"></a>Einschränkungen hinsichtlich der Parallelität   
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird ein Onlinesicherungsprozess verwendet, um das Ausführen einer Datenbanksicherung zu ermöglichen, während die Datenbank weiterhin verwendet wird. Bei einer Sicherung sind die meisten Vorgänge möglich, so sind z. B. die Anweisungen INSERT, UPDATE oder DELETE bei einem Sicherungsvorgang zulässig. Beim Versuch, einen Sicherungsvorgang zu starten, während eine Datenbankdatei erstellt oder gelöscht wird, wird der Sicherungsvorgang so lange verzögert, bis der Erstellungs- oder Löschvorgang abgeschlossen ist oder das Timeout für die Sicherung erreicht ist.  
  
 Folgende Vorgänge können nicht ausgeführt werden, während eine Datenbank oder ein Transaktionsprotokoll gesichert wird:  
  
-   Vorgänge, die die Dateiverwaltung betreffen, z. B. die ALTER DATABASE-Anweisung mit der Option ADD FILE oder REMOVE FILE.  
  
-   Vorgänge zum Verkleinern der Datenbank oder von Dateien. Dazu gehören auch Vorgänge zum automatischen Verkleinern.  
  
-   Wenn Sie versuchen, eine Datenbankdatei während des Sicherungsvorgangs zu erstellen oder zu löschen, tritt beim Erstellungs- oder Löschvorgang ein Fehler auf.  
  
 Wenn sich ein Sicherungsvorgang mit einem Dateiverwaltungsvorgang oder einem Verkleinerungsvorgang überschneidet, tritt ein Konflikt auf. Unabhängig davon, welcher am Konflikt beteiligte Vorgang zuerst begonnen hat, wartet der zweite Vorgang auf das Timeout der Sperre, die vom ersten Vorgang festgelegt wurde. (Der Timeoutzeitraum wird durch eine Timeouteinstellung für die Sitzung gesteuert.) Wenn die Sperre während des Timeoutzeitraums aufgehoben wird, wird der zweite Vorgang fortgesetzt. Wenn das Timeout für die Sperre eintritt, erzeugt der zweite Vorgang einen Fehler.  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
 **Sicherungsgeräte und -medien**  
  
-   [Definieren eines logischen Sicherungsmediums für eine Datenträgerdatei &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)  
  
-   [Definieren eines logischen Sicherungsmediums für ein Bandlaufwerk &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
-   [Angeben eines Datenträgers oder ein Bands als Sicherungsziel &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
-   [Löschen eines Sicherungsmediums &#40;SQL Server&#41;](../../relational-databases/backup-restore/delete-a-backup-device-sql-server.md)  
  
-   [Festlegen des Ablaufdatums für eine Sicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/set-the-expiration-date-on-a-backup-sql-server.md)  
  
-   [Anzeigen der Inhalte eines Sicherungsbands oder einer -datei &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [Anzeigen der Daten und Protokolldateien in einem Sicherungssatz &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-data-and-log-files-in-a-backup-set-sql-server.md)  
  
-   [Anzeigen der Eigenschaften und des Inhalts eines logischen Sicherungsmediums &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [Wiederherstellung einer Sicherung von einem Medium &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-backup-from-a-device-sql-server.md)  
  
-   [Lernprogramm: SQL Server-Sicherung und -Wiederherstellung im Windows Azure-BLOB-Speicherdienst](~/relational-databases/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)  
  
 **So erstellen Sie eine Sicherung**  
  
> [!NOTE]  
>  Verwenden Sie für Teilsicherungen oder Kopiesicherungen die [!INCLUDE[tsql](../../includes/tsql-md.md)][BACKUP](../../t-sql/statements/backup-transact-sql.md) -Anweisung mit der Option PARTIAL bzw. COPY_ONLY.  
  
-   [Erstellen einer vollständigen Datenbanksicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [Sichern eines Transaktionsprotokolls &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   [Sichern von Dateien und Dateigruppen &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)  
  
-   [Erstellen einer differenziellen Datenbanksicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
-   [Sichern des Transaktionsprotokolls bei beschädigter Datenbank &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)  
  
-   [Aktivieren oder deaktivieren von Sicherungsprüfsummen während der Sicherung oder Wiederherstellung &#40;SQL Server&#41;](../../relational-databases/backup-restore/enable-or-disable-backup-checksums-during-backup-or-restore-sql-server.md)  
  
-   [Angeben, ob ein Sicherungs- oder Wiederherstellungsvorgang fortgesetzt wird, nachdem ein Fehler festgestellt wurde &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-if-backup-or-restore-continues-or-stops-after-error.md)  
  
-   [Einschränken der CPU-Nutzung durch die Sicherungskomprimierung mithilfe der Ressourcenkontrolle &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)  
  
-   [Tutorial: SQL Server-Sicherung und -Wiederherstellung im Windows Azure-BLOB-Speicherdienst](~/relational-databases/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)  
  
## <a name="and-more"></a>Weitere Informationen 
 [Sichern und Wiederherstellen von SQL Server-Datenbanken](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Übersicht über Wiederherstellungsvorgänge &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [Wartungspläne](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Das Transaktionsprotokoll &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [Wiederherstellungsmodelle &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)  
  
  
