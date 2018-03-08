---
title: Sys.syscharsets (Transact-SQL) | Microsoft Docs
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
- sys.syscharsets
- syscharsets
- sys.syscharsets_TSQL
- syscharsets_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syscharsets system table
- sys.syscharsets compatibility view
ms.assetid: f16d987c-bd19-4668-9ef7-785b8fb9ff5b
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b0f88ab4d96160dc9b466379ec525c7858a579f1
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="syssyscharsets-transact-sql"></a>sys.syscharsets (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Enthält eine Zeile für jeden Zeichensatz und Sortierreihenfolge definiert, die für die Verwendung durch die [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Eine der Sortierreihenfolgen ist in **sysconfigures** als Standard-Sortierreihenfolge markiert. Dies ist die einzige Sortierreihenfolge, die tatsächlich verwendet wird.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**type**|**smallint**|Typ der Entität, die diese Zeile darstellt:<br /><br /> 1001 = Zeichensatz<br /><br /> 2001 = Sortierreihenfolge|  
|**id**|**tinyint**|Eindeutige ID für den Zeichensatz oder die Sortierreihenfolge. Beachten Sie, dass Sortierreihenfolgen und Zeichensätze nicht dieselbe ID haben können. Der ID-Bereich von 1 bis 240 ist für die Verwendung in [!INCLUDE[ssDE](../../includes/ssde-md.md)] reserviert.|  
|**csid**|**tinyint**|Wenn die Zeile einen Zeichensatz darstellt, ist dieses Feld ungenutzt. Wenn die Zeile eine Sortierreihenfolge darstellt, ist dieses Feld die ID des Zeichensatzes, auf dem die Sortierreihenfolge aufgebaut ist. Es wird davon ausgegangen, dass eine Zeichensatzzeile mit dieser ID in dieser Tabelle vorhanden ist.|  
|**status**|**smallint**|Bits für Informationen über den internen Systemstatus.|  
|**name**|**sysname**|Eindeutiger Name für den Zeichensatz oder die Sortierreihenfolge. Dieses Feld darf nur die Buchstaben A-Z oder a-z, die Zahlen 0-9 und Unterstriche (_) enthalten; es muss außerdem mit einem Buchstaben beginnen.|  
|**description**|**nvarchar(255)**|Optionale Beschreibung der Funktionen des Zeichensatzes oder der Sortierreihenfolge.|  
|**binarydefinition**|**varbinary(6000)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**definition**|**image**|Interne Definition des Zeichensatzes oder der Sortierreihenfolge. Die Struktur der Daten in diesem Feld hängt vom Typ ab.|  
  
## <a name="see-also"></a>Siehe auch  
 [Zuordnen von Systemtabellen zu Systemsichten &#40; Transact-SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Kompatibilitätssichten &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
