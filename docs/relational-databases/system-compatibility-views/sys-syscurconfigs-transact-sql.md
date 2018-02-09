---
title: Sys.syscurconfigs (Transact-SQL) | Microsoft Docs
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
- sys.syscurconfigs
- sys.syscurconfigs_TSQL
- syscurconfigs
- syscurconfigs_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.syscurconfigs compatibility view
- syscurconfigs system table
ms.assetid: 454ab849-07a5-4b50-ba0a-6b1b14721f77
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 930bf46731bb657076a6cc2e2dd3420594d293a2
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="syssyscurconfigs-transact-sql"></a>sys.syscurconfigs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält einen Eintrag für jede aktuelle Konfigurationsoption. Außerdem enthält diese Sicht vier Einträge, die die Konfigurationsstruktur beschreiben. **Syscurconfigs** wird dynamisch erstellt, wenn von einem Benutzer abgefragt. Weitere Informationen finden Sie unter [sys.sysconfigures &#40; Transact-SQL &#41; ](../../relational-databases/system-compatibility-views/sys-sysconfigures-transact-sql.md).  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**value**|**int**|Vom Benutzer änderbarer Wert für die Variable. Dies dient der [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] nur, wenn RECONFIGURE ausgeführt wurde.|  
|**config**|**smallint**|Nummer der Konfigurationsvariablen.|  
|**comment**|**nvarchar(255)**|Erläuterung der Konfigurationsoption.|  
|**status**|**smallint**|Bitmuster, das den Status der Option kennzeichnet. Folgende Werte sind möglich:<br /><br /> 0 = Statisch Die Einstellung wird beim Neustart des Servers wirksam.<br /><br /> 1 = Dynamisch. Variable wird beim Ausführen der RECONFIGURE-Anweisung wirksam.<br /><br /> 2 = Erweitert. Variable wird nur angezeigt, wenn **Erweiterte Optionen anzeigen** festgelegt ist.<br /><br /> 3 = Dynamisch und erweitert.|  
  
## <a name="see-also"></a>Siehe auch  
 [Zuordnen von Systemtabellen zu Systemsichten &#40; Transact-SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Kompatibilitätssichten &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
