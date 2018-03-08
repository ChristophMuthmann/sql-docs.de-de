---
title: sys.registered_search_property_lists (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
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
- registered_search_property_lists_TSQL
- sys.registered_search_property_lists
- registered_search_property_lists
- sys.registered_search_property_lists_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- sys.registered_search_property_lists catalog view
- search property lists [SQL Server], viewing
ms.assetid: 630d4caa-9bea-4cd3-a5b1-01098b0855fc
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 43beb06c378f7c9a829acf6f7d42c5eb25bb2973
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysregisteredsearchpropertylists-transact-sql"></a>sys.registered_search_property_lists (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jede Sucheigenschaftenliste in der aktuellen Datenbank.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**property_list_id**|**int**|Die ID der Eigenschaftenliste.|  
|**name**|**sysname**|Der Name der Eigenschaftenliste.|  
|**create_date**|**datetime**|Datum, an dem die Eigenschaftenliste erstellt wurde.|  
|**modify_date**|**datetime**|Datum, an dem die Eigenschaftenliste zuletzt mithilfe einer beliebigen ALTER-Anweisung geändert wurde.|  
|**principal_id**|**int**|Der Besitzer der Eigenschaftenliste.|  
  
## <a name="remarks"></a>Hinweise  
 Weitere Informationen finden Sie unter [Suchen von Dokumenteigenschaften mithilfe von Sucheigenschaftenlisten](../../relational-databases/search/search-document-properties-with-search-property-lists.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Die Sichtbarkeit der Metadaten für Sucheigenschaftenlisten ist auf solche beschränkt, die Sie besitzen oder für die Sie über eine REFERENCE-Berechtigung verfügen.  
  
> [!NOTE]  
>  REFERENCE- oder CONTROL-Berechtigungen können vom Besitzer einer Sucheigenschaftenliste gewährt werden. Benutzer mit CONTROL-Berechtigung können anderen Benutzern auch eine REFERENCE-Berechtigung erteilen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden die ID und der Name der Sucheigenschaftenlisten in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank angezeigt.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT property_list_id, name FROM sys.registered_search_property_lists;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [sys.fulltext_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)  
  
  
