---
title: Sys. database_scoped_configurations (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/29/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- database_scoped_configurations
- database_scoped_configurations_TSQL
- sys.database_scoped_configurations
- sys.database_scoped_configurations_TSQL
helpviewer_keywords: sys.database_scoped_configurations catalog view
ms.assetid: 8899310a-3464-4d38-9f2f-88396c4e7dc2
caps.latest.revision: "13"
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 70b0f5c2ecb1f15828d5ac1c219033c337bb3a8f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdatabasescopedconfigurations-transact-sql"></a>Sys. database_scoped_configurations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Enthält eine Zeile für jede Konfiguration. 
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**configuration_id**|**int**|Die ID der Konfigurationsoption.|  
|**name**|**nvarchar(60)**|Der Name der Konfigurationsoption. Informationen zu den möglichen Konfigurationen finden Sie unter [ALTER DATABASE SCOPED CONFIGURATION &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).|  
|**Wert**|**SQLVARIANT**|Der Wert für diese Konfigurationsoption für das primäre Replikat festgelegt.|  
|**value_for_secondary**|**SQLVARIANT**|Der Wert für diese Konfigurationsoption für die sekundären Replikate.|  
  
##  <a name="Permissions"></a> Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="remarks"></a>Hinweise  
 Wenn NULL zurückgegeben wird, als der Wert für **Value_for_secondary**, dies bedeutet, dass die sekundäre Datenbank auf Primär festgelegt ist.  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER DATABASE ausgelegte CONFIGURATION &#40; Transact-SQL &#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)  
  
  
