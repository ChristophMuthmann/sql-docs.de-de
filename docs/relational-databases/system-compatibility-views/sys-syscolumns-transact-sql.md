---
title: Sys.syscolumns (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-enginel, sql-data-warehouse, pdw
ms.service: 
ms.component: system-compatibility-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.syscolumns
- sys.syscolumns_TSQL
- syscolumns_TSQL
- syscolumns
dev_langs: TSQL
helpviewer_keywords:
- syscolumns system table
- sys.syscolumns compatibility view
ms.assetid: 863fd87b-ff33-4ac5-9aa9-df21140681da
caps.latest.revision: "32"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 94f43de0bf804d366b599c053d8dddadf51d809f
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="syssyscolumns-transact-sql"></a>sys.syscolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Gibt jeweils eine Zeile für die einzelnen Spalten aller Tabellen und Sichten sowie eine Zeile für jeden Parameter einer gespeicherten Prozedur in der Datenbank zurück.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Name der Spalte oder des Prozedurparameters|  
|**id**|**int**|Objekt-ID der Tabelle, zu der diese Spalte gehört, oder ID der gespeicherten Prozedur, der dieser Parameter zugeordnet ist|  
|**xTyp gleich**|**tinyint**|Physischer Speichertyp aus **sys.types**|  
|**typestat**|**tinyint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xusertype**|**smallint**|ID des erweiterten benutzerdefinierten Datentyps. Führt zu einem Überlauf oder gibt NULL zurück, wenn die Anzahl der Datentypen 32.767 übersteigt.|  
|**Länge**|**smallint**|Maximale physische Speicherlänge aus **sys**.**types**.|  
|**xprec**|**tinyint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**XScale**|**tinyint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**Spalten-ID**|**smallint**|Spalten- oder Parameter-ID|  
|**XOffset**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**bitpos**|**tinyint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**reserviert**|**tinyint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**colstat**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**cdefault**|**int**|ID des Standards für diese Spalte|  
|**Domäne**|**int**|ID der Regel oder CHECK-Einschränkung für diese Spalte|  
|**Anzahl**|**smallint**|Nummer der Unterprozedur, wenn die Prozedur gruppiert ist.<br /><br /> 0 = Einträge, die sich nicht auf eine Prozedur beziehen.|  
|**colorder**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**autoval**|**varbinary(8000)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**Offset**|**smallint**|Offset in die Zeile, in der diese Spalte enthalten ist|  
|**collationid**|**int**|ID der Sortierung der Spalte. NULL für nicht zeichenbasierte Spalten.|  
|**status**|**tinyint**|Bitmuster, das zum Beschreiben einer Eigenschaft der Spalte oder des Parameters verwendet wird:<br /><br /> 0x08 = In der Spalte sind NULL-Werte zulässig.<br /><br /> 0x10 = ANSI-Auffüllung war aktiviert, als **varchar** oder **varbinary** -Spalten hinzugefügt wurden. Nachfolgende Leerzeichen werden bei **varchar** -Spalten beibehalten, nachfolgende Nullen werden bei **varbinary** -Spalten beibehalten.<br /><br /> 0x40 = Der Parameter ist ein OUTPUT-Parameter.<br /><br /> 0x80 = Die Spalte ist eine Identitätsspalte.|  
|**Typ**|**tinyint**|Physischer Speichertyp aus **sys**.**types**.|  
|**Benutzertyp**|**smallint**|ID des benutzerdefinierten Datentyps aus **sys.types**. Führt zu einem Überlauf oder gibt NULL zurück, wenn die Anzahl der Datentypen 32.767 übersteigt.|  
|**printfmt**|**varchar(255)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**prec**|**smallint**|Genauigkeitsgrad für diese Spalte.<br /><br /> -1 = **xml** oder ein Typ für hohe Werte.|  
|**Skalierung**|**int**|Dezimalstellen in dieser Spalte.<br /><br /> NULL = Datentyp nicht numerisch.|  
|**ist berechnet**|**int**|Flag, das anzeigt, ob die Spalte berechnet ist:<br /><br /> 0 = Nicht berechnet<br /><br /> 1 = Berechnet|  
|**isoutparam**|**int**|Gibt an, ob der Prozedurparameter ein Ausgabeparameter ist.<br /><br /> 1 = True<br /><br /> 0 = False|  
|**IsNullable**|**int**|Gibt an, ob die Spalte NULL-Werte zulässt.<br /><br /> 1 = True<br /><br /> 0 = False|  
|**Sortierung**|**sysname**|Name der Sortierung der Spalte. NULL, wenn es keine zeichenbasierte Spalte ist.|  
  
## <a name="see-also"></a>Siehe auch  
 [Zuordnen von Systemtabellen zu Systemsichten &#40; Transact-SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Kompatibilitätssichten &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
