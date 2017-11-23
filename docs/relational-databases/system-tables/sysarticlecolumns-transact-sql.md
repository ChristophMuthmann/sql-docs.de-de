---
title: Sysarticlecolumns (Transact-SQL) | Microsoft Docs
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
- sysarticlecolumns
- sysarticlecolumns_TSQL
dev_langs: TSQL
helpviewer_keywords: sysarticlecolumns system table
ms.assetid: 55918592-e05d-43b6-843b-7e4d82fa6275
caps.latest.revision: "26"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2b4872dce57b1f7f33a1fc03af3aae31562ceab2
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sysarticlecolumns-transact-sql"></a>sysarticlecolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **Sysarticlecolumns** -Tabelle enthält eine Zeile für jede Tabellenspalte, die in einer Momentaufnahme- oder transaktionsveröffentlichung veröffentlicht wird, und ordnet jede Spalte dem zugehörigen Artikel. Diese Tabelle wird in der Veröffentlichungsdatenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|Identifiziert einen Artikel.|  
|**Spalten-ID**|**smallint**|Identifiziert eine Spalte in einem Artikel.|  
|**is_udt**|**bit**|Zeigt an, ob die Spalte dem benutzerdefinierten Datentyp (UDT) zugehört. Der Wert **1** zeigt eine UDT-Spalte.|  
|**is_xml**|**bit**|Gibt an, ob die Spalte ist eine **Xml** Spalte. Der Wert **1** gibt eine XML-Spalte an.|  
|**is_max**|**bit**|Gibt an, ob die Spalte einen hohen Wert-Datentypspalte **varchar(max)**, **nvarchar(max)**, und **varbinary(max)**. Der Wert **1** gibt eine Spalte mit großen Werten an.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
