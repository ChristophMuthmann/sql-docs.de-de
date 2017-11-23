---
title: Sp_delete_firewall_rule (Azure SQL-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 07/27/2016
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
- sp_delete_firewall_rule_TSQL
- sp_delete_firewall_rule
- sys.sp_delete_firewall_rule
- sys.sp_delete_firewall_rule_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_delete_firewall_rule procedure
ms.assetid: cf93eed1-ba97-4850-9fcc-b9c5a9317908
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: aa2815c27668bc680ce5da72b6713e29b517f43b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spdeletefirewallrule-azure-sql-database"></a>sp_delete_firewall_rule (Azure SQL-Datenbank)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

  Entfernt Firewalleinstellungen auf Serverebene vom [!INCLUDE[ssSDS](../../includes/sssds-md.md)]-Server. Diese gespeicherte Prozedur ist nur in der master-Datenbank für den Prinzipalanmeldenamen auf Serverebene verfügbar.  

  
## <a name="syntax"></a>Syntax  
  
```  
sp_delete_firewall_rule [@name =] 'name' 
[ ; ] 
```  
  
## <a name="arguments"></a>Argumente  
 Das Argument der gespeicherten Prozedur lautet:  
  
 [@name =] '*Namen*"  
 Der Name der Firewalleinstellung auf Serverebene, die entfernt wird. *Namen* ist **Nvarchar (128)** hat keinen Standardwert.  
  
## <a name="remarks"></a>Hinweise  
 In [!INCLUDE[ssSDS](../../includes/sssds-md.md)], Anmeldedaten erforderlich, um eine Verbindung zu authentifizieren und Firewallregeln auf Serverebene werden in jeder Datenbank vorübergehend zwischengespeichert. Dieser Cache wird in regelmäßigen Abständen aktualisiert. Führen Sie zum Erzwingen einer Aktualisierung des Authentifizierungscache und stellen Sie sicher, dass eine Datenbank die aktuelle Version der Tabelle Anmeldungen verfügt, [DBCC FLUSHAUTHCACHE &#40; Transact-SQL &#41; ](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Firewallregeln auf Serverebene können nur durch den Prinzipalanmeldenamen auf Serverebene gelöscht werden. Der Benutzer muss mit der Masterdatenbank auszuführende Sp_delete_firewall_rule verbunden werden.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird die Firewalleinstellung auf Serverebene namens Example setting 1 entfernt. Führen Sie die Anweisung in der virtuellen Masterdatenbank ein.  
  
```   
EXEC sp_delete_firewall_rule N'Example setting 1';   
```  
  
## <a name="see-also"></a>Siehe auch  
 [Azure SQL-Datenbank-Firewall](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)   
 [Vorgehensweise: Konfigurieren von Firewalleinstellungen (Azure SQL-Datenbank)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 [Sp_set_firewall_rule &#40; Azure SQL-Datenbank &#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [Sys. firewall_rules &#40; Azure SQL-Datenbank &#41;](../../relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database.md)  
  
  


