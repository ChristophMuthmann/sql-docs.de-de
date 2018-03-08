---
title: Sys.sysconstraints (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-compatibility-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysconstraints
- sys.sysconstraints
- sysconstraints_TSQL
- sys.sysconstraints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysconstraints compatibility view
- sysconstraints system table
ms.assetid: f2b2e2ad-ba24-48a1-913c-8ee4e0895dc4
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c2fd5089c30f3a9dffa293293b5d83df97ec7fb0
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="syssysconstraints-transact-sql"></a>sys.sysconstraints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Enthält Zuordnungen von Einschränkungen zu den Objekten, die diese Einschränkungen in der Datenbank besitzen.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**constid**|**int**|Nummer der Einschränkung.|  
|**id**|**int**|ID der Tabelle, die die Einschränkung besitzt.|  
|**colid**|**smallint**|ID der Spalte, für die die Einschränkung definiert ist.<br /><br /> 0 = Tabelleneinschränkung|  
|**spare1**|**tinyint**|Reserviert.|  
|**status**|**int**|Pseudobitmaske zur Anzeige des Status. Folgende Werte sind möglich:<br /><br /> 1 = PRIMARY KEY-Einschränkung<br /><br /> 2 = UNIQUE KEY-Einschränkung<br /><br /> 3 = FOREIGN KEY-Einschränkung<br /><br /> 4 = CHECK-Einschränkung<br /><br /> 5 = DEFAULT-Einschränkung<br /><br /> 16 = Einschränkung auf Spaltenebene<br /><br /> 32 = Einschränkung auf Tabellenebene|  
|**actions**|**int**|Reserviert.|  
|**error**|**int**|Reserviert.|  
  
## <a name="see-also"></a>Siehe auch  
 [Zuordnen von Systemtabellen zu Systemsichten &#40; Transact-SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Kompatibilitätssichten &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
