---
title: Migrieren der verwalteten Sicherungseinstellungen von SQL Server 2014 zu SQL Server 2016 | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ae937ebb-24ff-4a33-be3c-8f85328dfc75
caps.latest.revision: "7"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0bbc82f05c8bd82abf999602a2881a47b435d7a1
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="migrate-sql-server-2014-managed-backup-settings-to-sql-server-2016"></a>Migrieren der verwalteten Sicherungseinstellungen von SQL Server 2014 zu SQL Server 2016
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In diesem Thema werden Migrationsaspekte für [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] bei der Aktualisierung von [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] auf [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] erläutert.  
  
 Die Verfahren und das zugrunde liegende Verhalten von [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] wurden in [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]geändert. In den folgenden Abschnitten werden die funktionale Änderungen und deren Bedeutung beschrieben.  
  
## <a name="overview"></a>Übersicht  
 Die folgende Tabelle beschreibt einige der wichtigsten funktionalen Unterschiede für [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] zwischen [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] und [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].  
  
|Bereich|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|  
|----------|---------------------------|---------------------------|  
|**Namespace:**|smart_admin|managed_backup|  
|**Gespeicherte Systemprozeduren:**|sp_set_db_backup<br /><br /> sp_set_instance_backup|[managed_backup.sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)<br /><br /> [sp_backup_config_advanced](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)<br /><br /> [sp_backup_config_schedule](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)|  
|**Sicherheit:**|SQL-Anmeldeinformationen mit einem Microsoft Azure-Speicherkonto und Ihrem Zugriffsschlüssel.|SQL-Anmeldeinformationen mit einem Microsoft Azure Shared Access Signature (SAS)-Token.|  
|**Zugrunde liegende Speicher:**|Microsoft Azure-Speicher mithilfe des Seiten-Blobs.|Microsoft Azure-Speicher mithilfe des Block-Blobs.|  
  
## <a name="benefits"></a>Vorteile  
 Die neuen Funktionen in [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]bieten zahlreiche Vorteile.  
  
-   Die Speicherkosten für Block-Blobs sind geringer.  
  
-   Mit Striping können Sie erheblich größere Sicherungskopien (12 TB im Vergleich zu 1 TB bei Seiten-Blobs) speichern.  
  
-   Striping verbessert auch die Wiederherstellungszeit für große Datenbanken  
  
-   Informationen zu weiteren Verbesserungen an [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)][!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]finden Sie unter [SQL Server Managed Backup to Microsoft Azure](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md).  
  
## <a name="considerations"></a>Weitere Überlegungen  
 Nach dem Upgrade von [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]sind die folgenden Aspekte bezüglich [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] zu beachten:  
  
-   Alle zuvor für [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] in [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] konfigurierten Datenbanken verwenden weiterhin die **smart_admin-** Systemprozeduren und das zugrunde liegende Verhalten in [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].  
  
-   Die **smart_admin** -Prozeduren werden für neue Konfigurationen von [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] in [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]nicht unterstützt. Sie müssen die neuen **managed_backup** -Prozeduren und -Funktionen verwenden.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [SQL Server Managed Backup für Microsoft Azure](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
  
  
