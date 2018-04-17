---
title: Domänen (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-information-schema-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DOMAINS_TSQL
- DOMAINS
dev_langs:
- TSQL
helpviewer_keywords:
- DOMAINS view
- INFORMATION_SCHEMA.DOMAINS view
ms.assetid: f0b734d5-816f-4b10-a60c-615931b515c2
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a13c0a859b642c272a99b2a935b41933b558578d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="domains-transact-sql"></a>DOMAINS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt eine Zeile für jeden Aliasdatentyp zurück, auf den der aktuelle Benutzer in der aktuellen Datenbank zugreifen kann.  
  
 Geben Sie zum Abrufen von Informationen aus diesen Sichten den vollqualifizierten Namen des **INFORMATION_SCHEMA. *** View_name*.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**DOMAIN_CATALOG**|**Nvarchar (**128**)**|Datenbank, in der der Aliasdatentyp vorhanden ist.|  
|**DOMAIN_SCHEMA**|**Nvarchar (**128**)**|Der Name des Schemas, das den Aliasdatentyp enthält.<br /><br /> **\*\* Wichtige \* \***  verwenden Sie keine INFORMATION_SCHEMA-Sichten, die um das Schema eines Datentyps zu bestimmen. Die einzige zuverlässige Möglichkeit zum Finden des Schemas eines Typs besteht darin, die TYPEPROPERTY-Funktion zu verwenden.|  
|**DOMÄNENNAME**|**sysname**|Aliasdatentyp.|  
|**DATA_TYPE**|**sysname**|Vom System bereitgestellter Datentyp|  
|**CHARACTER_MAXIMUM_LENGTH**|**int**|Maximale Länge (in Zeichen) für binäre Daten, Zeichendaten, Text- und Tmage-Daten<br /><br /> -1 für **Xml** und Typ mit umfangreichen Werten. Andernfalls wird NULL zurückgegeben. Weitere Informationen finden Sie unter [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md).|  
|**CHARACTER_OCTET_LENGTH**|**int**|Maximale Länge (in Bytes) für binäre Daten, Zeichendaten, Text- und Image-Daten.<br /><br /> -1 für **Xml** und Typ mit umfangreichen Werten. Andernfalls wird NULL zurückgegeben.|  
|**COLLATION_CATALOG**|**Varchar (**6**)**|Gibt immer NULL zurück.|  
|**COLLATION_SCHEMA**|**Varchar (**3**)**|Gibt immer NULL zurück.|  
|**SORTIERUNGSNAME**|**Nvarchar (**128**)**|Gibt den eindeutigen Namen für die Sortierreihenfolge zurück, wenn die Spalte Zeichendaten oder **Text** -Datentyp. Andernfalls wird NULL zurückgegeben.|  
|**CHARACTER_SET_CATALOG**|**Varchar (**6**)**|Gibt **master**. Dies gibt an die Datenbank, in dem sich der Zeichensatz befindet, falls die Spalte Zeichendaten oder **Text** -Datentyp. Andernfalls wird NULL zurückgegeben.|  
|**CHARACTER_SET_SCHEMA**|**Varchar (**3**)**|Gibt immer NULL zurück.|  
|**CHARACTER_SET_NAME**|**Nvarchar (**128**)**|Gibt den eindeutigen Namen für den Zeichensatz, falls diese Spalte Zeichendaten oder **Text** -Datentyp. Andernfalls wird NULL zurückgegeben.|  
|**"NUMERIC_PRECISION"**|**tinyint**|Genauigkeit für Spalten mit ungefähren numerischen Daten, exakten numerischen Daten, ganzzahligen Daten oder Währungsdaten. Andernfalls wird NULL zurückgegeben.|  
|**NUMERIC_PRECISION_RADIX**|**smallint**|Basis der Genauigkeit für Spalten mit ungefähren numerischen Daten, exakten numerischen Daten, ganzzahligen Daten oder Währungsdaten. Andernfalls wird NULL zurückgegeben.|  
|**NUMERIC_SCALE**|**tinyint**|Anzahl der Dezimalstellen für Spalten mit ungefähren numerischen Daten, exakten numerischen Daten, ganzzahligen Daten oder Währungsdaten. Andernfalls wird NULL zurückgegeben.|  
|**DATETIME_PRECISION**|**smallint**|Untertypcode für **"DateTime"** und ISO **Intervall** -Datentyp. Für andere Datentypen gibt diese Spalte einen NULL-Wert zurück.|  
|**DOMAIN_DEFAULT**|**Nvarchar (**4000**)**|Tatsächlicher Text der Definition der [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisung.|  
  
## <a name="see-also"></a>Siehe auch  
 [Systemsichten &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Informationsschemasichten &#40;Transact-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [Sys.syscharsets &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syscharsets-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)  
  
  
