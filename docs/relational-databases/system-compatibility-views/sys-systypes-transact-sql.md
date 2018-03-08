---
title: Sys.systypes (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-compatibility-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.systypes_TSQL
- systypes_TSQL
- sys.systypes
- systypes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.systypes compatibility view
- systypes system table
ms.assetid: 1b0b1d0c-5f7b-470b-bd52-8bfa922d7889
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: aa54909c2d3f5e83a51ef1814564ae80828a292a
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="syssystypes-transact-sql"></a>sys.systypes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt eine Zeile für jeden vom System bereitgestellten und jeden benutzerdefinierten Datentyp zurück, der in der Datenbank definiert ist.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Name des Datentyps.|  
|**xtype**|**tinyint**|Physischer Speichertyp.|  
|**status**|**tinyint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xusertype**|**smallint**|Erweiterter Benutzertyp. Führt zu einem Überlauf oder gibt NULL zurück, wenn die Anzahl der Datentypen 32.767 übersteigt.|  
|**length**|**smallint**|Physische Länge des Datentyps.|  
|**xprec**|**tinyint**|Vom Server verwendete interne Genauigkeit. Darf in Abfragen nicht verwendet werden.|  
|**xscale**|**tinyint**|Vom Server verwendete interne Dezimalstellen. Darf in Abfragen nicht verwendet werden.|  
|**tdefault**|**int**|ID der gespeicherten Prozedur zur Integritätsprüfung für diesen Datentyp.|  
|**domain**|**int**|ID der gespeicherten Prozedur zur Integritätsprüfung für diesen Datentyp.|  
|**uid**|**smallint**|Schema-ID des Typbesitzers.<br /><br /> Bei Datenbanken, die von einer früheren Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aktualisiert wurden, ist die Schema-ID gleich der Benutzer-ID des Besitzers.<br /><br /> **\*\*Wichtige \* \***  bei Verwendung von keines der folgenden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DDL-Anweisungen, verwenden Sie die [sys.types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md) -Katalogsicht anstelle von **sys.systypes**.<br /><br /> ALTER AUTHORIZATION ON TYPE<br /><br /> CREATE TYPE<br /><br /> Führt zu einem Überlauf oder gibt NULL zurück, wenn die Anzahl von Benutzern und Rollen 32.767 übersteigt.|  
|**reserved**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**collationid**|**int**|Falls zeichenbasiert, **Collationid** ist die Id der Sortierung der aktuellen Datenbank; andernfalls ist NULL.|  
|**usertype**|**smallint**|User type ID. Führt zu einem Überlauf oder gibt NULL zurück, wenn die Anzahl der Datentypen 32.767 übersteigt.|  
|**variable**|**bit**|Datentyp mit variabler Länge.<br /><br /> 1 = True<br /><br /> 0 = False|  
|**allownulls**|**bit**|Zeigt die Standard-NULL-Zulässigkeit für diesen Datentyp an. Dieser Standardwert wird überschrieben, wenn es sich bei NULL-Zulässigkeit mithilfe des Parameters [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) oder [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md).|  
|**type**|**tinyint**|Physischer Speicherdatentyp.|  
|**printfmt**|**varchar(255)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**prec**|**smallint**|Genauigkeitsgrad für diesen Datentyp.<br /><br /> -1 = **Xml** oder große Werttypen.|  
|**scale**|**tinyint**|Dezimalstellen für diesen Datentyp (basierend auf der Genauigkeit).<br /><br /> NULL = Datentyp nicht numerisch.|  
|**collation**|**sysname**|Falls zeichenbasiert, **Sortierung** wird bei der Sortierung der aktuellen Datenbank; andernfalls ist NULL.|  
  
## <a name="see-also"></a>Siehe auch  
 [Kompatibilitätssichten &#40; Transact-SQL &#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)   
 [Zuordnen von Systemtabellen zu Systemsichten &#40; Transact-SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)  
  
  
