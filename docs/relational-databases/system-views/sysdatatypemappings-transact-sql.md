---
title: Sysdatatypemappings (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sysdatatypemappings
- sysdatatypemappings_TSQL
dev_langs: TSQL
helpviewer_keywords: sysdatatypemappings view
ms.assetid: 5dfafb70-3e3d-4465-b293-1acff1f855b6
caps.latest.revision: "12"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 60e850e319c4c31c2208448fe29a28acf13a8d45
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdatatypemappings-transact-sql"></a>sysdatatypemappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Mit der **sysdatatypemappings** -Sicht wird die Zuordnung zwischen SQL Server-Datentypen und Datentypen eines Nicht-SQL Server-Datenbank-Managementsystems (DBMS) angezeigt. Diese Sicht wird in der **msdb** -Datenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**mapping_id**|**int**|Die ID der Datentypzuordnung.|  
|**source_dbms**|**sysname**|Gibt den Namen des DBMS an, aus dem die Datentypen zugeordnet werden, wobei die folgenden Werte möglich sind:<br /><br /> **MSSQLSERVER** = die Quelle ist eine SQL Server-Datenbank.<br /><br /> **ORACLE** = Die Quelle ist eine Oracle-Datenbank.|  
|**source_version**|**sysname**|Gibt die Produktversion des Quell-DBMS an.|  
|**source_type**|**sysname**|Gibt den im Quell-DBMS aufgelisteten Datentyp an.|  
|**source_length_min**|**bigint**|Die Mindestlänge des Datentyps im Quell-DBMS, wobei der Wert NULL angibt, dass die Länge nicht verwendet wird.|  
|**source_length_max**|**bigint**|Die maximale Länge des Datentyps im Quell-DBMS, wobei der Wert NULL angibt, dass die Länge nicht verwendet wird.|  
|**source_precision_min**|**bigint**|Die Mindestgenauigkeit des Datentyps im Quell-DBMS, wobei der Wert NULL angibt, dass die Genauigkeit nicht verwendet wird.|  
|**source_precision_max**|**bigint**|Die maximale Genauigkeit des Datentyps im Quell-DBMS, wobei der Wert NULL angibt, dass die Genauigkeit nicht verwendet wird.|  
|**source_scale_min**|**int**|Die Mindestdezimalstellen des Datentyps im Quell-DBMS, wobei der Wert NULL angibt, dass die Dezimalstellen nicht verwendet werden.|  
|**source_scale_max**|**int**|Die maximalen Dezimalstellen des Datentyps im Quell-DBMS, wobei der Wert NULL angibt, dass die Dezimalstellen nicht verwendet werden.|  
|**source_nullable**|**bit**|Gibt an, ob der Zieldatentyp NULL-Werte unterstützt.|  
|**source_createparams**|**int**|Nur interne Verwendung.|  
|**destination_dbms**|**sysname**|Gibt den Namen des Ziel-DBMS an, wobei die folgenden Werte möglich sind:<br /><br /> **MSSQLSERVER** = Das Ziel ist eine SQL Server-Datenbank.<br /><br /> **ORACLE** = Das Ziel ist eine Oracle-Datenbank.<br /><br /> **DB2** = Das Ziel ist eine IBM DB2-Datenbank.<br /><br /> **SYBASE** = Das Ziel ist eine Sybase-Datenbank.|  
|**destination_version**|**sysname**|Die Produktversion des Ziel-DBMS.|  
|**destination_type**|**sysname**|Der Datentyp im Ziel-DBMS.|  
|**destination_length**|**bigint**|Die Länge des Datentyps im Ziel-DBMS.|  
|**destination_precision**|**bigint**|Die Genauigkeit des Datentyps im Ziel-DBMS.|  
|**destination_scale**|**int**|Die Dezimalstellen des Datentyps im Ziel-DBMS.|  
|**destination_nullable**|**bit**|Gibt an, ob der Datentyp im Ziel-DBMS NULL-Werte unterstützt.|  
|**destination_createparams**|**int**|Nur interne Verwendung.|  
|**Products**|**bit**|Gibt an, ob beim Zuordnen zwischen dem Datentyp des Quell- und Ziel-DBMS Daten verloren gehen.|  
|**is_default**|**bit**|Gibt an, ob standardmäßig die Datentypzuordnung verwendet wird.|  
  
## <a name="see-also"></a>Siehe auch  
 [Heterogene Datenbankreplikation](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Replikationstabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40; Transact-SQL &#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [Sp_helpdatatypemap &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)  
  
  
