---
title: Sys. foreign_key_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.foreign_key_columns
- foreign_key_columns
- sys.foreign_key_columns_TSQL
- foreign_key_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.foreign_key_columns catalog view
ms.assetid: 7247f065-5441-4bcf-9f25-c84a03290dc6
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 73b6c67b2c4d1b709e799a5ad1070391372fea19
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysforeignkeycolumns-transact-sql"></a>sys.foreign_key_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Enthält eine Zeile für jede Spalte oder Spaltengruppe, die einen Fremdschlüssel enthält.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**constraint_object_id**|**int**|ID der FOREIGN KEY-Einschränkung.|  
|**constraint_column_id**|**int**|ID der Spalte oder der Spaltengruppe, die die FOREIGN KEY-Anweisung enthält (*1..n* , wobei n=Anzahl von Spalten).|  
|**"parent_object_id"**|**int**|Die ID des übergeordneten Objekts der Einschränkung, das das verweisende Objekt darstellt.|  
|**parent_column_id**|**int**|Die ID der übergeordneten Spalte, die die verweisende Spalte darstellt.|  
|**referenced_object_id**|**int**|Die ID des Objekts, auf das verwiesen wird und das den Kandidatenschlüssel aufweist.|  
|**referenced_column_id**|**int**|Die ID der Spalte, auf die verwiesen wird (Kandidatenschlüsselspalte).|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten für Objekte &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Häufig gestellte Fragen zu Abfragen des SQL Server-Systemkatalogs](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
