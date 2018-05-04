---
title: Sys.sysconfigures (Transact-SQL) | Microsoft Docs
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
- sys.sysconfigures
- sysconfigures
- sys.sysconfigures_TSQL
- sysconfigures_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysconfigures compatibility view
- sysconfigures system table
ms.assetid: 146bf10a-c898-4676-a2a1-673fb1cee7a2
caps.latest.revision: 39
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 62423ffb1f596a65fbd7a754947c2c3d04f7fb2f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="syssysconfigures-transact-sql"></a>sys.sysconfigures (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jede von einem Benutzer festgelegte Konfigurationsoption. **Sysconfigures** enthält die verschiedenen Konfigurationsoptionen, die vor dem letzten Start von definiert sind [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], sowie alle dynamischen Konfigurationsoptionen seitdem festgelegten.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**value**|**int**|Vom Benutzer änderbarer Wert für die Variable. Dies dient der [!INCLUDE[ssDE](../../includes/ssde-md.md)] nur, wenn RECONFIGURE ausgeführt wurde.|  
|**config**|**int**|Nummer der Konfigurationsvariablen.|  
|**Kommentar**|**nvarchar(255)**|Erläuterung der Konfigurationsoption.|  
|**status**|**smallint**|Bitmuster, das den Status der Option anzeigt. Folgende Werte sind möglich:<br /><br /> 0 = Statisch Die Einstellung wird beim Neustart des Servers wirksam.<br /><br /> 1 = Dynamisch. Variable wird beim Ausführen der RECONFIGURE-Anweisung wirksam.<br /><br /> 2 = Erweitert. Variable wird nur angezeigt, wenn **Erweiterte Optionen anzeigen** festgelegt ist. Die Einstellung wird beim Neustart des Servers wirksam.<br /><br /> 3 = Dynamisch und erweitert.|  
  
## <a name="see-also"></a>Siehe auch  
 [Zuordnen von Systemtabellen zu Systemsichten &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Kompatibilitätssichten &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
