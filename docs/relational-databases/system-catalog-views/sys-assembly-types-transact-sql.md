---
title: Sys. assembly_types (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- assembly_types
- sys.assembly_types
- sys.assembly_types_TSQL
- assembly_types_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.assembly_types catalog view
ms.assetid: 35f0384f-7a6d-41b1-9461-f1406d68f317
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 79cd6c92deb31c2d6bedfa9ec8587f950accbf75
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysassemblytypes-transact-sql"></a>sys.assembly_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Enthält eine Zeile für jeden benutzerdefinierten Datentyp, der durch eine CLR-Assembly definiert ist. Die folgenden **Sys. assembly_types** in der Liste der geerbten Spalten angezeigt (finden Sie unter [sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)) nach **Rule_object_id**.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**assembly_id**|**int**|ID der Assembly, aus der dieser Typ erstellt wurde.|  
|**assembly_class**|**sysname**|Name der Klasse innerhalb der Assembly, mit der dieser Typ definiert wird.|  
|**is_binary_ordered**|**bit**|Die Bytesortierung dieses Typs entspricht der Sortierung mithilfe von Vergleichsoperatoren für den Typ.|  
|**is_fixed_length**|**bit**|Die Länge des Typs ist immer mit max_length identisch.|  
|**prog_id**|**nvarchar(40)**|ProgID des Typs gemäß Einbindung für COM.|  
|**assembly_qualified_name**|**nvarchar(4000)**|Der vollqualifizierte Name der Assembly. Der Name hat ein Format, das an Type.GetType() übergeben werden kann.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Katalogsichten für Skalartypen &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/scalar-types-catalog-views-transact-sql.md)  
  
  
