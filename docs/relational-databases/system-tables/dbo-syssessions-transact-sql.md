---
title: dbo.syssessions (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dbo.syssessions_TSQL
- dbo.syssessions
- syssessions_TSQL
- syssessions
dev_langs: TSQL
helpviewer_keywords: syssessions system table
ms.assetid: 187819b6-c7f4-4a26-b74c-0a89e96695cf
caps.latest.revision: "14"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 140d81eef1b0f6b745e5f889b7889c265820405c
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="dbosyssessions-transact-sql"></a>dbo.syssessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Jedes Mal [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent gestartet wird, wird eine neue Sitzung erstellt. Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent verwendet Sitzungen, um den Status von Aufträgen beizubehalten, wenn der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent-Dienst neu gestartet oder unerwartet beendet wird. Jede Zeile der **syssessions** -Tabelle enthält Informationen zu einer Sitzung. Mithilfe der **sysjobactivity** -Tabelle kann der Auftragsstatus am Ende einer Sitzung angezeigt werden.  
  
 Diese Tabelle wird in der **msdb** -Datenbank gespeichert.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|ID einer Sitzung des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agents.|  
|**agent_start_date**|**datetime**|Datum und Uhrzeit, zu der der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent-Dienst für diese Sitzung gestartet wurde.|  
  
## <a name="remarks"></a>Hinweise  
 Nur Mitglieder der festen Serverrolle **sysadmin** können auf diese Tabelle zugreifen.  
  
## <a name="see-also"></a>Siehe auch  
 [dbo.sysjobactivity &#40; Transact-SQL &#41;](../../relational-databases/system-tables/dbo-sysjobactivity-transact-sql.md)  
  
  
