---
title: Parameter (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-information-schema-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- PARAMETERS_TSQL
- PARAMETERS
dev_langs:
- TSQL
helpviewer_keywords:
- PARAMETERS view
- INFORMATION_SCHEMA.PARAMETERS view
ms.assetid: 06ded0ca-7d21-4400-864a-b801e855b257
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 71aaf16dd45c0bc5efb6a2741f554b346abf4905
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="parameters-transact-sql"></a>PARAMETERS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt eine Zeile für jeden Parameter einer benutzerdefinierten Funktion oder gespeicherten Prozedur zurück, auf die der aktuelle Benutzer in der aktuellen Datenbank zugreifen kann. Für Funktionen gibt diese Sicht auch eine Zeile mit Informationen zum Rückgabewert zurück.  
  
 Geben Sie zum Abrufen von Informationen aus diesen Sichten den vollqualifizierten Namen des **INFORMATION_SCHEMA. *** View_name*.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**SPECIFIC_CATALOG**|**Nvarchar (** 128 **)**|Katalogname der Routine, für die dies ein Parameter ist|  
|**SPECIFIC_SCHEMA**|**Nvarchar (** 128 **)**|Schemaname der Routine, für die dies ein Parameter ist<br /><br /> **\*\* Wichtige \* \***  verwenden Sie keine INFORMATION_SCHEMA-Sichten, die um das Schema eines Objekts zu bestimmen. Die einzig zuverlässige Möglichkeit zum Finden des Schemas eines Objekts besteht darin, die sys.objects-Katalogsicht abzufragen.|  
|**"SPECIFIC_NAME"**|**Nvarchar (** 128 **)**|Name der Routine, für die dies ein Parameter ist|  
|**ORDINAL_POSITION**|**int**|Die Ordnungsposition des Parameters, beginnend bei 1. Für den Rückgabewerts einer Funktion ist dies 0.|  
|**PARAMETER_MODE**|**Nvarchar (** 10 **)**|Gibt IN zurück, wenn es ein Eingabeparameter ist, OUT, wenn es ein Ausgabeparameter ist, und INOUT, wenn es ein Eingabe/Ausgabeparameter ist.|  
|**IS_RESULT**|**Nvarchar (** 10 **)**|Gibt YES zurück, wenn das Ergebnis auf einer Routine beruht, die eine Funktion ist. Andernfalls gibt "Nein".|  
|**AS_LOCATOR**|**Nvarchar (** 10 **)**|Gibt YES zurück, wenn der Parameter als Lokator deklariert wurde. Andernfalls gibt "Nein".|  
|**PARAMETERNAME**|**Nvarchar (** 128 **)**|Der Name des Parameters. NULL, wenn er dem Rückgabewert einer Funktion entspricht.|  
|**DATA_TYPE**|**Nvarchar (** 128 **)**|Vom System bereitgestellter Datentyp|  
|**CHARACTER_MAXIMUM_LENGTH**|**int**|Maximale Länge in Zeichen für binary-Datentypen oder Zeichendatentypen<br /><br /> -1 für **Xml** und Typ mit umfangreichen Werten. Andernfalls wird NULL zurückgegeben.|  
|**CHARACTER_OCTET_LENGTH**|**int**|Maximale Länge in Bytes für binary-Datentypen oder Zeichendatentypen<br /><br /> -1 für **Xml** und Typ mit umfangreichen Werten. Andernfalls wird NULL zurückgegeben.|  
|**COLLATION_CATALOG**|**Nvarchar (** 128 **)**|Gibt immer NULL zurück.|  
|**COLLATION_SCHEMA**|**Nvarchar (** 128 **)**|Gibt immer NULL zurück.|  
|**SORTIERUNGSNAME**|**Nvarchar (** 128 **)**|Name der Sortierung des Parameters. Wenn es sich nicht um einen der Zeichentypen handelt, wird NULL zurückgegeben.|  
|**CHARACTER_SET_CATALOG**|**Nvarchar (** 128 **)**|Katalogname des Zeichensatzes des Parameters. Wenn es sich nicht um einen der Zeichentypen handelt, wird NULL zurückgegeben.|  
|**CHARACTER_SET_SCHEMA**|**Nvarchar (** 128 **)**|Gibt immer NULL zurück.|  
|**CHARACTER_SET_NAME**|**Nvarchar (** 128 **)**|Name des Zeichensatzes des Parameters. Wenn es sich nicht um einen der Zeichentypen handelt, wird NULL zurückgegeben.|  
|**"NUMERIC_PRECISION"**|**tinyint**|Genauigkeit für Spalten mit ungefähren numerischen Daten, exakten numerischen Daten, ganzzahligen Daten oder Währungsdaten. Andernfalls wird NULL zurückgegeben.|  
|**NUMERIC_PRECISION_RADIX**|**smallint**|Basis der Genauigkeit für Spalten mit ungefähren numerischen Daten, exakten numerischen Daten, ganzzahligen Daten oder Währungsdaten. Andernfalls wird NULL zurückgegeben.|  
|**NUMERIC_SCALE**|**tinyint**|Anzahl der Dezimalstellen für Spalten mit ungefähren numerischen Daten, exakten numerischen Daten, ganzzahligen Daten oder Währungsdaten. Andernfalls wird NULL zurückgegeben.|  
|**DATETIME_PRECISION**|**smallint**|Genauigkeit in Bruchteilen von Sekunden, wenn der Parametertyp ist **"DateTime"** oder **Smalldatetime**. Andernfalls wird NULL zurückgegeben.|  
|**INTERVAL_TYPE**|**Nvarchar (** 30 **)**|NULL. Zur künftigen Verwendung reserviert.|  
|**INTERVAL_PRECISION**|**smallint**|NULL. Zur künftigen Verwendung reserviert.|  
|**USER_DEFINED_TYPE_CATALOG**|**Nvarchar (** 128 **)**|NULL. Zur künftigen Verwendung reserviert.|  
|**USER_DEFINED_TYPE_SCHEMA**|**Nvarchar (** 128 **)**|NULL. Zur künftigen Verwendung reserviert.|  
|**USER_DEFINED_TYPE_NAME**|**Nvarchar (** 128 **)**|NULL. Zur künftigen Verwendung reserviert.|  
|**SCOPE_CATALOG**|**Nvarchar (** 128 **)**|NULL. Zur künftigen Verwendung reserviert.|  
|**SCOPE_SCHEMA**|**Nvarchar (** 128 **)**|NULL. Zur künftigen Verwendung reserviert.|  
|**SCOPE_NAME**|**Nvarchar (** 128 **)**|NULL. Zur künftigen Verwendung reserviert.|  
  
## <a name="see-also"></a>Siehe auch  
 [Systemsichten &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Informationsschemasichten &#40;Transact-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [Sys.Parameters & #40; Transact-SQL & #41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)  
  
  
