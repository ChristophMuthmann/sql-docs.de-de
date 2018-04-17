---
title: dm_xe_packages (Transact-SQL) | Microsoft Docs
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
- dm_xe_packages_TSQL
- sys.dm_xe_packages_TSQL
- dm_xe_packages
- sys.dm_xe_packages
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xe_packages dynamic management view
- extended events [SQL Server], views
ms.assetid: 2e5ecbe9-3ea8-45e6-a161-e31671a03e1d
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b3b2750f9df15cedf531eee94432761e0168036a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmxepackages-transact-sql"></a>sys.dm_xe_packages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Listet alle für das Modul für erweiterte Ereignisse registrierten Pakete.  
  
 
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|name|**nvarchar(60)**|Der Name des Pakets. Die Beschreibung wird vom Paket selbst verfügbar gemacht. Lässt keine NULL-Werte zu.|  
|guid|**uniqueidentifier**|Die GUID, die das Paket identifiziert. Lässt keine NULL-Werte zu.|  
|description|**nvarchar(256)**|Die Paketbeschreibung. Descriptionis vom Paketersteller festgelegt und ist nicht zulässig.|  
|capabilities|**int**|Bitmap, die die Funktionen dieses Pakets beschreibt. Lässt NULL-Werte zu.|  
|capabilities_desc|**nvarchar(256)**|Eine Liste aller möglichen Funktionen für dieses Paket. Lässt NULL-Werte zu.|  
|module_guid|**uniqueidentifier**|Die GUID des Moduls, das dieses Paket verfügbar macht. Lässt keine NULL-Werte zu.|  
|module_address|**varbinary(8)**|Die Basisadresse, an der das Modul geladen wird, das das Paket enthält. Ein einzelnes Modul macht möglicherweise mehrere Pakete verfügbar. Lässt keine NULL-Werte zu.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
## <a name="remarks"></a>Hinweise  
 Die für das Modul für erweiterte Ereignisse registrierten Pakete machen Folgendes verfügbar: Ereignisse, die Aktionen, die beim Auslösen der Ereignisse ausgeführt werden können, sowie Ziele für die synchrone und asynchrone Verarbeitung von Ereignisdaten.  
  
 Diese Pakete können dynamisch in einen Prozessadressbereich geladen werden. Sobald das Paket geladen wird, registriert es alle Objekte, die es verfügbar macht, für das Modul für erweiterte Ereignisse.  
  
## <a name="relationship-cardinalities"></a>Kardinalität der Beziehungen  
  
||||  
|-|-|-|  
|Von|Aktion|Beziehung|  
|sys.dm_xe_packages.module_address|sys.dm_os_loaded_modules.base_address|n:1|  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

