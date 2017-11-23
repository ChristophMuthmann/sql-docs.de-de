---
title: "\"sysdac_instances_internal\" (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysdac_instances_internal_TSQL
- sysdac_instances_internal
dev_langs: TSQL
helpviewer_keywords: sysdac_instances_internal
ms.assetid: d2d52cc4-3463-431a-b779-6fbfdeee1dfc
caps.latest.revision: "9"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e7760659f0f4158a47b1e775106f376aa9f0f13a
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="data-tier-application-tables---sysdacinstancesinternal"></a>Data-Tier-Anwendungstabellen - "sysdac_instances_internal"
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Zeigt eine Zeile für jede Instanz der Datenebenenanwendung (DAC) an, die für eine [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz bereitgestellt wird. Diese Tabelle wird im Dbo-Schema in der Msdb-Datenbank gespeichert.  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|instance_id|**uniqueidentifier**|Der Bezeichner der DAC-Instanz.|  
|instance_name|**sysname**|Der Name der DAC-Instanz, die bei der Bereitstellung der Instanz angegeben wurde.|  
|type_name|**sysname**|Der Name der DAC, die bei der Erstellung des DAC-Pakets angegeben wurde.|  
|type_version|**nvarchar(64)**|Die Version der DAC, die bei der Erstellung des DAC-Pakets angegeben wurde.|  
|Beschreibung|**nvarchar(4000)**|Eine Beschreibung der DAC, die bei der Erstellung des DAC-Pakets geschrieben wurde.|  
|type_stream|**varbinary(max)**|Ein Bitdatenstrom, der die codierte Darstellung der in der DAC enthaltenen logischen Objekte, z. B. Tabellen und Sichten, enthält.|  
|date_created|**datetime**|Datum und Uhrzeit der Erstellung der DAC-Instanz.|  
|created_by|**sysname**|Der Anmeldename, unter dem die DAC-Instanz erstellt wurde.|  
  
## <a name="remarks"></a>Hinweise  
 Nur-Lese Zugriff auf diese Sicht ist für alle Benutzer mit Berechtigungen zum Verbinden mit der master-Datenbank verfügbar.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Serverrolle sysadmin.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenebenenanwendungen](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [dbo.sysdac_instances &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/data-tier-application-views-dbo-sysdac-instances.md)  
  
  
