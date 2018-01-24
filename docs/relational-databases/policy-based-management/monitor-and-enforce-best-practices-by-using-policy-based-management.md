---
title: "Überwachen und Erzwingen von Best Practices mit der richtlinienbasierten Verwaltung | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Best Practices [Database Engine]
ms.assetid: 46788407-187e-4b0b-bfe4-529af8d77c60
caps.latest.revision: "27"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f48c7d177acea6812a7b10610a2ab67930b3e9e2
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="monitor-and-enforce-best-practices-by-using-policy-based-management"></a>Überwachen und Erzwingen von Best Practices mit der richtlinienbasierten Verwaltung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Mit der richtlinienbasierten Verwaltung können Sie bewährte Methoden für [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] überwachen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt eine Reihe von Richtliniendateien bereit, die Sie als Richtlinien für Best Practices importieren und für die Auswertung der Richtlinien für einen Zielsatz mit Instanzen, Instanzobjekten, Datenbanken oder Datenbankobjekten verwenden können. Sie können Richtlinien manuell auswerten, Richtlinien zum Auswerten eines Zielsatzes entsprechend einem Zeitplan festlegen oder Richtlinien zum Auswerten eines Zielsatzes entsprechend einem Ereignis angeben. Weitere Informationen finden Sie unter [Verwalten von Servern mit der richtlinienbasierten Verwaltung](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md).  
  
## <a name="policy-and-rules-for-database-engine"></a>Richtlinie und Regeln für Datenbankmodul  
 Die folgende Tabelle enthält die Richtlinien, die in der Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] enthalten sind, sowie Informationen über die Regeln für bewährte Methoden, die von den einzelnen Richtlinien ausgewertet werden. Die Richtlinien werden als XML-Dateien gespeichert und werden in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]importiert. Weitere Informationen über das Importieren von Richtlinien finden Sie unter [Importieren einer Richtlinie der richtlinienbasierten Verwaltung](../../relational-databases/policy-based-management/import-a-policy-based-management-policy.md).  
  
|Richtlinienname|Regel für Best Practice|  
|-----------------|------------------------|  
|Verschlüsselungsalgorithmus für asymmetrischen Schlüssel|[Verschlüsselungsstärke von asymmetrischen Schlüsseln](../../relational-databases/policy-based-management/asymmetric-keys-encryption-strength.md)|  
|Speicherort für Sicherung und Datendatei|[Sicherungsdateien und Datenbankdateien müssen auf separaten Medien gespeichert sein](http://msdn.microsoft.com/library/7039bebb-1f25-4cf3-81f1-393dfb78da12)|  
|Sicherungs- und Datendateispeicherort|[Platzieren von Daten- und Protokolldateien auf separaten Laufwerken](../../relational-databases/policy-based-management/place-data-and-log-files-on-separate-drives.md)|  
|Automatisches Schließen der Datenbank|[Festlegen der Datenbankoption AUTO_CLOSE auf OFF](../../relational-databases/policy-based-management/set-the-auto-close-database-option-to-off.md)|  
|Automatisches Verkleinern der Datenbank|[Festlegen der AUTO_SHRINK-Datenbankoption auf OFF](../../relational-databases/policy-based-management/set-the-auto-shrink-database-option-to-off.md)|  
|Datenbanksortierung|[Festlegen der Sortierung benutzerdefinierter Datenbanken übereinstimmend zu jener der master- und model-Datenbanken](http://msdn.microsoft.com/library/c686446f-dae1-4b05-a3df-837b3422988d)|  
|Datenbankseitenüberprüfung|[Festlegen der PAGE_VERIFY-Datenbankoption auf CHECKSUM](../../relational-databases/policy-based-management/set-the-page-verify-database-option-to-checksum.md)|  
|Datenbankseitenstatus|[Prüfen der Integrität von Datenbanken mit fehlerverdächtigen Seiten](../../relational-databases/policy-based-management/check-integrity-of-database-with-suspect-pages.md)|  
|Gastberechtigungen|[Gastberechtigungen für Benutzerdatenbanken](../../relational-databases/policy-based-management/guest-permissions-on-user-databases.md)|  
|Datum der letzten erfolgreichen Sicherung|[Obsolete Sicherung](../../relational-databases/policy-based-management/outdated-backup.md)|  
|Öffentlich – Keine Serverberechtigungen|[Serverberechtigungen für 'public'](../../relational-databases/policy-based-management/server-public-permissions.md)|  
|Überlappung der SQL Server-64-Bit-Affinitätsmaske|[Correct Affinity Mask and Affinity Input and Output Mask Overlap](../../relational-databases/policy-based-management/correct-affinity-mask-and-affinity-input-and-output-mask-overlap.md)|  
|SQL Server-Affinitätsmaske|[Beibehalten des Standardwerts für die Affinitätsmaske](../../relational-databases/policy-based-management/keep-the-affinity-mask-default-value.md)|  
|Schwellenwert für blockierte SQL Server-Prozesse|[Erhöhen oder Deaktivieren des Schwellenwerts für blockierte Prozesse](../../relational-databases/policy-based-management/increase-or-disable-blocked-process-threshold.md)|  
|SQL Server-Standardablaufverfolgung|[Protokolldateien für Standardablaufverfolgung deaktiviert](../../relational-databases/policy-based-management/default-trace-log-files-disabled.md)|  
|SQL Server - Dynamische Sperren|[Beibehalten des Standardwerts für die Konfigurationsoption 'locks'](../../relational-databases/policy-based-management/keep-the-locks-configuration-option-default-value.md)|  
|SQL Server-Lightweightpooling|[Deaktivieren des Lightweightpoolings](../../relational-databases/policy-based-management/disable-lightweight-pooling.md)|  
|SQL Server-Anmeldemodus|[Auswählen eines Authentifizierungsmodus](../../relational-databases/security/choose-an-authentication-mode.md)|  
|Maximaler Grad an Parallelität für SQL Server|[Festlegen der 'Max. Grad an Parallelität'-Option auf optimale Leistung](../../relational-databases/policy-based-management/set-the-max-degree-of-parallelism-option-for-optimal-performance.md)|  
|Maximale Arbeitsthreadanzahl von SQL Server für die 32-Bit-Konfiguration von SQL Server 2000|[Überprüfen der Einstellung 'Max. Anzahl von Arbeitsthreads'](../../relational-databases/policy-based-management/verify-max-worker-threads-setting.md)|  
|Maximale Arbeitsthreadanzahl von SQL Server für die 64-Bit-Konfiguration von SQL Server 2000|[Überprüfen der Einstellung 'Max. Anzahl von Arbeitsthreads'](../../relational-databases/policy-based-management/verify-max-worker-threads-setting.md)|  
|Maximale Arbeitsthreadanzahl von SQL Server für SQL Server 2005 und höher|[Überprüfen der Einstellung 'Max. Anzahl von Arbeitsthreads'](../../relational-databases/policy-based-management/verify-max-worker-threads-setting.md)|  
|SQL Server-Netzwerkpaketgröße|[Netzwerkpaketgröße darf 8060 Bytes nicht überschreiten](../../relational-databases/policy-based-management/network-packet-size-should-not-exceed-8060-bytes.md)|  
|SQL Server-Kennwortablauf|[Ablauf des SQL Server-Anmeldekennworts](../../relational-databases/policy-based-management/sql-server-login-password-expiration.md)|  
|SQL Server-Kennwortrichtlinie|[Sicherheit des SQL Server-Anmeldekennworts](../../relational-databases/policy-based-management/sql-server-login-password-strength.md)|  
|Symmetrische Schlüsselverschlüsselung für Benutzerdatenbanken|[Symmetrische Schlüssel für Benutzerdatenbanken](../../relational-databases/policy-based-management/symmetric-keys-on-user-databases.md)|  
|Symmetrischer Schlüssel für master-Datenbank|[Symmetrische Schlüssel für Systemdatenbanken](../../relational-databases/policy-based-management/symmetric-keys-on-system-databases.md)|  
|Symmetrischer Schlüssel für Systemdatenbanken|[Symmetrische Schlüssel für Systemdatenbanken](../../relational-databases/policy-based-management/symmetric-keys-on-system-databases.md)|  
|Vertrauenswürdige Datenbank|[Bit für die Kennzeichnung der Datenbank als vertrauenswürdig](../../relational-databases/policy-based-management/trustworthy-bit.md)|  
|Fehler aufgrund einer Beschädigung einer Cluster-Datenträgerressource im Windows-Ereignisprotokoll|[Erkennen von SCSI-Hostadapterproblemen](../../relational-databases/policy-based-management/detect-scsi-host-adapter-issues.md)|  
|Gerätetreiber-Steuerungsfehler im Windows-Ereignisprotokoll|[Gerätetreiber-Steuerungsfehler](../../relational-databases/policy-based-management/device-driver-control-error.md)|  
|Fehler "Gerät nicht bereit" im Windows-Ereignisprotokoll|[Fehler 'Gerät nicht bereit'](../../relational-databases/policy-based-management/device-not-ready-error.md)|  
|Fehler aufgrund fehlerhafter E/A-Anforderung im Windows-Ereignisprotokoll|[Detect Failed Input and Output Requests](../../relational-databases/policy-based-management/detect-failed-input-and-output-requests.md)|  
|E/A-Verzögerungswarnung im Windows-Ereignisprotokoll|[Check Disk Input and Output Subsystem for IO Delay Problems](../../relational-databases/policy-based-management/check-disk-input-and-output-subsystem-for-io-delay-problems.md)|  
|E/A-Fehler im Windows-Ereignisprotokoll während eines Hardwareseitenfehlers|[Input and Output Error During Hard Page Fault](../../relational-databases/policy-based-management/input-and-output-error-during-hard-page-fault.md)|  
|Fehler beim erneuten Leseversuch im Windows-Ereignisprotokoll|[Überprüfen des Datenträger-E/A-Subsystems auf Lesewiederholungsprobleme](../../relational-databases/policy-based-management/check-disk-input-output-subsystem-for-read-retry-problems.md)|  
|E/A-Timeoutfehler des Speichersystems im Windows-Ereignisprotokoll|[Speichersystem – E/A-Timeout](../../relational-databases/policy-based-management/storage-system-input-output-time-out.md)|  
|Fehler aufgrund eines Systemfehlers im Windows-Ereignisprotokoll|[Unerwartete Systemfehler](../../relational-databases/policy-based-management/unexpected-system-failures.md)|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Arbeiten mit Facets der richtlinienbasierten Verwaltung](../../relational-databases/policy-based-management/working-with-policy-based-management-facets.md)  
  
  
