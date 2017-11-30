---
title: Sys.syspermissions (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-compatibility-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.syspermissions_TSQL
- syspermissions_TSQL
- sys.syspermissions
- syspermissions
dev_langs: TSQL
helpviewer_keywords:
- syspermissions system table
- sys.syspermissions compatibility view
ms.assetid: ba9a9a88-55d2-41a7-b09b-342e8b9a54c5
caps.latest.revision: "36"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 517e30926bbe4becfb2cc3764c153ab683796144
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="syssyspermissions-transact-sql"></a>sys.syspermissions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält Informationen zu Berechtigungen, die Benutzern, Gruppen und Rollen in der Datenbank erteilt oder verweigert werden.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|**id**|**int**|ID des Objekts für Objektberechtigungen.<br /><br /> 0 = Anweisungsberechtigungen.|  
|**Empfänger**|**smallint**|ID des Benutzers, der Gruppe oder der Rolle, auf den bzw. die sich die Berechtigung auswirkt.|  
|**GRANTOR**|**smallint**|ID des Benutzers, der Gruppe oder der Rolle, der bzw. die die Berechtigung erteilt oder verweigert hat.|  
|**actadd**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**actmod**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**Ausw**|**varbinary(4000)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**selmod**|**varbinary(4000)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**updadd**|**varbinary(4000)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**updmod**|**varbinary(4000)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**refadd**|**varbinary(4000)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**refmod**|**varbinary(4000)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
## <a name="see-also"></a>Siehe auch  
 [Zuordnen von Systemtabellen zu Systemsichten &#40; Transact-SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Kompatibilitätssichten &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
