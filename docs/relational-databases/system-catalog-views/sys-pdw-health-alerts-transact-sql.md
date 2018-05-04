---
title: Sys.pdw_health_alerts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: pdw
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 49c01e5f-ee47-41a0-871d-35a759f50851
caps.latest.revision: 7
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d1aa54191828a71c66c4575451c571621383ae24
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="syspdwhealthalerts-transact-sql"></a>sys.pdw_health_alerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Speichert Eigenschaften für die anderen Warnungen, die auftreten können, auf dem System. Dies ist eine Katalogtabelle für Warnungen.  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|alert_id|**int**|Eindeutiger Bezeichner der Warnung.<br /><br /> Der Schlüssel für diese Ansicht.|NOT NULL|  
|component_id|**int**|ID der Komponente, die diese Warnung gilt. Die Komponente ist eine allgemeine Komponente-Bezeichner, z. B. "Stromversorgung," und ist nicht spezifisch für eine Installation. Finden Sie unter [sys.pdw_health_components &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).|NOT NULL|  
|alert_name|**nvarchar(255)**|Der Name der Warnung.|NOT NULL|  
|state|**nvarchar(32)**|Status der Warnung.|NOT NULL<br /><br /> Mögliche Werte:<br /><br /> 'Operational'<br /><br /> "Weiter"<br /><br /> "Heruntergestuft"<br /><br /> "Fehlgeschlagen"|  
|severity|**nvarchar(32)**|Schweregrad der Warnung.|NOT NULL<br /><br /> Mögliche Werte:<br /><br /> "Information"<br /><br /> "Warnung"<br /><br /> "Fehler"|  
|Typ|**nvarchar(32)**|Der Typ der Warnung.|NOT NULL<br /><br /> Mögliche Werte:<br /><br /> StatusChange - wurde der Status geändert werden.<br /><br /> Schwellenwert - ein Wert hat den Schwellenwert überschritten.|  
|description|**nvarchar(4000)**|Beschreibung der Warnung.|NOT NULL|  
|Bedingung|**nvarchar(255)**|Geben Sie verwendet, wenn Schwellenwert =. Definiert, wie der Warnschwellenwert berechnet wird.|NULL|  
|status|**nvarchar(32)**|Warnungsstatus|NULL|  
|Value|**bit**|Gibt an, ob die Warnung auftreten, während des Systembetriebs zulässig ist.|NULL<br /><br /> Mögliche Werte<br /><br /> 0 – wird die Warnung nicht generiert.<br /><br /> 1 - Warnung wird generiert.|  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Datawarehouse und Parallel Datawarehouse-Katalogsichten](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
