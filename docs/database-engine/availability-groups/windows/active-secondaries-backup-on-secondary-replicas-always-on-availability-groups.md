---
title: "Aktive sekund&#228;re Replikate: Sicherung auf sekund&#228;ren Replikaten (AlwaysOn-Verf&#252;gbarkeitsgruppen) | Microsoft Docs"
ms.custom: ""
ms.date: "05/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Sicherungspriorität"
  - "Sicherung auf sekundären Replikaten"
  - "Verfügbarkeitsgruppen [SQL Server], Verfügbarkeitsreplikate"
  - "Verfügbarkeitsgruppen [SQL Server], Sicherung auf sekundären Replikaten"
  - "Aktive sekundäre Replikate [SQL Server], Sicherung auf"
  - "Voreinstellung für die automatisierte Sicherung"
  - "Verfügbarkeitsgruppen [SQL Server], aktive sekundäre Replikate"
ms.assetid: 82afe51b-71d1-4d5b-b20a-b57afc002405
caps.latest.revision: 34
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 34
---
# Aktive sekund&#228;re Replikate: Sicherung auf sekund&#228;ren Replikaten (AlwaysOn-Verf&#252;gbarkeitsgruppen)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Die Funktionen für aktive sekundäre [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]-Replikate umfassen auch die Unterstützung von Sicherungsvorgängen auf sekundären Replikaten. Sicherungsvorgänge können E/A und CPU (mit Sicherungskomprimierung) erheblich belasten. Durch die Auslagerung von Sicherungen auf ein sekundäres Replikat mit dem Status SYNCHRONIZED oder SYNCHRONIZING können Sie die Ressourcen auf der Serverinstanz verwenden, die das primäre Replikat für Arbeitsauslastungen erster Ebene hostet.  
  
> [!NOTE]  
>  RESTORE-Anweisungen sind in den primären und sekundären Datenbanken einer Verfügbarkeitsgruppe nicht zulässig.  
  
-   [Unterstützte Sicherungstypen](#SupportedBuTypes)  
  
-   [Konfigurieren, wo Sicherungsaufträge ausgeführt werden](#WhereBuJobsRun)  
  
-   [Verwandte Aufgaben](#RelatedTasks)  
  
##  <a name="SupportedBuTypes"></a> Auf sekundären Replikaten unterstützte Sicherungstypen  
  
-   **BACKUP DATABASE** unterstützt vollständige Kopiesicherungen von Datenbanken, Dateien oder Dateigruppen nur bei der Ausführung auf sekundären Replikaten. Beachten Sie, dass sich Kopiesicherungen nicht auf die Protokollkette auswirken bzw. kein differenzielles Bitmuster löschen.  
  
-   Differenzielle Sicherungen werden auf sekundären Replikaten nicht unterstützt.  
  
-   **BACKUP LOG** unterstützt nur reguläre Protokollsicherungen (die COPY_ONLY-Option wird für Protokollsicherungen auf sekundären Replikaten nicht unterstützt).  
  
     Bei sämtlichen Protokollsicherungen von Replikaten (primär oder sekundär) wird ungeachtet ihres Verfügbarkeitsmodus (mit synchronem Commit oder mit asynchronem Commit) eine konsistente Protokollkette sichergestellt.  
  
-   Zum Sichern einer sekundären Datenbank muss ein sekundäres Replikat mit dem primären Replikat kommunizieren können und den Status **SYNCHRONIZED** oder **SYNCHRONIZING**aufweisen.  
  
##  <a name="WhereBuJobsRun"></a> Konfigurieren, wo Sicherungsaufträge ausgeführt werden  
 Das Ausführen von Sicherungen auf einem sekundären Replikat zum Auslagern der Sicherungsarbeitsauslastung vom primären Produktionsserver ist ein großer Vorteil. Durch die Ausführung von Sicherungen auf sekundären Replikaten wird es jedoch wesentlich komplexer, den Ausführungsort von Sicherungsaufträgen zu bestimmen. Um diesen Vorgang zu vereinfachen, konfigurieren Sie den Ausführungsort von Sicherungsaufträgen wie folgt:  
  
1.  Konfigurieren Sie die Verfügbarkeitsgruppe, um anzugeben, welche Verfügbarkeitsreplikate am Ort, an dem Sie Sicherungen wünschen, ausgeführt werden sollen. Weitere Informationen finden Sie unter den Parametern *AUTOMATED_BACKUP_PREFERENCE* und *BACKUP_PRIORITY* in [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/create-availability-group-transact-sql.md) oder [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md).  
  
2.  Erstellen Sie skriptbasierte Sicherungsaufträge für jede Verfügbarkeitsdatenbank auf jeder Serverinstanz, die ein Verfügbarkeitsreplikat hostet, das für das Ausführen von Sicherungen infrage kommt. Weitere Informationen finden Sie im Abschnitt „Nachverfolgung: Nach dem Konfigurieren einer Sicherung auf sekundären Replikaten“ von [Konfigurieren der Sicherung auf Verfügbarkeitsreplikaten &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
 **So konfigurieren Sie die Sicherung auf sekundären Replikaten**  
  
-   [Konfigurieren der Sicherung auf Verfügbarkeitsreplikaten &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
 **So bestimmen Sie, ob es sich beim aktuellen Replikat um ein bevorzugtes Sicherungsreplikat handelt**  
  
-   [sys.fn_hadr_backup_is_preferred_replica](../../../relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql.md)  
  
 **So erstellen Sie einen Sicherungsauftrag**  
  
-   [Verwenden des Wartungsplanungs-Assistenten](../../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)  
  
-   [Implementieren von Aufträgen](../../../ssms/agent/implement-jobs.md)  
  
## Siehe auch  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Kopiesicherungen &#40;SQL Server&#41;](../../../relational-databases/backup-restore/copy-only-backups-sql-server.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md)  
  
  