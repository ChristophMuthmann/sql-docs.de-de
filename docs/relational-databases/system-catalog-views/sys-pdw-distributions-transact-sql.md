---
title: Sys.pdw_distributions (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 572b5187-9753-4063-adf8-65dea87d11f8
caps.latest.revision: "7"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3018a1c7ef35aa2c1308a37f8d84de4a61d0d6d6
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="syspdwdistributions-transact-sql"></a>Sys.pdw_distributions (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Enthält Informationen zu den Verteilungen auf dem Gerät. Sie enthält eine Zeile pro Einheit-Verteilung.  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|distribution_id|**int**|Eindeutige numerische Id, die die Verteilung zugeordnet.<br /><br /> Der Schlüssel für diese Ansicht.|zwischen 1 und die Anzahl von Serverknoten in Appliance, die die Anzahl der pro-Serverknoten multipliziert.|  
|pdw_node_id|**int**|Die ID des Knotens, auf der diese Verteilung.|Finden Sie unter Pdw_node_id in [sys.dm_pdw_nodes &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|name|**nvarchar(32)**|Zeichenfolgen Sie-ID, die die Verteilung, als Suffix für verteilte Tabellen verwendet.|Zeichenfolge zusammengesetzt von "A-Z", "a-Z", "0-9', '_','-'.|  
|position|**int**|Die Position der Verteilung innerhalb eines je nach anderen Verteilungen auf diesem Knoten Knotens.|zwischen 1 und die Anzahl der Verteilungen pro Knoten.|  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Datawarehouse und Parallel Datawarehouse-Katalogsichten](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
