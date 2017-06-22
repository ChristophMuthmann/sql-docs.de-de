---
title: "SQL Server Managed Backup für Microsoft Azure | Microsoft-Dokumentation"
ms.custom: 
ms.date: 10/18/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: afa01165-39e0-4efe-ac0e-664edb8599fd
caps.latest.revision: 44
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 529ae718a28d99104d8835ecaf2cdc4eb5fcc63f
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="sql-server-managed-backup-to-microsoft-azure"></a>SQL Server Managed Backup für Microsoft Azure
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] verwaltet und automatisiert SQL Server-Sicherungen in Microsoft Azure Blob Storage. Sie können es SQL Server ermöglichen, den Sicherungszeitplan basierend auf der Transaktionsarbeitsauslastung Ihrer Datenbank zu bestimmen. Alternativ können Sie die erweiterten Optionen zum Bestimmen eines Zeitplans verwenden. Die Aufbewahrungseinstellungen bestimmen, wie lange die Sicherungen in Azure Blob Storage gespeichert werden. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] unterstützt die Wiederherstellung zu einem bestimmten Zeitpunkt für den angegebenen Beibehaltungszeitraum.  
  
 Ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]wurden die Verfahren und das zugrunde liegende Verhalten von [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] geändert. Weitere Informationen finden Sie unter [Migrate SQL Server 2014 Managed Backup Settings to SQL Server 2016](../../relational-databases/backup-restore/migrate-sql-server-2014-managed-backup-settings-to-sql-server-2016.md).  
  
> [!TIP]  
>  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] wird für SQL Server-Instanzen empfohlen, die auf virtuellen Microsoft Azure-Computern ausgeführt werden.  
  
## <a name="benefits"></a>Vorteile  
 Für die Automatisierung von Sicherungen für mehrere Datenbanken sind derzeit die Entwicklung einer Sicherungsstrategie, das Schreiben von eigenem Code und eine Planung der Sicherungen erforderlich. Mithilfe von [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]können Sie einen Sicherungsplan erstellen, indem Sie nur den Aufbewahrungszeitraum und den Speicherort festlegen. Obwohl erweiterte Optionen verfügbar sind, werden diese nicht benötigt. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] plant, wartet und führt die Sicherungen aus.  
  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] kann auf Datenbank- oder SQL Server-Instanzebene konfiguriert werden. Wenn Sie auf Instanzebene konfigurieren, werden alle neuen Datenbanken ebenfalls automatisch gesichert. Einstellungen auf Datenbankebene können verwendet werden, um im Einzelfall Standardwerte der Instanzebene zu überschreiben.  
  
 Sie können die Sicherungen auch verschlüsseln, um die Sicherheitsvorkehrungen zu erhöhen. Außerdem können Sie einen benutzerdefinierten Zeitplan einrichten, um zu steuern, wann die Sicherungen erstellt werden. Weitere Informationen zum Verwenden des Microsoft Azure-Blobspeicherdiensts für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Sicherungen finden Sie unter [SQL Server-Sicherung und -Wiederherstellung mit dem Microsoft Azure-Blobspeicherdienst](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
##  <a name="Prereqs"></a> Voraussetzungen  
 Microsoft Azure Storage wird von [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] zum Speichern der Sicherungsdateien verwendet. Die folgenden Voraussetzungen gelten:  
  
|Voraussetzung|Beschreibung|  
|------------------|-----------------|  
|**Microsoft Azure-Konto**|Für erste Schritte mit Azure können Sie die [kostenlose Testversion](http://azure.microsoft.com/pricing/free-trial/) verwenden, bevor Sie sich mit den [Kaufoptionen](http://azure.microsoft.com/pricing/purchase-options/)beschäftigen.|  
|**Azure-Speicherkonto**|Die Sicherungen werden in einem Azure Blob Storage zugeordneten Azure-Speicherkonto gespeichert. Eine Schritt-für-Schritt-Anleitung zum Erstellen eines Speicherkontos finden Sie unter [Informationen zu Azure-Speicherkonten](http://azure.microsoft.com/en-us/documentation/articles/storage-create-storage-account/).|  
|**Blobcontainer**|Blobs sind in Containern organisiert. Sie geben den Zielcontainer für die Sicherungsdateien an. Sie können im [Azure-Verwaltungsportal](https://manage.windowsazure.com/) oder mithilfe des [Azure PowerShell](http://azure.microsoft.com/en-us/documentation/articles/powershell-install-configure/)-Befehls **New-AzureStorageContainer** einen Container erstellen.|  
|**Shared Access Signature (SAS)**|Der Zugriff auf den Zielcontainer wird durch eine Shared Access Signature (SAS) gesteuert. Einen Überblick über die SAS finden Sie unter [Shared Access Signatures, Teil 1: Grundlagen zum SAS-Modell](http://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/). Sie können ein SAS-Token im Code oder mithilfe des PowerShell-Befehls **New-AzureStorageContainerSASToken** erstellen. Ein PowerShell-Skript, das diesen Prozess vereinfacht, finden Sie unter [Simplifying creation of SQL Credentials with Shared Access Signature ( SAS ) tokens on Azure Storage with Powershell](http://blogs.msdn.com/b/sqlcat/archive/2015/03/21/simplifying-creation-sql-credentials-with-shared-access-signature-sas-keys-on-azure-storage-containers-with-powershell.aspx)(Vereinfachen der Erstellung von SQL-Anmeldeinformationen mit Shared Access Signature-Token in Azure Storage mit PowerShell). Das SAS-Token kann in **SQL-Anmeldeinformationen** für die Verwendung mit [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]gespeichert werden.|  
|**SQL Server-Agent**|Der SQL Server-Agent muss ausgeführt werden, damit [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] funktioniert. Ziehen Sie in Betracht, die Startoption auf „automatisch“ festzulegen.|  
  
## <a name="components"></a>Components  
 Transact-SQL ist die Hauptschnittstelle für die Interaktion mit [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Gespeicherte Systemprozeduren werden für die Aktivierung, Konfiguration und Überwachung von [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]verwendet. Systemfunktionen werden zum Abrufen vorhandener Konfigurationseinstellungen, Parameterwerte und Sicherungsdateiinformationen verwendet. Erweiterte Ereignisse dienen der Überwachung von Fehlern und Warnungen. Warnmechanismen werden über SQL Agent-Aufträge und die richtlinienbasierte Verwaltung in SQL Server aktiviert. Es folgt eine Liste der Objekte und eine Beschreibung ihrer Funktionen im Hinblick auf [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].  
  
 PowerShell-Cmdlets sind ebenfalls verfügbar zur Konfiguration von [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. SQL Server Management Studio unterstützt das Wiederherstellen von Sicherungen, die mit [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] erstellt wurden, über die Aufgabe **Datenbank wiederherstellen** .  
  
|||  
|-|-|  
|Systemobjekt|Beschreibung|  
|**MSDB**|Speichert die Metadaten und den Sicherungsverlauf für alle von [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]erstellten Sicherungen.|  
|[managed_backup.sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)|Aktiviert [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].|  
|[managed_backup.sp_backup_config_advanced &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)|Konfiguriert die erweiterten Einstellungen für [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)], wie z.B. die Verschlüsselung.|  
|[managed_backup.sp_backup_config_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)|Erstellt einen benutzerdefinierten Zeitplan für [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].|  
|[managed_backup.sp_ backup_master_switch &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-master-switch-transact-sql.md)|Hält [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]an und setzt es fort.|  
|[managed_backup.sp_set_parameter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-set-parameter-transact-sql.md)|Aktiviert und konfiguriert die Überwachung für [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Beispiele: Aktivierung erweiterter Ereignisse, E-Mail-Einstellungen für Benachrichtigungen|  
|[managed_backup.sp_backup_on_demand &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-on-demand-transact-sql.md)|Führt eine Ad-hoc-Sicherung für eine Datenbank durch, die für die Verwendung von [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] ohne Unterbrechung der Protokollkette aktiviert ist.|  
|[managed_backup.fn_backup_db_config &#40;Transact-SQL&#41;](../../relational-databases/system-functions/managed-backup-fn-backup-db-config-transact-sql.md)|Gibt den aktuellen [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] -Status und die Konfigurationswerte für eine Datenbank bzw. für alle Datenbanken der Instanz zurück.|  
|[managed_backup.fn_is_master_switch_on &#40;Transact-SQL&#41;](../../relational-databases/system-functions/managed-backup-fn-is-master-switch-on-transact-sql.md)|Gibt den Status des Hauptschalters zurück.|  
|[managed_backup.sp_get_backup_diagnostics &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-get-backup-diagnostics-transact-sql.md)|Gibt die Ereignisse zurück, die von erweiterten Ereignissen protokolliert wurden.|  
|[managed_backup.fn_get_parameter &#40;Transact-SQL&#41;](../../relational-databases/system-functions/managed-backup-fn-get-parameter-transact-sql.md)|Gibt die aktuellen Werte für die Sicherungssystemeinstellungen zurück, z.B. für die Überwachungs- oder E-Mail-Einstellungen für Warnungen.|  
|[managed_backup.fn_available_backups &#40;Transact-SQL&#41;](../../relational-databases/system-functions/managed-backup-fn-available-backups-transact-sql.md)|Ruft verfügbare Sicherungen für eine angegebene Datenbank bzw. für alle Datenbanken einer Instanz ab.|  
|[managed_backup.fn_get_current_xevent_settings &#40;Transact-SQL&#41;](../../relational-databases/system-functions/managed-backup-fn-get-current-xevent-settings-transact-sql.md)|Gibt die aktuellen Einstellungen für erweiterte Ereignisse zurück.|  
|[managed_backup.fn_get_health_status &#40;Transact-SQL&#41;](../../relational-databases/system-functions/managed-backup-fn-get-health-status-transact-sql.md)|Gibt die aggregierte Anzahl von Fehlern zurück, die von den erweiterten Ereignissen für einen bestimmten Zeitraum protokolliert wurden.|  
  
## <a name="backup-strategy"></a>Sicherungsstrategie  
  
### <a name="backup-scheduling"></a>Sicherungszeitplanung  
 Sie können mithilfe der gespeicherten Systemprozedur [managed_backup.sp_backup_config_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md). Falls Sie keinen benutzerdefinierten Zeitplan angeben, werden der Typ der geplanten Sicherungen und die Sicherungshäufigkeit basierend auf der Arbeitsauslastung der Datenbank bestimmt. Anhand der Beibehaltungsdauereinstellungen wird ermittelt, wie lange eine Sicherungsdatei im Speicher gehalten werden soll. Außerdem wird die Wiederherstellbarkeit der Datenbank zu einem bestimmten Zeitpunkt innerhalb der Beibehaltungsdauer geprüft.  
  
### <a name="backup-file-naming-conventions"></a>Benennungskonventionen für Sicherungsdateien  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] verwendet den Container, den Sie angeben, damit Sie die Kontrolle über den Containernamen haben. Für Sicherungsdateien werden Nicht-Verfügbarkeitsdatenbanken mithilfe der folgenden Konvention benannt: Der Name wird mit den ersten 40 Zeichen des Datenbanknamens, der Datenbank-GUID ohne „-“ und dem Zeitstempel erstellt. Der Unterstrich wird zwischen Segmenten als Trennzeichen eingefügt. Als Dateierweiterung wird **.bak** bei einer vollständigen Sicherung und **.log** für Protokollsicherungen verwendet. Bei Datenbanken in Verfügbarkeitsgruppen gilt neben der oben beschriebenen Dateinamenskonvention, dass nach den 40 Zeichen des Datenbanknamens die GUID der Verfügbarkeitsgruppen-Datenbank angehängt wird. Der Wert für die GUID der Verfügbarkeitsgruppen-Datenbank entspricht dem group_database_id-Wert in sys.databases.  
  
### <a name="full-database-backup"></a>Vollständige Datenbanksicherung  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] -Agent plant eine vollständige Datenbanksicherung, wenn eine der folgenden Bedingungen wahr ist:  
  
-   Eine Datenbank wird zum ersten Mal für [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] aktiviert, oder [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] wird mit den Standardeinstellungen auf Instanzebene aktiviert.  
  
-   Das Anwachsen der Protokollgröße seit der letzten vollständigen Datenbanksicherung entspricht 1 GB oder mehr.  
  
-   Das maximale Zeitintervall von einer Woche seit der letzten vollständigen Datenbanksicherung wurde überschritten.  
  
-   Die Protokollkette ist unterbrochen. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] prüft in regelmäßigen Abständen, ob die Protokollkette intakt ist, indem die erste und die letzte LSN der Sicherungsdateien miteinander verglichen werden. Sollte die Protokollkette aus irgendeinem Grund unterbrochen sein, plant [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] eine vollständige Datenbanksicherung. Die häufigste Ursache für die Unterbrechung einer Protokollkette ist ein Sicherungsbefehl, der entweder mit Transact-SQL oder über eine Sicherungsaufgabe in SQL Server Management Studio ausgeführt wurde.  Weitere häufige Szenarien sind das versehentliche Löschen der Sicherungsprotokolldateien oder das versehentliche Überschreiben von Sicherungen.  
  
### <a name="transaction-log-backup"></a>Transaktionsprotokollsicherung  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] plant eine Protokollsicherung, wenn eine der folgenden Bedingungen wahr ist:  
  
-   Es wurde kein Protokollsicherungsverlauf gefunden. Dies trifft in der Regel dann zu, wenn [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] das erste Mal aktiviert wird.  
  
-   Der belegte Speicher für die Transaktionsprotokolle beträgt 5 MB oder mehr.  
  
-   Das maximale Zeitintervall von 2 Stunden seit der letzten Protokollsicherung wurde erreicht.  
  
-   Immer, wenn die Transaktionsprotokollsicherung hinter einer vollständigen Datenbanksicherung zurückliegt. Das Ziel besteht darin, die Protokollkette vor der vollständigen Sicherung zu halten.  
  
## <a name="retention-period-settings"></a>Beibehaltungsdauereinstellungen  
 Bei der Aktivierung der Sicherung müssen Sie die Beibehaltungsdauer in Tagen festlegen: Mindestwert ist 1 Tag, Maximalwert ist 30 Tage.  
  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] bewertet anhand der Beibehaltungsdauereinstellungen die Wiederherstellbarkeit der Datenbank zu einem bestimmten Zeitpunkt im angegebenen Zeitraum, um zu ermitteln, welche Sicherungsdateien behalten und welche gelöscht werden sollen. Über backup_finish_date der Sicherung wird die in den Beibehaltungsdauereinstellungen angegebene Zeit ermittelt und abgeglichen.  
  
## <a name="important-considerations"></a>Wichtige Überlegungen  
 Wenn für eine Datenbank ein Auftrag für eine vollständige Datenbanksicherung ausgeführt wird, wartet [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] , bis der aktuelle Auftrag abgeschlossen ist, bevor eine weitere vollständige Datenbanksicherung für dieselbe Datenbank ausgeführt wird. Entsprechend kann nur eine Transaktionsprotokollsicherung zu einem bestimmten Zeitpunkt ausgeführt werden. Eine vollständige Datenbanksicherung und eine Transaktionsprotokollsicherung können jedoch gleichzeitig ausgeführt werden. Fehler werden als erweiterte Ereignisse protokolliert.  
  
 Wenn mehr als 10 gleichzeitige vollständige Datenbanksicherungen geplant werden, wird über den Debug-Kanal der erweiterten Ereignisse eine Warnung ausgegeben. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] verwaltet dann eine Prioritätswarteschlange für die verbliebenen zu sichernden Datenbanken, bis alle Sicherungen geplant und abgeschlossen sind.  
  
##  <a name="support_limits"></a> Unterstützbarkeit  
 Die folgenden Einschränkungen und Überlegungen hinsichtlich der Unterstützung gelten nur für [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]:  
  
-   Die Sicherung der Systemdatenbanken **master**, **model**und **msdb** wird unterstützt. Die Sicherung von **tempdb** wird nicht unterstützt. 
  
-   Für [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]werden alle Wiederherstellungsmodelle (vollständig, massenprotokolliert und einfach) unterstützt.  
  
-   [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] -Agent unterstützt nur vollständige Datenbanksicherungen und Protokollsicherungen. Die Dateisicherungsautomatisierung wird nicht unterstützt.  
  
-   Microsoft Azure Blob Storage ist die einzige unterstützte Option zum Speichern von Sicherungen. Sicherungen auf Datenträger oder Band werden nicht unterstützt.  
  
-   [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] verwendet die Funktion „Sichern in Blockblob“. Die maximale Größe eines Blockblobs beträgt 200 GB. Die maximale Größe einer einzelnen Sicherung kann durch Verbinden jedoch bis zu 12 TB betragen. Wenn Ihre Sicherungsanforderungen diese Größen überschreiten, ziehen Sie eine Komprimierung in Betracht, und testen Sie die Sicherungsdateigröße vor dem Einrichten von [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Sie können diese testen, indem Sie eine Sicherung entweder auf einem lokalen Datenträger oder manuell mithilfe der Transact-SQL-Anweisung **BACKUP TO URL** in einen Microsoft Azure-Speicher durchführen. Weitere Informationen finden Sie unter [SQL Server Backup to URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md).  
  
-   [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] gelten ggf. bestimmte Einschränkungen, wenn eine Konfiguration in Kombination mit anderen Technologien erfolgt, die Sicherungen, eine hohe Verfügbarkeit und eine Wiederherstellung im Notfall unterstützen.  
  
## <a name="see-also"></a>Siehe auch  
- [Aktivieren der verwalteten SQL Server-Sicherung in Microsoft Azure](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md)   
- [Konfigurieren der erweiterten Optionen für die verwaltete Sicherung von SQL Server zu Microsoft Azure](../../relational-databases/backup-restore/configure-advanced-options-for-sql-server-managed-backup-to-microsoft-azure.md)   
- [Deaktivieren der verwalteten SQL Server-Sicherung in Microsoft Azure](../../relational-databases/backup-restore/disable-sql-server-managed-backup-to-microsoft-azure.md)
- [Sichern und Wiederherstellen von Systemdatenbanken](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)
- [Sichern und Wiederherstellen von SQL Server-Datenbanken](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
  
  

