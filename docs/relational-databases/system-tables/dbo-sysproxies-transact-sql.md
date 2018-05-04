---
title: dbo.sysproxies (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dbo.sysproxies_TSQL
- sysproxies_TSQL
- dbo.sysproxies
- sysproxies
dev_langs:
- TSQL
helpviewer_keywords:
- sysproxies system table
ms.assetid: a73da875-be22-45fc-b5e2-ea7ebd48e2d6
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cce18f3a97f374a554fd9248f0ee3594205532fa
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="dbosysproxies-transact-sql"></a>dbo.sysproxies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Definiert Attribute eines ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Proxykonto. Diese Tabelle wird in der **msdb** -Datenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|ID des Proxykontos.|  
|**name**|**sysname**|Name des Proxykontos.|  
|**credential_id**|**int**|ID der vom Proxykonto verwendeten Anmeldeinformationen.|  
|**Aktiviert**|**tinyint**|Status des Proxykontos:<br /><br /> **0** = Deaktiviert. **1** = Aktiviert.|  
|**description**|**nvarchar(512)**|Beschreibung, die der Benutzer bei Erstellung des Proxykontos eingegeben hat.|  
|**user_sid**|**varbinary(85)**|Microsoft Windows-Sicherheits-ID ( *security_identifier* ) des Benutzers oder der Gruppe, der bzw. die den Proxyanmeldeinformationen zugeordnet ist.|  
|**credential_date_created**|**datetime**|Datum und Uhrzeit des Zeitpunkts, an dem die Anmeldeinformationen erstellt wurden.|  
  
## <a name="remarks"></a>Hinweise  
 Nur Mitglieder der festen Serverrolle **sysadmin** können auf die **sysproxies** -Tabelle zugreifen.  
  
## <a name="see-also"></a>Siehe auch  
 [dbo.sysproxylogin &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysproxylogin-transact-sql.md)   
 [dbo.sysproxysubsystem &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysproxysubsystem-transact-sql.md)   
 [dbo.syssubsystems &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-syssubsystems-transact-sql.md)  
  
  
