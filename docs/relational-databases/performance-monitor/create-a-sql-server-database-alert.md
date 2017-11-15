---
title: Erstellen einer SQL Server-Datenbankwarnung | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- database performance [SQL Server], alerts
- alerts [SQL Server], creating
- thresholds [SQL Server]
- database alerts [SQL Server]
- tuning databases [SQL Server], alerts
- monitoring performance [SQL Server], alerts
- monitoring server performance [SQL Server], alerts
- database monitoring [SQL Server], alerts
- server performance [SQL Server], alerts
ms.assetid: 0511136a-1b6b-4095-aa45-39e77b67aba2
caps.latest.revision: "22"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: d3c3be8076e26cfcf61e3623ad76221d993a46c1
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="create-a-sql-server-database-alert"></a>Erstellen einer SQL Server-Datenbankwarnung
  Sie können mithilfe des Systemmonitors eine Warnung erstellen, die ausgelöst wird, sobald ein Schwellenwert für einen Leistungsindikator des Systemmonitors erreicht wird. Als Reaktion auf die Warnung startet der Systemmonitor eine Anwendung, z. B. eine für die Verarbeitung der Warnung geschriebene benutzerdefinierte Anwendung. Sie könnten beispielsweise eine Warnung erstellen, die ausgelöst wird, wenn die Anzahl der Deadlocks einen bestimmten Wert überschreitet.  
  
 Sie können Warnungen auch mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] und mithilfe des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents erstellen. Weitere Informationen finden Sie unter [Warnungen](http://msdn.microsoft.com/library/3f57d0f0-4781-46ec-82cd-b751dc5affef).  
  
 Weitere Informationen zum Verwenden des Systemmonitors zum Einrichten einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbankwarnung finden Sie unter [Einrichten einer SQL Server-Datenbankwarnung &#40;Windows&#41;](../../relational-databases/performance/set-up-a-sql-server-database-alert-windows.md).  
  
## <a name="see-also"></a>Siehe auch  
 [sp_add_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)   
 [sys.sysperfinfo &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysperfinfo-transact-sql.md)  
  
  
