---
title: Erstellen von Aufträgen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- jobs [SQL Server Agent], creating
- SQL Server Agent jobs, creating
ms.assetid: 465fb7fc-7622-4252-a178-ea51691c935b
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: fa49591e0004b4cf77a7997dd3c15d84c86516c0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="create-jobs"></a>Erstellen von Aufträgen
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Ein Auftrag besteht aus einer festgelegten Folge von Operationen, die der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-Agent der Reihenfolge nach ausführt. Über einen Auftrag können zahlreiche Aktivitäten ausgeführt werden, u. a. das Ausführen von [!INCLUDE[tsql](../../includes/tsql_md.md)] -Skripts, Eingabeaufforderungsanwendungen, Microsoft ActiveX-Skripts, Integration Services-Paketen, Analysis Services-Befehlen und -abfragen bzw. Replikationstasks. Aufträge können wiederholte oder planbare Tasks ausführen, und sie können Benutzer in Form von Warnungen hinsichtlich des Auftragsstatus benachrichtigen. Dies führt zu einer deutlichen Vereinfachung der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Verwaltung.  
  
Um einen Auftrag erstellen zu können, muss ein Benutzer Mitglied einer der festen Datenbankrollen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents oder Mitglied der festen Serverrolle **sysadmin** sein. Ein Auftrag kann nur von seinem Besitzer bzw. Mitgliedern der **sysadmin** -Rolle bearbeitet werden. Mitglieder der **sysadmin** -Rolle können anderen Benutzern den Auftragsbesitz zuweisen und sämtliche Aufträge ausführen, ungeachtet des Auftragsbesitzers. Weitere Informationen zu den festen Datenbankrollen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents finden Sie unter [Feste Datenbankrollen des SQL Server-Agents](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
Aufträge können so geschrieben werden, dass sie auf der lokalen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder auf mehreren Instanzen in einem Unternehmen ausgeführt werden. Zum Ausführen von Aufträgen auf mehreren Servern müssen Sie mindestens einen Masterserver und einen oder mehrere Zielserver einrichten. Weitere Informationen zu Master- und Zielservern finden Sie unter [Automatisierte Verwaltung in einem Unternehmen](../../ssms/agent/automated-administration-across-an-enterprise.md).  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent zeichnet die Informationen von Aufträgen und Auftragsschritten im Auftragsverlauf auf.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**Beschreibung**|**Thema**|  
|Beschreibt, wie ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Auftrag erstellt wird.|[Erstellen eines Auftrags](../../ssms/agent/create-a-job.md)|  
|Beschreibt, wie Sie den Besitz eines [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Auftrags einem anderen Benutzer neu zuweisen können.|[Give Others Ownership of a Job](../../ssms/agent/give-others-ownership-of-a-job.md)|  
|Beschreibt, wie Sie das Auftragsverlaufsprotokoll des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents einrichten.|[Set Up the Job History Log](../../ssms/agent/set-up-the-job-history-log.md)|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Verwalten von Auftragsschritten](../../ssms/agent/manage-job-steps.md)  
[Automatisierte Verwaltung in einem Unternehmen](../../ssms/agent/automated-administration-across-an-enterprise.md)  
[Anlegen und Zuweisen von Zeitplänen zu Aufträgen](../../ssms/agent/create-and-attach-schedules-to-jobs.md)  
[Ausführen von Aufträgen](../../ssms/agent/run-jobs.md)  
[Anzeigen oder Ändern von Aufträgen](../../ssms/agent/view-or-modify-jobs.md)  
  
