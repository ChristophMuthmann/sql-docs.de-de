---
title: Sp_set_database_firewall_rule (Azure SQL-Datenbank) | Microsoft Docs
ms.custom: ''
ms.date: 08/04/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-stored-procedures
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_set_database_firewall_rule
- sp_set_database_firewall_rule_TSQL
- sys.sp_set_database_firewall_rule
- sys.sp_set_database_firewall_rule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_set_database_firewall_rule
- firewall_rules, setting database rules
ms.assetid: 8f0506b6-a4ac-4e4d-91db-8077c40cb17a
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 33ba0433400c5848cc3e96dd0afad6e8c402660d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spsetdatabasefirewallrule-azure-sql-database"></a>sp_set_database_firewall_rule (Azure SQL-Datenbank)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Erstellt oder aktualisiert die Firewallregeln auf Datenbankebene für Ihre [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Datenbank-Firewallregeln können so konfiguriert sein, für die **master** Datenbank, und für Benutzerdatenbanken auf [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Datenbank-Firewallregeln sind besonders nützlich, wenn Sie eigenständige Datenbankbenutzer verwenden. Weitere Informationen finden Sie unter [Eigenständige Datenbankbenutzer - machen Sie Ihre Datenbank portabel](../../relational-databases/security/contained-database-users-making-your-database-portable.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_set_database_firewall_rule [@name = ] [N]'name'  
, [@start_ip_address =] 'start_ip_address'  
, [@end_ip_address =] 'end_ip_address'
[ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 **[@name**  =] [N] "*Namen*"  
 Der verwendete Name, um die Firewalleinstellung auf Datenbankebene zu beschreiben und von anderen zu unterscheiden. *Namen* ist **vom Datentyp nvarchar(128)** verfügt über keinen Standardwert. Der Bezeichner für die Unicode- `N` ist optional für [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]. 
  
 **[@start_ip_address**  =] '*Start_ip_address*"  
 Die niedrigste IP-Adresse im Bereich der Firewalleinstellung auf Datenbankebene. IP-Adressen, die gleich oder größer dieser IP-Adresse sind, können versuchen, eine Verbindung mit der [!INCLUDE[ssSDS](../../includes/sssds-md.md)]-Instanz herzustellen. Die niedrigste mögliche IP-Adresse ist `0.0.0.0`. *Start_ip_address* ist **varchar(50)-Spalte** verfügt über keinen Standardwert.  
  
 [**@end_ip_address** =] '*End_ip_address*"  
 Die höchste IP-Adresse im Bereich der Firewalleinstellung auf Datenbankebene. IP-Adressen gleich oder kleiner als dieser versuchen kann, für die Verbindung der [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Instanz. Die höchste mögliche IP-Adresse ist `255.255.255.255`. *End_ip_address* ist **varchar(50)-Spalte** verfügt über keinen Standardwert.  
  
 Die folgende Tabelle enthält die unterstützten Argumente und Optionen in [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
> [!NOTE]  
>  Verbindungsversuche von Azure sind zulässig, wenn sowohl dieses Feld und die *Start_ip_address* Feld gleich `0.0.0.0`.  
  
## <a name="remarks"></a>Hinweise  
 Die Namen der Firewalleinstellungen auf Datenbankebene für eine Datenbank müssen eindeutig sein. Wenn der Name der für die gespeicherte Prozedur bereitgestellten Firewalleinstellung auf Datenbankebene bereits in der Tabelle mit den Firewalleinstellungen auf Datenbankebene vorhanden ist, werden die Start- und End-IP-Adressen aktualisiert. Andernfalls wird eine neue Firewalleinstellung auf Datenbankebene erstellt.  
  
 Beim Hinzufügen einer firewalleinstellung auf Datenbankebene, in dem die Anfangs- und die End-IP-Adressen gleich sind `0.0.0.0`, aktivieren Sie den Zugriff auf die Datenbank auf dem [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Server von anderen Azure-Ressourcen. Geben Sie einen Wert für die *Namen* Parameter, mit denen Sie denken Sie daran, welchem Zweck die firewalleinstellung dient.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die **CONTROL**-Berechtigung für die Datenbank.  
  
## <a name="examples"></a>Beispiele  
 Der folgende Code erstellt eine Datenbank firewalleinstellung auf Serverebene namens `Allow Azure` , die ermöglicht den Zugriff auf die Datenbank aus Azure.  
  
```  
-- Enable Azure connections.  
EXECUTE sp_set_database_firewall_rule N'Allow Azure', '0.0.0.0', '0.0.0.0';  
  
```  
  
 Der folgende Code erstellt eine Datenbank firewalleinstellung auf Serverebene aufgerufene `Example DB Setting 1` exklusiv für die IP-Adresse `0.0.0.4`. Anschließend wird die `sp_set_database firewall_rule` gespeicherte Prozedur erneut aufgerufen, um die End-IP-Adresse aktualisieren `0.0.0.6`in dieser firewalleinstellung. Dies erstellt einen Bereich aus dem IP-Adressen kann `0.0.0.4`, `0.0.0.5`, und `0.0.0.6` für den Datenbankzugriff.
  
```  
-- Create database-level firewall setting for only IP 0.0.0.4  
EXECUTE sp_set_database_firewall_rule N'Example DB Setting 1', '0.0.0.4', '0.0.0.4';  
  
-- Update database-level firewall setting to create a range of allowed IP addresses
EXECUTE sp_set_database_firewall_rule N'Example DB Setting 1', '0.0.0.4', '0.0.0.6';  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Azure SQL-Datenbank-Firewall](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)   
 [Vorgehensweise: Konfigurieren von Firewalleinstellungen (Azure SQL-Datenbank)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 ["sp_set_firewall_rule" &#40;Azure SQL-Datenbank&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [Sp_delete_database_firewall_rule &#40;Azure SQL-Datenbank&#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)   
 [Sys. database_firewall_rules &#40;Azure SQL-Datenbank&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)  
  
  
