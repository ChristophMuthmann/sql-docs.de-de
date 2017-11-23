---
title: Sys. Foreign_Keys (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- foreign_keys
- sys.foreign_keys
- sys.foreign_keys_TSQL
- foreign_keys_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.foreign_keys catalog view
ms.assetid: e960df1a-13fc-43ee-ba91-34c1b719ac2c
caps.latest.revision: "37"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f2051dc726a4622f5340dc0972cf6fc38798d3f9
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sysforeignkeys-transact-sql"></a>sys.foreign_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Enthält eine Zeile pro Objekt, das eine FOREIGN KEY-Einschränkung mit **sys.object.type** = f  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**\<Von sys.objects geerbte Spalten >**||Eine Liste der Spalten, die diese Sicht erbt, finden Sie unter [sys.objects &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).|  
|**referenced_object_id**|**int**|ID des Objekts, auf das verwiesen wird.|  
|**key_index_id**|**int**|ID des Schlüsselindexes innerhalb des Objekts, auf das verwiesen wird.|  
|**is_disabled**|**bit**|Die FOREIGN KEY-Einschränkung ist deaktiviert.|  
|**is_not_for_replication**|**bit**|Die FOREIGN KEY-Einschränkung wurde mithilfe der Option NOT FOR REPLICATION erstellt.|  
|**Sys. check_constraints**|**bit**|Die FOREIGN KEY-Einschränkung wurde nicht vom System überprüft.|  
|**delete_referential_action**|**tinyint**|Die referenzielle Aktion, die für den Fall eines Löschvorgangs für FOREIGN KEY deklariert wurde.<br /><br /> 0 = Keine Aktion<br /><br /> 1 = Überlappend<br /><br /> 2 = NULL festlegen<br /><br /> 3 = Standard festlegen|  
|**delete_referential_action_desc**|**nvarchar(60)**|Beschreibung der referenziellen Aktion, die für den Fall eines Löschvorgangs für FOREIGN KEY deklariert wurde:<br /><br /> NO_ACTION<br /><br /> CASCADE<br /><br /> SET_NULL<br /><br /> SET_DEFAULT|  
|**update_referential_action**|**tinyint**|Die referenzielle Aktion, die für den Fall eines Updatevorgangs für FOREIGN KEY deklariert wurde.<br /><br /> 0 = Keine Aktion<br /><br /> 1 = Überlappend<br /><br /> 2 = NULL festlegen<br /><br /> 3 = Standard festlegen|  
|**update_referential_action_desc**|**nvarchar(60)**|Beschreibung der referenziellen Aktion, die für den Fall eines Updatevorgangs für FOREIGN KEY deklariert wurde:<br /><br /> NO_ACTION<br /><br /> CASCADE<br /><br /> SET_NULL<br /><br /> SET_DEFAULT|  
|**is_system_named**|**bit**|1 = Namen vom System generiert wurde.<br /><br /> 0 = Der Name wurde vom Benutzer angegeben.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Katalogsichten für Objekte &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Häufig gestellte Fragen zu Abfragen des SQL Server-Systemkatalogs](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
