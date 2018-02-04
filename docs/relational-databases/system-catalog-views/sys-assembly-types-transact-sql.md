---
title: Sys. assembly_types (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f4411b518085338e18b01697fd445ca1d18e7ce1
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysassemblytypes-transact-sql"></a>sys.assembly_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Enthält eine Zeile für jeden benutzerdefinierten Datentyp, der durch eine CLR-Assembly definiert ist. Die folgenden **Sys. assembly_types** in der Liste der geerbten Spalten angezeigt (siehe [sys.types &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)) nach **Rule_object_id**.  
  
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
 [Skalare Typen Katalogsichten &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/scalar-types-catalog-views-transact-sql.md)  
  
  
