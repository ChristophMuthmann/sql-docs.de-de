---
title: syscollector_collection_items (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- syscollector_collection_items_TSQL
- syscollector_collection_items
dev_langs:
- TSQL
helpviewer_keywords:
- syscollector_collection_items view
- add data collector view
ms.assetid: a279ecd1-a59c-4315-9f08-bf221f00a465
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ca9b8aed18c716e235d1848d7130395cf4fe7875
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="syscollectorcollectionitems-transact-sql"></a>syscollector_collection_items (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen über ein Element in einem Sammlungssatz zurück.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**collection_set_id**|**int**|Identifiziert den Sammlungssatz. Lässt keine NULL-Werte zu.|  
|**collection_item_id**|**int**|Identifiziert ein Element im Sammlungssatz. Lässt keine NULL-Werte zu.|  
|**collector_type_uid**|**uniqueidentifier**|Die für die Identifikation des Sammlertyps verwendete GUID. Lässt keine NULL-Werte zu.|  
|**name**|**nvarchar(4000)**|Der Name des Sammlungssatzes. Lässt NULL-Werte zu.|  
|**frequency**|**int**|Die Häufigkeit, mit der Daten von einem Sammelelement gesammelt werden. Lässt keine NULL-Werte zu.|  
|**parameters**|**xml**|Beschreibt die Parametrisierung für den Sammlertyp, der dem Sammelelement zugeordnet ist. Das XML-Schema für dieses sammelelement wird mit der XML-Schema (XSD) in gespeicherten überprüft die **Parameter_schema** für einen bestimmten sammlertyp. Lässt NULL-Werte zu. Weitere Informationen finden Sie unter [Syscollector_collector_types &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/syscollector-collector-types-transact-sql.md).|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert SELECT für **dc_operator**, **dc_proxy**.  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Prozeduren für den Datensammler &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Sichten des Datensammlers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [Datensammlung](../../relational-databases/data-collection/data-collection.md)  
  
  
