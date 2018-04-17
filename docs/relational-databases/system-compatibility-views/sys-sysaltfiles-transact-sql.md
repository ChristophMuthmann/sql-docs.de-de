---
title: Sys.sysaltfiles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-compatibility-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sysaltfiles_TSQL
- sys.sysaltfiles
- sysaltfiles_TSQL
- sysaltfiles
dev_langs:
- TSQL
helpviewer_keywords:
- sysaltfiles system table
- sys.sysaltfiles compatibility view
ms.assetid: 698dec23-5336-4108-87a5-f8e407f8da09
caps.latest.revision: 35
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c0e28c43fc99ee674b5190cb7d4404496ff6601a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="syssysaltfiles-transact-sql"></a>sys.sysaltfiles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält unter bestimmten Umständen Zeilen, die den Dateien in einer Datenbank entsprechen.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**fileid**|**smallint**|Datei-ID. Diese ist für jede Datenbank eindeutig.|  
|**groupid**|**smallint**|Dateigruppen-ID.|  
|**size**|**int**|Dateigröße in Seiten mit einer Größe von 8 KB.|  
|**maxsize**|**int**|Maximale Dateigröße in Seiten mit einer Größe von 8 KB.<br /><br /> 0 = Keine Vergrößerung.<br /><br /> -1 = Datei wird vergrößert, bis der Datenträger voll ist.<br /><br /> 268435456 = Protokolldatei wird bis zu einer maximalen Größe von 2 TB vergrößert.<br /><br /> Hinweis: Datenbanken, die mit einer unbegrenzten Protokolldateigröße aktualisiert werden werden-1 für die maximale Größe der Protokolldatei gemeldet.|  
|**growth**|**int**|Zuwachsgröße für die Datenbank.<br /><br /> 0 = Keine Vergrößerung. Kann je nach dem Wert von status entweder die Seitenanzahl oder der Prozentsatz der Dateigröße sein. Falls **status** 0x100000 ist, entspricht **growth** dem Prozentsatz der Dateigröße. Andernfalls handelt es sich um die Anzahl von Seiten.|  
|**status**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**perf**|**int**|Reserviert.|  
|**dbid**|**smallint**|Datenbank-ID der Datenbank, zu der diese Datei gehört.|  
|**name**|**sysname**|Logischer Name der Datei.|  
|**Dateiname**|**nvarchar(260)**|Name des physischen Geräts. Der Name schließt den vollständigen Pfad der Datei ein.|  
  
## <a name="see-also"></a>Siehe auch  
 [Zuordnen von Systemtabellen zu Systemsichten &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Kompatibilitätssichten &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
