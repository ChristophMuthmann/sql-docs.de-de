---
title: Sys. database_firewall_rules (Azure SQL-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: 
ms.prod_service: sql-database
ms.reviewer: 
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.database_firewall_rules_TSQL
- database_firewall_rules_TSQL
- sys.database_firewall_rules
- database_firewall_rules
dev_langs:
- TSQL
helpviewer_keywords:
- database_firewall_rules
- sys.database_firewall_rules
ms.assetid: 2e821593-3b9f-43d6-a99b-1ceffe177faf
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c598371c8df7a92622ec43700fc504b082640e1f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sysdatabasefirewallrules-azure-sql-database"></a>sys.database_firewall_rules (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Gibt Informationen über die auf Datenbankebene Firewalleinstellungen im Zusammenhang mit Ihrem [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Firewalleinstellungen auf Datenbankebene sind besonders nützlich, wenn eigenständige Datenbankbenutzer verwendet werden. Weitere Informationen finden Sie unter [Eigenständige Datenbankbenutzer - machen Sie Ihre Datenbank portabel](../../relational-databases/security/contained-database-users-making-your-database-portable.md).  
  
 Die `sys.database_firewall_rules` -Sicht enthält die folgenden Spalten:  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|id|**GANZE ZAHL**|Der Bezeichner der Firewalleinstellung auf Datenbankebene.|  
|name|**VOM DATENTYP NVARCHAR(128)**|Der ausgewählte Name, um die Firewalleinstellung auf Datenbankebene zu beschreiben und von anderen zu unterscheiden.|  
|start_ip_address|**VARCHAR(50)-SPALTE**|Die niedrigste IP-Adresse im Bereich der Firewalleinstellung auf Datenbankebene. IP-Adressen, die gleich oder größer dieser IP-Adresse sind, können versuchen, eine Verbindung mit der [!INCLUDE[ssSDS](../../includes/sssds-md.md)]-Instanz herzustellen. Die niedrigste mögliche IP-Adresse ist `0.0.0.0`.|  
|end_ip_address|**VARCHAR(50)-SPALTE**|Die höchste IP-Adresse im Bereich der Firewalleinstellung. IP-Adressen gleich oder kleiner als dieser versuchen kann, für die Verbindung der [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Instanz. Die höchste mögliche IP-Adresse ist `255.255.255.255`.<br /><br /> Hinweis: Windows Azure-Verbindungsversuche sind zulässig, wenn sowohl dieses Feld und die **Start_ip_address** Feld gleich `0.0.0.0`.|  
|create_date|**"DATETIME"**|UTC-Datum und -Uhrzeit der Erstellung der Firewalleinstellung auf Datenbankebene.|  
|modify_date|**"DATETIME"**|UTC-Datum und -Uhrzeit der letzten Änderung der Firewalleinstellung auf Datenbankebene.|  
  
## <a name="remarks"></a>Hinweise  
 Verwenden Sie zum Entfernen einer Datenbank-Firewallregel [Sp_delete_database_firewall_rule &#40; Azure SQL-Datenbank &#41; ](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md). Zum Festlegen einer Firewallregel für alle [!INCLUDE[ssSDS](../../includes/sssds-md.md)], finden Sie unter ["sp_set_firewall_rule" &#40; Azure SQL-Datenbank &#41; ](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md). Um Informationen zu vorhandenen Datenbank Firewallregeln zurückzugeben, Fragen [Sys. database_firewall_rules (Azure SQL-Datenbank)](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Diese Sicht ist in der **master** -Datenbank und in jeder Benutzerdatenbank verfügbar. Alle Benutzer, die berechtigt sind, eine Verbindung mit der Datenbank herzustellen, haben schreibgeschützten Zugriff auf diese Sicht.  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_set_firewall_rule &#40; Azure SQL-Datenbank &#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [Sys. database_firewall_rules (Azure SQL-Datenbank)](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)   
 [Sp_delete_database_firewall_rule &#40; Azure SQL-Datenbank &#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)   
 [Konfigurieren einer Windows-Firewalls für Datenbankmodulzugriff](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)   
 [Konfigurieren einer Firewall für FILESTREAM-Zugriff](../../relational-databases/blob/configure-a-firewall-for-filestream-access.md)   
 [Konfigurieren einer Firewall für den Zugriff auf den Berichtsserver](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)  
  
  
