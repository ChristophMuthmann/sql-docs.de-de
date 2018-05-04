---
title: Sys. partition_schemes (Transact-SQL) | Microsoft Docs
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
- partition_schemes_TSQL
- partition_schemes
- sys.partition_schemes_TSQL
- sys.partition_schemes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.partition_schemes catalog view
ms.assetid: ed557fd5-12b0-4cef-9e4f-440b02e99d1f
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 26c40a5f239e1cd52b4ab71410b4d7803e1b8109
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="syspartitionschemes-transact-sql"></a>sys.partition_schemes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Enthält eine Zeile für jeden Datenbereich, bei dem es sich um ein Partitionierungsschema handelt. **Typ** = PS.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**\<geerbte Spalten >**||Erbt Spalten von [Sys. data_spaces &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md).|  
|**function_id**|**int**|ID der Partitionsfunktion, die in dem Schema verwendet wird.|  
  
 Eine Liste der Spalten, die diese Sicht erbt, finden Sie unter [Sys. data_spaces &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle. Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Häufig gestellte Fragen zu Abfragen des SQL Server-Systemkatalogs](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
