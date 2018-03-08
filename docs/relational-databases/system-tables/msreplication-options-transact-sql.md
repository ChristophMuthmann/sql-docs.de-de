---
title: MSreplication_options (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- MSreplication_options
- MSreplication_options_TSQL
dev_langs: TSQL
helpviewer_keywords: MSreplication_options system table
ms.assetid: 23cf10d7-8bc1-4368-b5eb-e5576421e776
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5711a1f0de3f335867c3b5162a4ec77f52d79dfc
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="msreplicationoptions-transact-sql"></a>MSreplication_options (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MSreplication_options** -Tabelle speichert Metadaten, die intern von der Replikation verwendet wird. Diese Tabelle wird gespeichert, der **master** Datenbank.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**optname**|**sysname**|Nur interne Verwendung.|  
|**Wert**|**bit**|Nur interne Verwendung.|  
|**Hauptversion**|**int**|Nur interne Verwendung.|  
|**Nebenversion lauten**|**int**|Nur interne Verwendung.|  
|**Revision**|**int**|Nur interne Verwendung.|  
|**install_failures**|**int**|Nur interne Verwendung.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
