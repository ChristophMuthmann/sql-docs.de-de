---
title: ROUTINEN (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-information-schema-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ROUTINES_TSQL
- ROUTINES
dev_langs: TSQL
helpviewer_keywords:
- ROUTINES view
- INFORMATION_SCHEMA.ROUTINES view
ms.assetid: c75561b2-c9a1-48a1-9afa-a5896b6454cf
caps.latest.revision: "50"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 159bcda90286cfe2582cd88f41c39e682bf2097e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="routines-transact-sql"></a>ROUTINES (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt eine Zeile für jede gespeicherte Prozedur und Funktion zurück, auf die der aktuelle Benutzer in der aktuellen Datenbank zugreifen kann. Die Spalten, die den Rückgabewert beschreiben, sind nur auf Funktionen anwendbar. Für gespeicherte Prozeduren sind diese Spalten NULL.  
  
 Geben Sie zum Abrufen von Informationen aus diesen Sichten den vollqualifizierten Namen von INFORMATION_SCHEMA. *View_name*.  
  
> [!NOTE]  
>  Die ROUTINE_DEFINITION-Spalte enthält die quellanweisungen, die erstellt die Funktion oder gespeicherten Prozedur. Diese Quellanweisungen enthalten wahrscheinlich eingebettete Wagenrücklaufzeichen. Wenn Sie diese Spalte an eine Anwendung, die die Ergebnisse in einem Textformat anzeigt zurückgeben, können die eingebetteten Wagenrücklaufzeichen in den Ergebnissen ROUTINE_DEFINITION beeinflussen die Formatierung des gesamten Resultsets. Wenn Sie die ROUTINE_DEFINITION Spalte auswählen, müssen Sie die eingebetteten Wagenrücklaufzeichen anpassen; z. B. durch das Zurückgeben der Resultsets in einem Raster oder ROUTINE_DEFINITION in ein eigenes Textfeld zurückgeben.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|SPECIFIC_CATALOG|**Nvarchar (**128**)**|Spezifischer Name des Katalogs. Dieser Name ist derselbe wie für ROUTINE_CATALOG.|  
|SPECIFIC_SCHEMA|**Nvarchar (**128**)**|Spezifischer Name des Schemas.<br /><br /> **\*\*Wichtige \* \***  verwenden Sie keine INFORMATION_SCHEMA-Sichten, die um das Schema eines Objekts zu bestimmen. Die einzig zuverlässige Möglichkeit zum Finden des Schemas eines Objekts besteht darin, die sys.objects-Katalogsicht abzufragen.|  
|SPECIFIC_NAME|**Nvarchar (**128**)**|Spezifischer Name des Katalogs. Dieser Name ist derselbe wie für ROUTINE_NAME.|  
|ROUTINE_CATALOG|**Nvarchar (**128**)**|Katalogname der Funktion.|  
|ROUTINE_SCHEMA|**Nvarchar (**128**)**|Name des Schemas, das diese Funktion enthält.<br /><br /> **\*\*Wichtige \* \***  verwenden Sie keine INFORMATION_SCHEMA-Sichten, die um das Schema eines Objekts zu bestimmen. Die einzig zuverlässige Möglichkeit zum Finden des Schemas eines Objekts besteht darin, die sys.objects-Katalogsicht abzufragen.|  
|ROUTINE_NAME|**Nvarchar (**128**)**|Name der Funktion.|  
|ROUTINE_TYPE|**Nvarchar (**20**)**|Gibt PROCEDURE für gespeicherte Prozeduren und FUNCTION für Funktionen zurück.|  
|MODULE_CATALOG|**Nvarchar (**128**)**|NULL. Zur künftigen Verwendung reserviert.|  
|MODULE_SCHEMA|**Nvarchar (**128**)**|NULL. Zur künftigen Verwendung reserviert.|  
|MODULE_NAME|**Nvarchar (**128**)**|NULL. Zur künftigen Verwendung reserviert.|  
|UDT_CATALOG|**Nvarchar (**128**)**|NULL. Zur künftigen Verwendung reserviert.|  
|UDT_SCHEMA|**Nvarchar (**128**)**|NULL. Zur künftigen Verwendung reserviert.|  
|UDT_NAME|**Nvarchar (**128**)**|NULL. Zur künftigen Verwendung reserviert.|  
|DATA_TYPE|**Nvarchar (**128**)**|Datentyp des Rückgabewerts der Funktion. Gibt **Tabelle** Wenn eine Funktion mit Tabellenrückgabe.|  
|CHARACTER_MAXIMUM_LENGTH|**int**|Maximale Länge in Zeichen, wenn der Rückgabetyp ein Zeichentyp ist.<br /><br /> -1 für **Xml** und Typ mit umfangreichen Werten.|  
|CHARACTER_OCTET_LENGTH|**int**|Maximale Länge in Bytes, wenn der Rückgabetyp ein Zeichentyp ist.<br /><br /> -1 für **Xml** und Typ mit umfangreichen Werten.|  
|COLLATION_CATALOG|**Nvarchar (**128**)**|Gibt immer NULL zurück.|  
|COLLATION_SCHEMA|**Nvarchar (**128**)**|Gibt immer NULL zurück.|  
|COLLATION_NAME|**Nvarchar (**128**)**|Sortierungsname des Rückgabewerts. Für Nicht-Zeichentypen wird NULL zurückgegeben.|  
|CHARACTER_SET_CATALOG|**Nvarchar (**128**)**|Gibt immer NULL zurück.|  
|CHARACTER_SET_SCHEMA|**Nvarchar (**128**)**|Gibt immer NULL zurück.|  
|CHARACTER_SET_NAME|**Nvarchar (**128**)**|Name des Zeichensatzes des Rückgabewerts. Für Nicht-Zeichentypen wird NULL zurückgegeben.|  
|NUMERIC_PRECISION|**smallint**|Numerische Genauigkeit des Rückgabewerts. Für nicht-numerische Typen wird NULL zurückgegeben.|  
|NUMERIC_PRECISION_RADIX|**smallint**|Numerische Basis der Genauigkeit des Rückgabewerts. Für nicht-numerische Typen wird NULL zurückgegeben.|  
|NUMERIC_SCALE|**smallint**|Dezimalstellen des Rückgabewerts. Für nicht-numerische Typen wird NULL zurückgegeben.|  
|DATETIME_PRECISION|**smallint**|Fraktionale Genauigkeit von einer Sekunde, wenn der Rückgabewert vom Typ **"DateTime"**. Andernfalls wird NULL zurückgegeben.|  
|INTERVAL_TYPE|**Nvarchar (**30**)**|NULL. Zur künftigen Verwendung reserviert.|  
|INTERVAL_PRECISION|**smallint**|NULL. Zur künftigen Verwendung reserviert.|  
|TYPE_UDT_CATALOG|**Nvarchar (**128**)**|NULL. Zur künftigen Verwendung reserviert.|  
|TYPE_UDT_SCHEMA|**Nvarchar (**128**)**|NULL. Zur künftigen Verwendung reserviert.|  
|TYPE_UDT_NAME|**Nvarchar (**128**)**|NULL. Zur künftigen Verwendung reserviert.|  
|SCOPE_CATALOG|**Nvarchar (**128**)**|NULL. Zur künftigen Verwendung reserviert.|  
|SCOPE_SCHEMA|**Nvarchar (**128**)**|NULL. Zur künftigen Verwendung reserviert.|  
|SCOPE_NAME|**Nvarchar (**128**)**|NULL. Zur künftigen Verwendung reserviert.|  
|MAXIMUM_CARDINALITY|**bigint**|NULL. Zur künftigen Verwendung reserviert.|  
|DTD_IDENTIFIER|**Nvarchar (**128**)**|NULL. Zur künftigen Verwendung reserviert.|  
|ROUTINE_BODY|**Nvarchar (**30**)**|Gibt SQL für eine [!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktion und EXTERNAL für eine extern geschriebene Funktion zurück.<br /><br /> Funktionen sind immer SQL.|  
|ROUTINE_DEFINITION|**Nvarchar (**4000**)**|Gibt die ersten 4000 Zeichen des Definitionstexts der Funktion oder gespeicherten Prozedur zurück, wenn die Funktion oder gespeicherte Prozedur nicht verschlüsselt ist. Andernfalls wird NULL zurückgegeben.<br /><br /> Um sicherzustellen, dass Sie die vollständige Definition erhalten, Fragen Sie die [OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md) -Funktion oder der Definition-Spalte in der [sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) -Katalogsicht angezeigt.|  
|EXTERNAL_NAME|**Nvarchar (**128**)**|NULL. Zur künftigen Verwendung reserviert.|  
|EXTERNAL_LANGUAGE|**Nvarchar (**30**)**|NULL. Zur künftigen Verwendung reserviert.|  
|PARAMETER_STYLE|**Nvarchar (**30**)**|NULL. Zur künftigen Verwendung reserviert.|  
|IS_DETERMINISTIC|**Nvarchar (**10**)**|Gibt YES zurück, wenn die Routine deterministisch ist.<br /><br /> Gibt NO zurück, wenn die Routine nicht deterministisch ist.<br /><br /> Für gespeicherte Prozeduren wird immer NO zurückgegeben.|  
|SQL_DATA_ACCESS|**Nvarchar (**30**)**|Gibt einen der folgenden Werte zurück:<br /><br /> NONE = Die Funktion enthält keine SQL-Anweisungen.<br /><br /> CONTAINS = Die Funktion enthält möglicherweise SQL-Anweisungen.<br /><br /> READS = Die Funktion liest möglicherweise SQL-Daten.<br /><br /> MODIFIES = Die Funktion ändert möglicherweise SQL-Daten.<br /><br /> Gibt für alle Funktionen READS und für alle gespeicherten Prozeduren MODIFIES zurück.|  
|IS_NULL_CALL|**Nvarchar (**10**)**|Zeigt an, ob die Routine aufgerufen wird, wenn eines der Argumente NULL ist.|  
|SQL_PATH|**Nvarchar (**128**)**|NULL. Zur künftigen Verwendung reserviert.|  
|SCHEMA_LEVEL_ROUTINE|**Nvarchar (**10**)**|Gibt YES zurück, wenn es sich um eine Funktion auf Schemaebene handelt, oder NO, wenn es keine Funktion auf Schemaebene ist.<br /><br /> Es wird immer YES zurückgegeben.|  
|MAX_DYNAMIC_RESULT_SETS|**smallint**|Maximale Anzahl der dynamischen Resultsets, die durch die Routine zurückgegeben werden.<br /><br /> Gibt bei Funktionen 0 zurück.|  
|IS_USER_DEFINED_CAST|**Nvarchar (**10**)**|Gibt YES zurück, wenn es sich um eine benutzerdefinierte Typumwandlungsfunktion handelt, oder NO, wenn es keine benutzerdefinierte Typumwandlungsfunktion ist.<br /><br /> Es wird immer NO zurückgegeben.|  
|IS_IMPLICITLY_INVOCABLE|**Nvarchar (**10**)**|Gibt YES zurück, wenn die Routine implizit aufgerufen werden kann, und NO, wenn die Funktion nicht implizit aufgerufen werden kann.<br /><br /> Es wird immer NO zurückgegeben.|  
|CREATED|**datetime**|Zeitpunkt, zu dem die Routine erstellt wurde.|  
|LAST_ALTERED|**datetime**|Zeitpunkt der letzten Änderung der Funktion.|  
  
## <a name="see-also"></a>Siehe auch  
 [Systemsichten &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Informationsschemasichten &#40; Transact-SQL &#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [Sys.Objects &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.procedures &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-procedures-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)  
  
  
