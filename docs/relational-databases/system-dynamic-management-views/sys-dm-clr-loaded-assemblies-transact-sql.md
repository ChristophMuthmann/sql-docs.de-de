---
title: dm_clr_loaded_assemblies (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_clr_loaded_assemblies
- sys.dm_clr_loaded_assemblies_TSQL
- dm_clr_loaded_assemblies_TSQL
- sys.dm_clr_loaded_assemblies
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_clr_loaded_assemblies dynamic management view
ms.assetid: 8523d8db-d8a0-4b1f-ae19-6705d633e0a6
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: da771a7d64383bf9328d04353c071fbe9f8a1fc6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmclrloadedassemblies-transact-sql"></a>sys.dm_clr_loaded_assemblies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt für jede in den Serveradressraum geladene verwaltete Benutzerassembly eine Zeile zurück. Verwenden Sie diese Ansicht, verstehen und Behandeln von CLR-Integration Datenbankobjekte, die verwalteten in ausgeführt werden, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Assemblys stellen DLL-Dateien mit verwaltetem Code dar, die zum Definieren und Bereitstellen von verwalteten Datenbankobjekten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet werden. Wenn ein Benutzer eines dieser verwalteten Datenbankobjekte ausführt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und der CLR geladen die Assembly (und seinen verweisen), in dem das verwaltete Datenbankobjekt definiert wird. Die Assembly bleibt in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] geladen, damit die Leistung optimiert wird, sodass die in der Assembly enthaltenen verwalteten Datenbankobjekte in Zukunft aufgerufen werden können, ohne dass die Assembly neu geladen werden muss. Die Assembly wird nicht entladen, bis [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht genügend Arbeitsspeicher vorhanden. Weitere Informationen zu Assemblys und zur CLR-Integration finden Sie unter [CLR Hosted Environment](../../relational-databases/clr-integration/clr-integration-architecture-clr-hosted-environment.md). Weitere Informationen zu verwalteten Datenbankobjekten finden Sie unter [Erstellen von Datenbankobjekten mit Common Language Runtime &#40;CLR&#41; Integration](../../relational-databases/clr-integration/database-objects/building-database-objects-with-common-language-runtime-clr-integration.md).  

  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**assembly_id**|**int**|ID der geladenen Assembly. Die **Assembly_id** dienen zum Suchen nach weiteren Informationen über die Assembly in die [sys.assemblies &#40;Transact-SQL&#41; ](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md) -Katalogsicht angezeigt. Beachten Sie, dass die [!INCLUDE[tsql](../../includes/tsql-md.md)] [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md) Katalog zeigt Assemblys nur in der aktuellen Datenbank. Mit der **sqs.dm_clr_loaded_assemblies** -Sicht werden alle geladenen Assemblys auf dem Server angezeigt.|  
|**appdomain_address**|**int**|Adresse der Anwendungsdomäne (**AppDomain**), in der die Assembly geladen wird. Alle Assemblys, die sich im Besitz eines einzelnen Benutzers befinden, werden stets in derselben **AppDomain**geladen. Die **Appdomain_address** können verwendet werden, um weitere Informationen zum Suchen der **AppDomain** in der [dm_clr_appdomains](../../relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql.md) anzeigen.|  
|**load_time**|**datetime**|Zeit, zu der die Assembly geladen wurde. Beachten Sie, dass die Assembly geladen, bis bleibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht genügend Arbeitsspeicher vorhanden ist und entlädt die **AppDomain**. Sie können überwachen, **Load_time** , wie häufig [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht genügend Arbeitsspeicher vorhanden und entlädt die **AppDomain**.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
## <a name="remarks"></a>Hinweise  
 Die **dm_clr_loaded_assemblies.appdomain_address** -Sicht besitzt eine n:1-Beziehung mit  **dm_clr_appdomains.appdomain_address**. Die **dm_clr_loaded_assemblies.assembly_id** -Sicht besitzt eine 1:n-Beziehung mit **sys.assemblies.assembly_id**.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird veranschaulicht, wie Details zu allen Assemblys in der aktuellen Datenbank angezeigt werden können, die aktuell geladen sind.  
  
```  
 SELECT a.name, a.assembly_id, a.permission_set_desc, a.is_visible, a.create_date, l.load_time   
FROM sys.dm_clr_loaded_assemblies AS l   
INNER JOIN sys.assemblies AS a  
ON l.assembly_id = a.assembly_id;  
```  
  
 Im folgenden Beispiel wird veranschaulicht, wie Details der **AppDomain** angezeigt werden können, in der eine bestimmte Assembly geladen ist.  
  
```  
SELECT appdomain_id, creation_time, db_id, user_id, state  
FROM sys.dm_clr_appdomains AS a  
WHERE appdomain_address =   
(SELECT appdomain_address   
 FROM sys.dm_clr_loaded_assemblies  
 WHERE assembly_id = 555);  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Common Language Runtime verbundene dynamische Verwaltungssichten &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  
