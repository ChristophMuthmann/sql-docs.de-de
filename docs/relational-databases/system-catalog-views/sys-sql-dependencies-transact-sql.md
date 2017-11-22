---
title: Sys. sql_dependencies (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sql_dependencies
- sql_dependencies_TSQL
- sys.sql_dependencies_TSQL
- sys.sql_dependencies
dev_langs: TSQL
helpviewer_keywords: sys.sql_dependencies catalog view
ms.assetid: 1779aa87-a0b8-470a-a286-d7cc0b93ad2e
caps.latest.revision: "31"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ae071c927ab60f5b93e69a43d7ad443d333aa856
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="syssqldependencies-transact-sql"></a>sys.sql_dependencies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jede Abhängigkeit einer Entität, auf die im [!INCLUDE[tsql](../../includes/tsql-md.md)]-Ausdruck oder in Anweisungen verwiesen wird, die ein anderes verweisendes Objekt definieren.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Verwendung [Sys. sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) stattdessen.  

  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**Klasse**|**tinyint**|Identifiziert die Klasse der Entität, auf die verwiesen wird:<br /><br /> 0 = Objekt oder Spalte (nur nicht schemagebundene Verweise)<br /><br /> 1 = Objekt oder Spalte (schemagebundene Verweise)<br /><br /> 2 = Typen (schemagebundene Verweise)<br /><br /> 3 = XML-Schemaauflistungen (schemagebundene Verweise)<br /><br /> 4 = Partitionsfunktion (schemagebundene Verweise)|  
|**class_desc**|**nvarchar(60)**|Klassenbeschreibung der Entität, auf die verwiesen wird:<br /><br /> **OBJECT_OR_COLUMN_REFERENCE_NON_SCHEMA_BOUND**<br /><br /> **OBJECT_OR_COLUMN_REFERENCE_SCHEMA_BOUND**<br /><br /> **TYPE_REFERENCE**<br /><br /> **XML_SCHEMA_COLLECTION_REFERENCE**<br /><br /> **PARTITION_FUNCTION_REFERENCE**|  
|**object_id**|**int**|ID des verweisenden Objekts.|  
|**column_id**|**int**|Falls die verweisende ID eine Spalte angibt, ist dies die ID der verweisenden Spalte. Andernfalls ist der Wert 0.|  
|**referenced_major_id**|**int**|ID der Entität, auf die verwiesen wird. Die ID wird nach dem Wert der Klasse interpretiert, wobei Folgendes gilt:<br /><br /> 0, 1 = Objekt-ID des Objekts oder der Spalte.<br /><br /> 2 = Typ-ID.<br /><br /> 3 = XML-Schemaauflistungs-ID.|  
|**referenced_minor_id**|**int**|Sekundäre ID der Entität, auf die verwiesen wird. Die ID wird nach dem Wert der Klasse interpretiert, wobei Folgendes gilt:<br /><br /> Wenn class =:<br /><br /> 0 (null) **Referenced_minor_id** ist eine Spalten-ID, oder wenn nicht um eine Spalte, ist der Wert 0.<br /><br /> 1, **Referenced_minor_id** ist eine Spalten-ID, oder wenn nicht um eine Spalte, ist der Wert 0.<br /><br /> Andernfalls **Referenced_minor_id** = 0.|  
|**is_selected**|**bit**|Objekt oder Spalte ist ausgewählt.|  
|**"is_updated"**|**bit**|Objekt oder Spalte ist aktualisiert.|  
|**is_select_all**|**bit**|Objekt wird in SELECT *-Klausel verwendet (nur auf Objektebene).|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle. Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Katalogsichten für Objekte &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Häufig gestellte Fragen zu Abfragen des SQL Server-Systemkatalogs](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
