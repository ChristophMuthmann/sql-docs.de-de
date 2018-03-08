---
title: Sp_set_firewall_rule (Azure SQL-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 07/28/2016
ms.prod: 
ms.prod_service: sql-database, sql-data-warehouse
ms.reviewer: 
ms.service: sql-database
ms.component: system-stored-procedures
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_set_firewall_rule
- sp_set_firewall_rule_TSQL
- sys.sp_set_firewall_rule
- sys.sp_set_firewall_rule_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sp_set_firewall_rule
- firewall_rules, setting server rules
ms.assetid: a974a561-5382-4039-8499-3a56767bcefe
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 38ef5788aba91bfde21df091321a69dbacbeb8e9
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spsetfirewallrule-azure-sql-database"></a>sp_set_firewall_rule (Azure SQL-Datenbank)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

  Erstellt oder aktualisiert die Firewalleinstellungen auf Serverebene für den [!INCLUDE[ssSDS](../../includes/sssds-md.md)]-Server. Diese gespeicherte Prozedur ist nur in der master-Datenbank auf den prinzipalanmeldung auf Serverebene oder Azure Active Directory-Dienstprinzipal zugewiesenen verfügbar.  
  
  
## <a name="syntax"></a>Syntax  
  
```
sp_set_firewall_rule [@name =] 'name', 
    [@start_ip_address =] 'start_ip_address', 
    [@end_ip_address =] 'end_ip_address'
[ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 Die folgende Tabelle enthält die unterstützten Argumente und Optionen in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
|Name|Datatype|Description|  
|----------|--------------|-----------------|  
|[@name =] 'Name'|**VOM DATENTYP NVARCHAR(128)**|Der verwendete Name, um die Firewalleinstellung auf Serverebene zu beschreiben und von anderen zu unterscheiden.|  
|[@start_ip_address =] "Start_ip_address"|**VARCHAR(50)-SPALTE**|Die niedrigste IP-Adresse im Bereich der Firewalleinstellung auf Serverebene. IP-Adressen, die gleich oder größer dieser IP-Adresse sind, können versuchen, eine Verbindung mit dem [!INCLUDE[ssSDS](../../includes/sssds-md.md)]-Server herzustellen. Die niedrigste mögliche IP-Adresse ist `0.0.0.0`.|  
|[@end_ip_address =] "End_ip_address"|**VARCHAR(50)-SPALTE**|Die höchste IP-Adresse im Bereich der Firewalleinstellung auf Serverebene. IP-Adressen, die kleiner oder gleich dieser IP-Adresse sind, können versuchen, eine Verbindung mit dem [!INCLUDE[ssSDS](../../includes/sssds-md.md)]-Server herzustellen. Die höchste mögliche IP-Adresse ist `255.255.255.255`.<br /><br /> Hinweis: Verbindungsversuche von Azure sind zulässig, wenn sowohl dieses Feld und die *Start_ip_address* Feld gleich `0.0.0.0`.|  
  
## <a name="remarks"></a>Hinweise  
 Die Namen der Firewalleinstellungen auf Serverebene müssen eindeutig sein. Wenn der Name der für die gespeicherte Prozedur bereitgestellten Einstellung bereits in der Tabelle mit den Firewalleinstellungen vorhanden ist, werden die Start- und End-IP-Adressen aktualisiert. Andernfalls wird eine neue Firewalleinstellung auf Serverebene erstellt.  
  
 Beim Hinzufügen, in dem die Anfangs- und die End-IP-Adressen gleich sind, einer firewalleinstellung auf Serverebene `0.0.0.0`, Aktivieren des Zugriffs auf Ihre [!INCLUDE[ssSDS](../../includes/sssds-md.md)] -Server durch Azure. Geben Sie einen Wert für die *Namen* Parameter, mit denen Sie denken Sie daran, welchem Zweck die firewalleinstellung auf Serverebene dient.  
  
 In [!INCLUDE[ssSDS](../../includes/sssds-md.md)], Anmeldedaten erforderlich, um eine Verbindung zu authentifizieren und Firewallregeln auf Serverebene werden in jeder Datenbank vorübergehend zwischengespeichert. Dieser Cache wird in regelmäßigen Abständen aktualisiert. Führen Sie zum Erzwingen einer Aktualisierung des Authentifizierungscache und stellen Sie sicher, dass eine Datenbank die aktuelle Version der Tabelle Anmeldungen verfügt, [DBCC FLUSHAUTHCACHE &#40; Transact-SQL &#41; ](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Nur der Server serverebenenprinzipal-Anmeldung von im Rahmen des Bereitstellungsprozesses erstellt oder ein Azure Active Directory-Dienstprinzipal als Administrator kann erstellen oder Ändern von Firewallregeln auf Serverebene zugewiesen. Der Benutzer muss mit der master-Datenbank, führen Sie "sp_set_firewall_rule" verbunden werden.  
  
## <a name="examples"></a>Beispiele  
 Der folgende Code erstellt eine Firewall auf Serverebene Einstellung `Allow Azure` , die Zugriff über Azure ermöglicht. Führen Sie Folgendes in der virtuellen Masterdatenbank ein.  
  
```  
-- Enable Windows Azure connections.  
exec sp_set_firewall_rule N'Allow Azure', '0.0.0.0', '0.0.0.0';  
  
```  
  
 Der folgende Code erstellt eine Firewalleinstellung auf Serverebene namens `Example setting 1` nur für die IP-Adresse `0.0.0.2`. Anschließend wird die `sp_set_firewall_rule` gespeicherte Prozedur erneut aufgerufen, um die End-IP-Adresse aktualisieren `0.0.0.4`in dieser firewalleinstellung. Dies erstellt einen Bereich aus dem IP-Adressen kann `0.0.0.2`, `0.0.0.3`, und `0.0.0.4` auf den Server zuzugreifen.  
  
```  
-- Create server-level firewall setting for only IP 0.0.0.2  
exec sp_set_firewall_rule N'Example setting 1', '0.0.0.2', '0.0.0.2';  
  
-- Update server-level firewall setting to create a range of allowed IP addresses
exec sp_set_firewall_rule N'Example setting 1', '0.0.0.2', '0.0.0.4';  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Azure SQL-Datenbank-Firewall](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)   
 [Vorgehensweise: Konfigurieren von Firewalleinstellungen (Azure SQL-Datenbank)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 [Sys. firewall_rules &#40; Azure SQL-Datenbank &#41;](../../relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database.md)
