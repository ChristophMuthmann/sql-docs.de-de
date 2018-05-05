---
title: Sys.sysfiles (Transact-SQL) | Microsoft Docs
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
- sysfiles
- sys.sysfiles_TSQL
- sys.sysfiles
- sysfiles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysfiles system table
- sys.sysfiles compatibility view
ms.assetid: 3b47f38d-1cff-404d-89d3-9342c451c802
caps.latest.revision: 40
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: c1eceec521e6109735088225a5f394978607bf40
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="syssysfiles-transact-sql"></a>sys.sysfiles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jede Datei in einer Datenbank.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**fileid**|**smallint**|Datei-ID, die für jede Datenbank eindeutig ist.|  
|**groupid**|**smallint**|Dateigruppen-ID.|  
|**size**|**int**|Größe der Datei in Seiten mit einer Größe von 8 KB.|  
|**maxsize**|**int**|Maximale Dateigröße in Seiten mit einer Größe von 8 KB.<br /><br /> 0 = Keine Vergrößerung.<br /><br /> -1 = Datei wird vergrößert, bis der Datenträger voll ist.<br /><br /> 268435456 = Protokolldatei wird bis zu einer maximalen Größe von 2 TB vergrößert.<br /><br /> Hinweis: Datenbanken, die mit einer unbegrenzten Protokolldateigröße aktualisiert werden werden-1 für die maximale Größe der Protokolldatei gemeldet.|  
|**growth**|**int**|Zuwachsgröße für die Datenbank. Kann je nach Wert von **status**entweder die Seitenanzahl oder der Prozentsatz der Dateigröße sein.<br /><br /> 0 = Keine Vergrößerung.|  
|**status**|**int**|Statusbits für den **growth** -Wert in Megabyte (MB) oder Kilobyte (KB).<br /><br /> 0x2 = Datenträgerdatei.<br /><br /> 0x40 = Protokolldatei.<br /><br /> 0x100000 = Vergrößerung. Dieser Wert ist ein Prozentsatz (und nicht die Anzahl von Seiten).|  
|**perf**|**int**|Reserviert.|  
|**name**|**sysname**|Logischer Name der Datei.|  
|**Dateiname**|**nvarchar(260)**|Name des physischen Geräts. Der Name schließt den vollständigen Pfad der Datei ein.|  
  
## <a name="see-also"></a>Siehe auch  
 [Zuordnen von Systemtabellen zu Systemsichten &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Kompatibilitätssichten &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
