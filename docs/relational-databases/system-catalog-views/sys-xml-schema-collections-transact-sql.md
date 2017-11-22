---
title: Sys. xml_schema_collections (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_collections_TSQL
- sys.xml_schema_collections
- xml_schema_collections
- xml_schema_collections_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.xml_schema_collections catalog view
ms.assetid: f3f7f3dc-029f-4942-ab3c-75fa9814e40f
caps.latest.revision: "34"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 06c59000c8430a80604785c277dd3a6d3d3b0699
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysxmlschemacollections-transact-sql"></a>sys.xml_schema_collections (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt eine Zeile pro XML-Schemaauflistung zurück. Eine XML-Schemaauflistung ist eine benannte Menge von XSD-Definitionen. Die XML-Schemaauflistung selbst ist in einem relationalen Schema enthalten und wird durch einen [!INCLUDE[tsql](../../includes/tsql-md.md)]-Namen mit Schemabereich identifiziert. Die folgenden Tupel sind eindeutig: xml_collection_id, schema_id und name.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|xml_collection_id|**int**|ID der XML-Schemaauflistung. Ist innerhalb der Datenbank eindeutig.|  
|schema_id|**int**|ID des relationalen Schemas, das diese XML-Schemaauflistung enthält.|  
|principal_id|**int**|ID des einzelnen Besitzers, falls dieser nicht mit dem Schemabesitzer identisch ist. Standardmäßig gehören Objekte mit Schemabereich dem Schemabesitzer. Es kann jedoch ein alternativer Besitzer mithilfe der ALTER AUTHORIZATION-Anweisung angegeben werden, um den Besitzer zu ändern.<br /><br /> NULL = Kein alternativer einzelner Besitzer.|  
|name|**sysname**|Name der XML-Schemaauflistung.|  
|create_date|**datetime**|Datum, an dem die XML-Schemaauflistung erstellt wurde.|  
|modify_date|**datetime**|Datum, an dem die XML-Schemaauflistung zuletzt geändert wurde.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML-Schemas &#40; XML-Typsystem &#41; Katalogsichten &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)   
 [Häufig gestellte Fragen zu Abfragen des SQL Server-Systemkatalogs](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
