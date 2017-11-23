---
title: Sysarticlecolumns (Systemsicht) (Transact-SQL) | Microsoft Docs
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
- sysarticlecolumns
- sysarticlecolumns_TSQL
dev_langs: TSQL
helpviewer_keywords: sysarticlecolumns view
ms.assetid: a8dd8d13-c827-45c4-87ba-802725301382
caps.latest.revision: "10"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a7e5f8c29826bd37306fe2fc455b449ab6362c67
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysarticlecolumns-system-view-transact-sql"></a>sysarticlecolumns (Systemsicht) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **Sysarticlecolumns** -Sicht macht zusätzliche Informationen zu Spalten in veröffentlichten Artikeln verfügbar. Diese Sicht wird in der distribution-Datenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|Identifiziert einen Artikel.|  
|**Spalten-ID**|**int**|Identifiziert eine Spalte in einem Artikel.|  
|**is_udt**|**int**|Zeigt an, ob die Spalte dem benutzerdefinierten Datentyp (UDT) zugehört. Der Wert **1** zeigt eine UDT-Spalte.|  
|**is_xml**|**int**|Wenn die Spalte ist eine **Xml** Spalte. Der Wert **1** gibt eine **Xml** Spalte.|  
|**is_max**|**int**|Wenn die Spalte eine Spalte mit hohen Werten-Datentyp ist (**varchar(max)**, **nvarchar(max)** oder **varbinary(max)**). Der Wert **1** gibt eine Spalte mit großen Werten an.|  
  
## <a name="see-also"></a>Siehe auch  
 [sp_articlecolumn &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [Sysarticlecolumns &#40; Transact-SQL &#41;](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
