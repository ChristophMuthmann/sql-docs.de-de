---
title: Sys. xml_indexes (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- sys.xml_indexes_TSQL
- xml_indexes_TSQL
- sys.xml_indexes
- xml_indexes
dev_langs: TSQL
helpviewer_keywords: sys.xml_indexes catalog view
ms.assetid: 3408de72-b067-4fda-b5d5-8e856dfd9db3
caps.latest.revision: "34"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 23c5fc72f377b08e77b8b2c8167919bcbc707ec3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sysxmlindexes-transact-sql"></a>sys.xml_indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Zeile pro XML-Index zurück.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].|  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**\<geerbte Spalten >**||Erbt Spalten von [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).|  
|**using_xml_index_id**|**int**|NULL = Primärer XML-Index.<br /><br /> Nonnull = Sekundärer XML-Index.<br /><br /> Nonnull ist ein Selbstjoinhinweis auf den primären XML-Index.|  
|**secondary_type**|**char(1)**|Typbeschreibung des sekundären Indexes:<br /><br /> P = sekundärer XML-Index vom Typ PATH<br /><br /> V = sekundärer XML-Index vom Typ VALUE<br /><br /> R = sekundärer XML-Index vom Typ PROPERTY<br /><br /> NULL = Primärer XML-Index|  
|**secondary_type_desc**|**nvarchar(60)**|Typbeschreibung des sekundären Indexes:<br /><br /> PATH = sekundärer XML-Index vom Typ PATH<br /><br /> VALUE = sekundärer XML-Index vom Typ VALUE<br /><br /> PROPERTY = sekundäre XML-Indizes vom Typ PROPERTY<br /><br /> NULL = Primärer XML-Index|  
|**xml_index_type**|**tinyint**|Indextyp:<br /><br /> 0 = Primärer XML-Index<br /><br /> 1 = Sekundärer XML-Index<br /><br /> 2 = Selektiver XML-Index<br /><br /> 3 = Sekundärer, selektiver XML-Index|  
|**xml_index_type_description**|**nvarchar(60)**|Beschreibung des Typs des Index:<br /><br /> PRIMARY_XML<br /><br /> Sekundärer XML-Index<br /><br /> Selektiver XML-Index<br /><br /> Sekundärer, selektiver XML-Index|  
|**path_id**|**int**|NULL für alle XML-Indizes, mit Ausnahme sekundärer, selektiver XML-Indizes.<br /><br /> Andernfalls die ID des höher gestuften Pfads, über den der sekundäre, selektive XML-Index erstellt wird. Dieser Wert entspricht dem Wert von Dieser Wert entspricht dem Wert von path_idpath_id aus der sys.selective_xml_index_paths-Systemsicht.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Katalogsichten für Objekte &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  
  
  
