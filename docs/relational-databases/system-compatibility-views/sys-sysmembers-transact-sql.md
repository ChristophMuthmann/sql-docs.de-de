---
title: Sys.Sysmembers (Transact-SQL) | Microsoft Docs
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
- sys.sysmembers_TSQL
- sysmembers
- sys.sysmembers
- sysmembers_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sysmembers system table
- sys.sysmembers compatibility view
ms.assetid: ceb18341-f985-4849-ac83-21d67ab7b980
caps.latest.revision: "38"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 85cc702f5cbb9abb223325743886fa97fb9b9fbb
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="syssysmembers-transact-sql"></a>sys.sysmembers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jedes Mitglied einer Datenbankrolle.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**memberuid**|**smallint**|Benutzername für das Rollenmitglied. Führt zu einem Überlauf oder gibt NULL zurück, wenn die Anzahl von Benutzern und Rollen 32.767 übersteigt.|  
|**groupuid**|**smallint**|Benutzername für die Rolle. Führt zu einem Überlauf oder gibt NULL zurück, wenn die Anzahl von Benutzern und Rollen 32.767 übersteigt.|  
  
## <a name="see-also"></a>Siehe auch  
 [Zuordnen von Systemtabellen zu Systemsichten &#40; Transact-SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Kompatibilitätssichten &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
