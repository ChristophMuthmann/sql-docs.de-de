---
title: Sys. event_notifications (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- event_notifications_TSQL
- event_notifications
- sys.event_notifications_TSQL
- sys.event_notifications
dev_langs:
- TSQL
helpviewer_keywords:
- sys.event_notifications catalog view
ms.assetid: 136a76ee-2b35-4418-ab46-fda2d51f7d99
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 9e9892c0f2c5c469bd061d3a0ac29fe6a6030b5a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="syseventnotifications-transact-sql"></a>sys.event_notifications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt eine Zeile für jedes Objekt, das eine ereignisbenachrichtigung mit **sys.objects.type** = EN.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Name der Ereignisbenachrichtigung.|  
|**object_id**|**int**|Objekt-ID. Ist innerhalb einer Datenbank eindeutig.|  
|**parent_class**|**tinyint**|Klasse des übergeordneten Objekts.<br /><br /> 0 = Datenbank<br /><br /> 1 = Objekt oder Spalte|  
|**parent_class_desc**|**nvarchar(60)**|DATABASE<br /><br /> OBJECT_OR_COLUMN|  
|**Parent_ID**|**int**|ID des übergeordneten Objekts ungleich NULL.<br /><br /> 0 = Die übergeordnete Klasse ist die Datenbank.|  
|**create_date**|**datetime**|Erstellungsdatum.|  
|**modify_date**|**datetime**|Entspricht immer **Create_date**.|  
|**service_name**|**nvarchar(256)**|Name des Zieldienstes, an den die Benachrichtigung gesendet wird.|  
|**broker_instance**|**nvarchar(128)**|Broker-Instanz, an den die Benachrichtigung gesendet wird.|  
|**principal_id**|**int**|ID des Datenbankprinzipals, der Besitzer dieser Ereignisbenachrichtigung ist.|  
|**creator_sid**|**varbinary(85)**|SID des Anmeldenamens, der die Ereignisbenachrichtigung erstellt hat.<br /><br /> Ist gleich NULL, wenn die Option FAN_IN nicht angegeben ist.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten für Objekte &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
