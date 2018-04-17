---
title: Sys.sysperfinfo (Transact-SQL) | Microsoft Docs
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
- sysperfinfo_TSQL
- sys.sysperfinfo_TSQL
- sys.sysperfinfo
- sysperfinfo
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysperfinfo compatibility view
- sysperfinfo system table
ms.assetid: e22a81cd-27de-4690-9443-6aad6393bd3c
caps.latest.revision: 40
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 49ca7e752f40a1614d78d246f2339d2142cb0b7d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="syssysperfinfo-transact-sql"></a>sys.sysperfinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] -Darstellung der internen Leistungsindikatoren, die über den Windows-Systemmonitor angezeigt werden können.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**object_name**|**vom Typ NCHAR(128)**|Name des Leistungsobjekts, z. B. **SQLServer:LockManager** oder **SQLServer:BufferManager**.|  
|**counter_name**|**vom Typ NCHAR(128)**|Name des Leistungsindikators innerhalb des Objekts, z. B. **Seitenanforderungen** oder **Sperranforderungen**.|  
|**instance_name**|**vom Typ NCHAR(128)**|Benannte Instanz des Indikators. Es gibt z. B. Indikatoren für jeden Typ von Sperre, z. B. **Tabelle**, **Seite**, **Schlüssel**und so weiter. Durch den Instanznamen kann zwischen ähnlichen Indikatoren unterschieden werden.|  
|**cntr_value**|**bigint**|Tatsächlicher Indikatorwert. Häufig ist dies ein konstanter oder monoton wachsender Leistungsindikator, der das Auftreten des Instanzereignisses zählt.|  
|**cntr_type**|**int**|Typ des Leistungsindikators, wie von der Windows-Leistungsarchitektur definiert.|  
  
## <a name="see-also"></a>Siehe auch  
 [Zuordnen von Systemtabellen zu Systemsichten &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Kompatibilitätssichten &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
