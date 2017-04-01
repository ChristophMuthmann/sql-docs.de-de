---
title: "Erstellen einer SQL Server-Datenbankwarnung | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Datenbankleistung [SQL Server], Warnungen"
  - "Warnungen [SQL Server], erstellen"
  - "Schwellenwerte [SQL Server]"
  - "Datenbankwarnungen [SQL Server]"
  - "Optimieren von Datenbanken [SQL Server], Warnungen"
  - "Überwachen der Leistung [SQL Server], Warnungen"
  - "Überwachen der Serverleistung [SQL Server], Warnungen"
  - "Datenbanküberwachung [SQL Server], Warnungen"
  - "Serverleistung [SQL Server], Warnungen"
ms.assetid: 0511136a-1b6b-4095-aa45-39e77b67aba2
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# Erstellen einer SQL Server-Datenbankwarnung
  Sie können mithilfe des Systemmonitors eine Warnung erstellen, die ausgelöst wird, sobald ein Schwellenwert für einen Leistungsindikator des Systemmonitors erreicht wird. Als Reaktion auf die Warnung startet der Systemmonitor eine Anwendung, z. B. eine für die Verarbeitung der Warnung geschriebene benutzerdefinierte Anwendung. Sie könnten beispielsweise eine Warnung erstellen, die ausgelöst wird, wenn die Anzahl der Deadlocks einen bestimmten Wert überschreitet.  
  
 Sie können Warnungen auch mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] und mithilfe des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agents erstellen. Weitere Informationen finden Sie unter [Warnungen](../../ssms/agent/alerts.md).  
  
 Weitere Informationen zum Verwenden des Systemmonitors zum Einrichten einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbankwarnung finden Sie unter [Einrichten einer SQL Server-Datenbankwarnung &#40;Windows&#41;](../../relational-databases/performance/set-up-a-sql-server-database-alert-windows.md).  
  
## Siehe auch  
 [sp_add_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)   
 [sys.sysperfinfo &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysperfinfo-transact-sql.md)  
  
  