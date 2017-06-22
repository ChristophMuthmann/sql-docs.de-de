---
title: Migrieren der verwalteten Sicherungseinstellungen von SQL Server 2014 zu SQL Server 2016 | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ae937ebb-24ff-4a33-be3c-8f85328dfc75
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 902ad2ddd95a26f36ff9519e55d7af77ca7e2d8a
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="migrate-sql-server-2014-managed-backup-settings-to-sql-server-2016"></a>Migrieren der verwalteten Sicherungseinstellungen von SQL Server 2014 zu SQL Server 2016
  In diesem Thema werden Migrationsaspekte [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] bei der Aktualisierung von [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] auf [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]erläutert.  
  
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
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Managed Backup für Microsoft Azure](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
  
  
