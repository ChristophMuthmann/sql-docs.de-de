---
title: Sys. database_scoped_configurations (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 01/16/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- database_scoped_configurations
- database_scoped_configurations_TSQL
- sys.database_scoped_configurations
- sys.database_scoped_configurations_TSQL
helpviewer_keywords:
- sys.database_scoped_configurations catalog view
ms.assetid: 8899310a-3464-4d38-9f2f-88396c4e7dc2
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 84a4da130f637e85e4ebc950db5568f1fa8876f2
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysdatabasescopedconfigurations-transact-sql"></a>Sys. database_scoped_configurations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Enthält eine Zeile für jede Konfiguration. 
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**configuration_id**|**int**|Die ID der Konfigurationsoption.|  
|**name**|**nvarchar(60)**|Der Name der Konfigurationsoption. Informationen zu den möglichen Konfigurationen finden Sie unter [ALTER DATABASE SCOPED CONFIGURATION &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).|  
|**value**|**sqlvariant**|Der Wert für diese Konfigurationsoption für das primäre Replikat festgelegt.|  
|**value_for_secondary**|**sqlvariant**|Der Wert für diese Konfigurationsoption für die sekundären Replikate.|  
  
##  <a name="Permissions"></a> Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="remarks"></a>Hinweise  
 Wenn NULL zurückgegeben wird, als der Wert für **Value_for_secondary**, dies bedeutet, dass die sekundäre Datenbank auf Primär festgelegt ist.  
 
 Datenbankweit gültige Konfiguration wie die Einstellungen mit der Datenbank übernommen. Dies bedeutet, dass bei eine bestimmte Datenbank wiederhergestellt oder angefügt wird, die vorhandenen Konfigurationseinstellungen bleiben.
  
## <a name="see-also"></a>Siehe auch  
 [ALTER DATABASE SCOPED CONFIGURATION (Transact-SQL)](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)  
  
  
