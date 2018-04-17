---
title: IHpublishercolumnconstraints (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- IHpublishercolumnconstraints
- IHpublishercolumnconstraints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublishercolumnconstraints system table
ms.assetid: d7a41da6-e067-430a-8da2-3f6745b8a4f3
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f7f22a616c846f5f074c641c799a935ea23482b7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="ihpublishercolumnconstraints-transact-sql"></a>IHpublishercolumnconstraints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **IHpublishercolumnconstraints** -Systemtabelle ordnet Spalten einer nicht - SQL Server-Veröffentlichung in der [IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md) -Systemtabelle Einschränkungen in der [IHpublisherconstraints ](../../relational-databases/system-tables/ihpublisherconstraints-transact-sql.md) -Systemtabelle. Diese Tabelle wird in der Verteilungsdatenbank gespeichert.  
  
## <a name="definition"></a>Definition  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**publishercolumn_id**|**int**|Identifiziert die Spalte aus [IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md) mit einer zugeordneten Beschränkung.|  
|**publisherconstraint_id**|**int**|Identifiziert eine Beschränkung aus [IHpublisherconstraints](../../relational-databases/system-tables/ihpublisherconstraints-transact-sql.md) der Spalte zugeordnet.|  
|**indid**|**int**|Gibt die Position einer Spalte innerhalb der veröffentlichten Tabelle an.|  
  
## <a name="see-also"></a>Siehe auch  
 [Heterogene Datenbankreplikation](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
