---
title: Sys. numbered_procedures (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.numbered_procedures_TSQL
- numbered_procedures
- sys.numbered_procedures
- numbered_procedures_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.numbered_procedures catalog view
ms.assetid: 5b6d6498-bac6-4266-94b9-d16ef5089cf0
caps.latest.revision: "18"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e6a8dbd0f26b39c4fda367d2057cb9eb361586c5
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sysnumberedprocedures-transact-sql"></a>sys.numbered_procedures (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Enthält eine Zeile für jede gespeicherte Prozedur von SQL Server, die als nummerierte Prozedur erstellt wurde. Für die gespeicherte Basisprozedur (Nummer = 1) wird keine Zeile angezeigt. Einträge für die gespeicherten Basisprozeduren finden Sie in Sichten, wie z. B. **sys.objects** und **sys.procedures**.  
  
> [!IMPORTANT]  
>  Nummerierte Prozeduren sind als veraltet markiert. Von der Verwendung nummerierter Prozeduren wird abgeraten. Ein DEPRECATION_ANNOUNCEMENT-Ereignis wird ausgelöst, wenn eine Abfrage kompiliert wird, die diese Katalogsicht verwendet.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Die ID des Objekts der gespeicherten Prozedur.|  
|**procedure_number**|**smallint**|Die Nummer dieser Prozedur innerhalb des Objekts, d. h. 2 oder größer.|  
|**Definition**|**nvarchar(max)**|Der SQL Server-Text, mit dem diese Prozedur definiert wird.<br /><br /> NULL = verschlüsselt.|  
  
> [!NOTE]  
>  XML- und CLR-Parameter werden für nummerierte Prozeduren nicht unterstützt.  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten für Objekte &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
