---
title: Konfigurieren von Sicherungskomprimierung (SQL Server) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: backup-restore
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 430905eb-d218-458c-bd48-aeee6fbb7446
caps.latest.revision: 7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 551ec9e73f1844edfdc73af4486f46c5b41af168
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="configure-backup-compression-sql-server"></a>Konfigurieren von Sicherungskomprimierung (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Die Sicherungskomprimierung wird bei der Installation standardmäßig deaktiviert. Das Standardverhalten für die Sicherungskomprimierung wird auf Serverebene durch die Konfigurationsoption **backup compression default** definiert. Sie können jedoch die Standardeinstellung auf Serverebene überschreiben, wenn Sie eine einzelne Sicherung erstellen oder eine Reihe von Routinesicherungen einplanen. Zum Ändern der Standardeinstellung auf Serverlevel gehen Sie unter [Anzeigen oder Konfigurieren der Serverkonfigurationsoption Standardeinstellung für die Sicherungskomprimierung](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md).  
  
## <a name="override-the-backup-compression-default"></a>Überschreiben der Standardeinstellung für die Sicherungskomprimierung  
 Sie können das Verhalten der Sicherungskomprimierung für eine einzelne Sicherung, einen Sicherungsauftrag oder eine Protokollversandkonfiguration ändern.  
  
-   **[!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
     Verwenden Sie WITH NO_COMPRESSION oder WITH COMPRESSION in der [BACKUP](../../t-sql/statements/backup-transact-sql.md)-Anweisung, um die Standardeinstellung für die Serversicherungskomprimierung zu überschreiben.  
  
     Bei einer Protokollversandkonfiguration können Sie das Verhalten der Sicherungskomprimierung für Protokollsicherungen mithilfe von [sp_add_log_shipping_primary_database](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql.md)[sp_change_log_shipping_primary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-log-shipping-primary-database-transact-sql.md) steuern.  
  
-   **[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
     Informationen zum Anzeigen oder Konfigurieren der Standardoption für die Sicherungskomprimierung für eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], gehen Sie unter [Anzeigen oder Konfigurieren der Serverkonfigurationsoption Standardeinstellung für die Sicherungskomprimierung](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md).  
  
     Sie können die Standardeinstellung für die Serversicherungskomprimierung beim Erstellen einer Sicherung überschreiben, indem Sie die Optionen **Sicherung komprimieren** oder **Sicherung nicht komprimieren** in einem der folgenden Dialogfelder angeben:  
  
    -   [Datenbank sichern (Seite Optionen)](../../relational-databases/backup-restore/back-up-database-backup-options-page.md)  
  
         Beim Sichern einer Datenbank können Sie die Sicherungskomprimierung für eine einzelne Datenbank, Datei oder Protokollsicherung steuern.  
  
    -   [Verwenden des Wartungsplanungs-Assistenten](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)  
  
         Mit dem Wartungsplanungs-Assistenten können Sie die Sicherungskomprimierung bei jeder Gruppe von geplanten vollständigen oder differenziellen Datenbank- bzw. Protokollsicherungen steuern.  
  
    -   Integration Services (SSIS) [Task "Datenbank sichern"](../../integration-services/control-flow/back-up-database-task.md)  
  
         Sie können das Verhalten der Sicherungskomprimierung steuern, wenn Sie ein Paket für die Sicherung einer einzelnen oder mehrerer Datenbanken erstellen.  
  
    -   [Sicherungseinstellungen für den Transaktionsprotokollversand](../../relational-databases/databases/log-shipping-transaction-log-backup-settings.md)  
  
         Sie können das Sicherungskomprimierungsverhalten von Protokollsicherungen steuern.  
  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Sicherungskomprimierung &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-compression-sql-server.md)  
  
  
