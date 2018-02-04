---
title: Sys.pdw_diag_sessions (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 4d23688a-cddb-4eed-8231-ecde2a0b0e65
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 91ad46c8f8bc0391bab933d2033d54e43626a6cc
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="syspdwdiagsessions-transact-sql"></a>sys.pdw_diag_sessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Enthält Informationen zu den verschiedenen diagnosesitzungen, die auf dem System erstellt wurden.  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|**name**|**nvarchar(255)**|Name des Diagnostics-Sitzung.<br /><br /> Der Schlüssel für diese Ansicht.||  
|**xml_data**|**nvarchar(4000)**|XML-Nutzlast, die Beschreibung der Sitzung.||  
|**is_active**|**bit**|Flag, das angibt, ob das Flag aktiv ist.||  
|**host_address**|**nvarchar(255)**|Die Adresse des Computers die Sitzungsdefinition (Steuerungsknoten) hosten.||  
|**principal_id**|**int**|Die ID des Benutzers, der die Sitzung auf der Datenbankebene erstellt.||  
|**database_id**|**int**|Die ID der Datenbank, die Bestandteil der diagnosesitzung ist.|  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Datawarehouse und Parallel Datawarehouse-Katalogsichten](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
