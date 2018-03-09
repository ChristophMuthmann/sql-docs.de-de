---
title: Sys. allocation_units (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.allocation_units_TSQL
- sys.allocation_units
- allocation_units_TSQL
- allocation_units
dev_langs:
- TSQL
helpviewer_keywords:
- sys.allocation_units catalog view
ms.assetid: ec9de780-68fd-4551-b70b-2d3ab3709b3e
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ae268f41550268aab1afb03b587d2fd5e735e911
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="sysallocationunits-transact-sql"></a>sys.allocation_units (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Enthält eine Zeile für jede Zuordnungseinheit in der Datenbank.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|allocation_unit_id|**bigint**|ID der Zuordnungseinheit. Ist innerhalb einer Datenbank eindeutig.|  
|Typ|**tinyint**|Typ der Zuordnungseinheit:<br /><br /> 0 = Gelöscht<br /><br /> 1 = Daten in Zeilen (alle Datentypen mit Ausnahme von LOB-Datentypen)<br /><br /> 2 = LOB-Daten (Large Object) (**text**, **ntext**, **image**, **xml**, große Werttypen und benutzerdefinierte CLR-Typen)<br /><br /> 3 = Zeilenüberlaufdaten|  
|type_desc|**nvarchar(60)**|Beschreibung des Typs der Zuordnungseinheit:<br /><br /> **GELÖSCHT**<br /><br /> **IN_ROW_DATA**<br /><br /> **LOB_DATA**<br /><br /> **ROW_OVERFLOW_DATA**|  
|container_id|**bigint**|ID des Speichercontainers, der der Zuordnungseinheit zugeordnet ist.<br /><br /> Wenn Typ = 1 oder 3, Container_id = hobt_id.<br /><br /> Wenn Typ 2, und klicken Sie dann auf Container_id = partition_id.<br /><br /> 0 = Für die verzögerte Löschung gekennzeichnete Zuordnungseinheit|  
|data_space_id|**int**|ID der Dateigruppe, in der sich diese Zuordnungseinheit befindet.|  
|total_pages|**bigint**|Gesamtanzahl der Seiten, die von dieser Zuordnungseinheit zugeordnet oder reserviert wurden.|  
|used_pages|**bigint**|Gesamtanzahl der tatsächlich verwendeten Seiten.|  
|data_pages|**bigint**|Anzahl verwendeter Seiten, die über Folgendes verfügen:<br /><br /> Daten in Zeilen<br /><br /> LOB-Daten<br /><br /> Zeilenüberlaufdaten<br /><br /> <br /><br /> Beachten Sie, die der zurückgegebene Wert schließt interne Indexseiten und zuordnungsverwaltungsseiten aus.|  
  
> [!NOTE]  
>  Löschen oder große Indizes neu erstellen oder löschen oder Abschneiden große Tabellen die [!INCLUDE[ssDE](../../includes/ssde-md.md)] orientiert sich die tatsächlichen aufgehobenen seitenzuordnungen sowie die zugehörigen sperren, bis nach dem Commit der Transaktion. Bei verzögerten Löschvorgängen wird der zugeordnete Speicherplatz nicht sofort freigegeben. Aus diesem Grund können von Sys. allocation_units sofort nach dem Löschen oder Abschneiden eines großen Objekts zurückgegebenen Werte nicht den tatsächlich verfügbaren Speicherplatz wider.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle. Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Sys.Partitions &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [Katalogsichten für Objekte &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
