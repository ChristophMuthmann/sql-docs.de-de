---
title: SQL Server-Agent-Tabellen (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- SQL Server Agent, system tables
- system tables [SQL Server], SQL Server Agent
ms.assetid: 6cb39bfd-079e-4be4-9c42-2fa234c65ce1
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 37691cad424b53dc4e89458fd231fecbdcb06497
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sql-server-agent-tables-transact-sql"></a>SQL Server-Agent-Tabellen (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  In den Themen in diesem Abschnitt werden die Systemtabellen beschrieben, in denen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent verwendete Informationen gespeichert werden. Alle Tabellen sind im Dbo-Schema in der Msdb-Datenbank.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [dbo.sysalerts](../../relational-databases/system-tables/dbo-sysalerts-transact-sql.md)  
 Enthält eine Zeile für jede Warnung.  
  
 [dbo.syscategories](../../relational-databases/system-tables/dbo-syscategories-transact-sql.md)  
 Enthält die Kategorien, die von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] zur Organisation von Aufträgen, Warnungen und Operatoren verwendet werden.  
  
 [dbo.sysdownloadlist](../../relational-databases/system-tables/dbo-sysdownloadlist-transact-sql.md)  
 Enthält die Warteschlange der Downloadanweisungen für alle Zielserver.  
  
 [dbo.sysjobactivity](../../relational-databases/system-tables/dbo-sysjobactivity-transact-sql.md)  
 Enthält Informationen zu aktuellen Auftragsaktivitäten und zum aktuellen Auftragsstatus des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agents.  
  
 [dbo.sysjobhistory](../../relational-databases/system-tables/dbo-sysjobhistory-transact-sql.md)  
 Enthält Informationen zur Ausführung geplanter Aufträge durch den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent.  
  
 [dbo.sysjobs](../../relational-databases/system-tables/dbo-sysjobs-transact-sql.md)  
 Speichert die Informationen für jeden geplanten Auftrag, der vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent ausgeführt werden soll.  
  
 [dbo.sysjobschedules](../../relational-databases/system-tables/dbo-sysjobschedules-transact-sql.md)  
 Enthält Zeitplaninformationen für Aufträge von auszuführenden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent  
  
 [dbo.sysjobservers](../../relational-databases/system-tables/dbo-sysjobservers-transact-sql.md)  
 Speichert die Zuordnung oder Beziehung eines bestimmten Auftrags zu einem oder mehreren Zielservern.  
  
 [dbo.sysjobsteps](../../relational-databases/system-tables/dbo-sysjobsteps-transact-sql.md)  
 Enthält die Informationen für jeden Schritt in einem Auftrag, der vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent ausgeführt werden soll.  
  
 [dbo.sysjobstepslogs](../../relational-databases/system-tables/dbo-sysjobstepslogs-transact-sql.md)  
 Enthält Informationen zu Auftragsschrittprotokollen.  
  
 [dbo.sysnotifications](../../relational-databases/system-tables/dbo-sysnotifications-transact-sql.md)  
 Enthält eine Zeile für jede Benachrichtigung.  
  
 [dbo.sysoperators](../../relational-databases/system-tables/dbo-sysoperators-transact-sql.md)  
 Enthält eine Zeile für jede [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Operator.  
  
 [dbo.sysproxies](../../relational-databases/system-tables/dbo-sysproxies-transact-sql.md)  
 Enthält Informationen zu Proxykonten des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agents.  
  
 [dbo.sysproxylogin](../../relational-databases/system-tables/dbo-sysproxylogin-transact-sql.md)  
 Zeichnet auf, welche [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen den einzelnen Proxykonten des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agents zugeordnet sind.  
  
 [dbo.sysproxysubsystem](../../relational-databases/system-tables/dbo-sysproxysubsystem-transact-sql.md)  
 Zeichnet auf, welche [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Subsystem wird von den einzelnen Proxykonten verwendet.  
  
 [dbo.sysschedules](../../relational-databases/system-tables/dbo-sysschedules-transact-sql.md)  
 Enthält Informationen zu Auftragszeitplänen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agents.  
  
 [dbo.syssessions](../../relational-databases/system-tables/dbo-syssessions-transact-sql.md)  
 Enthält das Startdatum des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agents für jede [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agentsitzung. Mit jedem Start des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agentdiensts wird eine Sitzung erstellt.  
  
 [dbo.syssubsystems](../../relational-databases/system-tables/dbo-sysproxysubsystem-transact-sql.md)  
 Enthält Informationen zu allen verfügbaren Proxysubsystemen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agents.  
  
 [dbo.systargetservergroupmembers](../../relational-databases/system-tables/dbo-systargetservergroupmembers-transact-sql.md)  
 Zeichnet auf, welche Zielserver derzeit in dieser Multiservergruppe eingetragen sind.  
  
 [dbo.systargetservergroups](../../relational-databases/system-tables/dbo-systargetservergroups-transact-sql.md)  
 Zeichnet auf, welche Zielservergruppen derzeit in dieser Multiserverumgebung eingetragen sind.  
  
 [dbo.systargetservers](../../relational-databases/system-tables/dbo-systargetservers-transact-sql.md)  
 Zeichnet auf, welche Zielserver derzeit in dieser Domäne für Multiservervorgänge eingetragen sind.  
  
 [dbo.systaskids](../../relational-databases/system-tables/dbo-systaskids-transact-sql.md)  
 Enthält eine Zuordnung von in früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellten Tasks zu [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]-Aufträgen in der aktuellen Version.  
  
  
