---
title: MSmerge_errorlineage (Transact-SQL) | Microsoft Docs
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
- MSmerge_errorlineage_TSQL
- MSmerge_errorlineage
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_errorlineage system table
ms.assetid: 3bcbd328-c958-4cd4-a573-3c35539fa919
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c11b1f3f9da7d6fedd4521cec0a1620f87f8b4f8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="msmergeerrorlineage-transact-sql"></a>MSmerge_errorlineage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MSmerge_errorlineage** -Tabelle enthält Zeilen, die auf dem Abonnenten gelöscht wurden, aber deren Löschung wird nicht an den Verleger weitergegeben. Diese Tabelle wird in der Veröffentlichungs- und in der Abonnementdatenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**tablenick**|**int**|Der ganzzahlige Wert, der der Tabelle zugewiesen ist, die für Mergereplikation veröffentlicht wird. Entspricht dem Nickname-Feld der **Sysmergearticles** Tabelle.|  
|**rowguid**|**uniqueidentifier**|Der Zeilenbezeichner.|  
|**Datenherkunft**|**varbinary(501)**|Speichert eine Verlaufsliste mit den Abonnenten und Verlegern, die eine Zeile aktualisiert haben. Er wird verwendet, um Konfliktsituationen zu entdecken und aufzulösen.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
