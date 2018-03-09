---
title: Model-Datenbank | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/04/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- template databases [SQL Server]
- model database [SQL Server], about model databases
- model database [SQL Server]
ms.assetid: 4e4f739b-fd27-4dce-8be6-3d808040d8d7
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 6733a6d7440071e655004df7dc7926b33503ed1b
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="model-database"></a>model-Datenbank
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Die **model**-Datenbank wird als Vorlage für alle Datenbanken verwendet, die auf einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz erstellt werden. Da **tempdb** bei jedem Start von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellt wird, muss die **model** -Datenbank zu jedem Zeitpunkt auf einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -System vorhanden sein. Der gesamte Inhalt der **model** -Datenbank, einschließlich Datenbankoptionen, wird in die neue Datenbank kopiert. Einige Einstellungen der **model** -Datenbank werden auch zum Erstellen einer neuen **tempdb** -Datenbank während des Startvorgangs verwendet; deshalb muss die **model** -Datenbank immer in einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -System vorhanden sein.  
  
 Neu erstellte Benutzerdatenbanken verwenden dasselbe [Wiederherstellungsmodell](../../relational-databases/backup-restore/recovery-models-sql-server.md) wie die model-Datenbank. Der Standard ist vom Benutzer konfigurierbar. Informationen zum aktuellen Wiederherstellungsmodell der model-Datenbank finden Sie unter [Anzeigen oder Ändern des Wiederherstellungsmodells einer Datenbank &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md).  
  
> [!IMPORTANT]  
>  Wenn Sie die **model**-Datenbank mit benutzerspezifischen Vorlageninformationen ändern, empfiehlt es sich, dass Sie **model** sichern. Weitere Informationen finden Sie unter [Sichern und Wiederherstellen von Systemdatenbanken &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md).  
  
## <a name="model-usage"></a>Verwenden der model-Datenbank  
 Wenn eine CREATE DATABASE-Anweisung ausgegeben wird, wird der erste Teil der Datenbank erstellt, indem der Inhalt der **model** -Datenbank kopiert wird. Der Rest der neuen Datenbank wird dann mit leeren Seiten gefüllt.  
  
 Wenn Sie Änderungen an der **model** -Datenbank vornehmen, werden diese Änderungen an alle anschließend erstellten Datenbanken vererbt. Sie könnten z. B. Berechtigungen oder Datenbankoptionen festlegen oder Objekte wie Tabellen, Funktionen oder gespeicherte Prozeduren hinzufügen. Die Dateieigenschaften der **model** -Datenbank stellen eine Ausnahme dar und werden bis auf die Anfangsgröße der Datendatei ignoriert. Die anfängliche Standardgröße der model-Datenbankdaten und der Protokolldatei beträgt 8 MB.  
  
## <a name="physical-properties-of-model"></a>Physische Eigenschaften der model-Datenbank  
 Die folgende Tabelle zeigt die Anfangskonfigurationswerte der **model** -Daten und -Protokolldateien.  
  
|File|Logischer Name (logical name)|Physischer Name (physical name)|Dateivergrößerung (file growth)|  
|----------|------------------|-------------------|-----------------|  
|Primäre Daten|modeldev|model.mdf|Automatische Vergrößerung um 64 MB, bis der Speicherplatz auf dem Datenträger erschöpft ist.|  
|Log|modellog|modellog.ldf|Automatische Vergrößerung um 64 MB bis maximal 2 TB.|  
  
 Informationen zu den Standardwerten für die Dateivergrößerung für Versionen vor [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]finden Sie unter [model-Datenbank](https://msdn.microsoft.com/library/ms186388\(v=sql.120\).aspx).  
  
 Informationen zum Verschieben der **model** -Datenbank oder -Protokolldateien finden Sie unter [Verschieben von Systemdatenbanken](../../relational-databases/databases/move-system-databases.md).  
  
### <a name="database-options"></a>Datenbankoptionen  
 Die folgende Tabelle zeigt den Standardwert jeder Datenbankoption in der **model** -Datenbank und gibt an, ob die Option geändert werden kann. Zum Anzeigen der aktuellen Einstellungen dieser Optionen verwenden Sie die Katalogsicht [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) .  
  
|Datenbankoption|Standardwert|Kann geändert werden.|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|OFF|ja|  
|ANSI_NULL_DEFAULT|OFF|ja|  
|ANSI_NULLS|OFF|ja|  
|ANSI_PADDING|OFF|ja|  
|ANSI_WARNINGS|OFF|ja|  
|ARITHABORT|OFF|ja|  
|AUTO_CLOSE|OFF|ja|  
|AUTO_CREATE_STATISTICS|ON|ja|  
|AUTO_SHRINK|OFF|ja|  
|AUTO_UPDATE_STATISTICS|ON|ja|  
|AUTO_UPDATE_STATISTICS_ASYNC|OFF|ja|  
|CHANGE_TRACKING|OFF|nein|  
|CONCAT_NULL_YIELDS_NULL|OFF|ja|  
|CURSOR_CLOSE_ON_COMMIT|OFF|ja|  
|CURSOR_DEFAULT|GLOBAL|ja|  
|Datenbankverfügbarkeitsoptionen|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|nein<br /><br /> ja<br /><br /> ja|  
|DATE_CORRELATION_OPTIMIZATION|OFF|ja|  
|DB_CHAINING|OFF|nein|  
|ENCRYPTION|OFF|nein|  
|MIXED_PAGE_ALLOCATION|ON|nein|  
|NUMERIC_ROUNDABORT|OFF|ja|  
|PAGE_VERIFY|CHECKSUM|ja|  
|PARAMETERIZATION|SIMPLE|ja|  
|QUOTED_IDENTIFIER|OFF|ja|  
|READ_COMMITTED_SNAPSHOT|OFF|ja|  
|RECOVERY|Hängt von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Edition ab*|ja|  
|RECURSIVE_TRIGGERS|OFF|ja|  
|Service Broker-Optionen|DISABLE_BROKER|nein|  
|TRUSTWORTHY|OFF|nein|  
  
 *Informationen zum Überprüfen des aktuellen Wiederherstellungsmodells der Datenbank finden Sie unter [Anzeigen oder Ändern des Wiederherstellungsmodells einer Datenbank &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md) oder [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).  
  
 Eine Beschreibung dieser Datenbankoptionen finden Sie unter [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
## <a name="restrictions"></a>Restrictions  
 Die folgenden Operationen können an der **model** -Datenbank nicht ausgeführt werden:  
  
-   Hinzufügen von Dateien oder Dateigruppen.  
  
-   Ändern der Sortierung. Die Standardsortierung entspricht der Serversortierung.  
  
-   Ändern des Datenbankbesitzers Der Besitzer von**model** ist **sa**.  
  
-   Löschen der Datenbank.  
  
-   Löschen des **guest** -Benutzers aus der Datenbank.  
  
-   Aktivieren von Change Data Capture  
  
-   Teilnehmen an der Datenbankspiegelung.  
  
-   Entfernen der primären Dateigruppe, der primären Datendatei oder der Protokolldatei.  
  
-   Umbenennen der Datenbank oder der primären Dateigruppe.  
  
-   Versetzen der Datenbank in den OFFLINE-Modus.  
  
-   Versetzen der primären Dateigruppe in den READ_ONLY-Modus.  
  
-   Erstellen von Prozeduren, Sichten oder Triggern mit der Option WITH ENCRYPTION. Der Verschlüsselungsschlüssel ist an die Datenbank gebunden, in der das Objekt erstellt wird. In der **model** -Datenbank erstellte verschlüsselte Objekte können nur in **model**verwendet werden.  
  
## <a name="related-content"></a>Verwandte Inhalte  
 [Systemdatenbanken](../../relational-databases/databases/system-databases.md)  
  
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
  
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
 [Verschieben von Datenbankdateien](../../relational-databases/databases/move-database-files.md)  
  
  
