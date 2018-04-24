---
title: Implementieren von Aufträgen | Microsoft-Dokumentation
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
- jobs [SQL Server Agent]
- SQL Server Agent jobs
- SQL Server Agent jobs, about jobs
- jobs [SQL Server Agent], about jobs
ms.assetid: 69e06724-25c7-4fb3-8a5b-3d4596f21756
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 0f16a99dd009d3e3e7e31349100aa26de82c890b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="implement-jobs"></a>Implementieren von Aufträgen
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Sie können [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Aufträge verwenden, um regelmäßig anfallende administrative Tasks zu automatisieren und periodisch ausführen, sodass die Effizienz der Verwaltung verbessert wird.  
  
Ein Auftrag besteht aus einer festgelegten Folge von Operationen, die der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent der Reihenfolge nach ausführt. Ein Auftrag kann eine Reihe von Aktivitäten ausführen, z. B. das Ausführen von [!INCLUDE[tsql](../../includes/tsql_md.md)] -Skripts, Befehlszeilenanwendungen, Microsoft ActiveX-Skripts, Integration Services-Paketen, Analysis Services-Befehlen und -Abfragen sowie Replikationstasks. Aufträge können wiederkehrende oder planbare Tasks ausführen, und sie können Benutzer durch Generieren von Warnungen automatisch über den Auftragsstatus informieren, sodass die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Verwaltung erheblich vereinfacht wird.  
  
Sie können einen Auftrag manuell ausführen oder ihn so konfigurieren, dass er gemäß einem Zeitplan oder als Reaktion auf Warnungen ausgeführt wird.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**Beschreibung**|**Thema**|  
|Enthält Informationen zum Erstellen von Aufträgen und Zuweisen des Besitz.|[Erstellen von Aufträgen](../../ssms/agent/create-jobs.md)|  
|Enthält Informationen zum Organisieren von Aufträgen in Kategorien.|[Organisieren von Aufträgen](../../ssms/agent/organize-jobs.md)|  
|Enthält Informationen zu den verschiedenen Auftragsschritten, die Sie erstellen können, und beschreibt, wie Sie diese Auftragsschritte verwalten.|[Verwalten von Auftragsschritten](../../ssms/agent/manage-job-steps.md)|  
|Enthält Informationen zur Definition des Auftragsbeginns sowie der Häufigkeit der Ausführung.|[Anlegen und Zuweisen von Zeitplänen zu Aufträgen](../../ssms/agent/create-and-attach-schedules-to-jobs.md)|  
|Enthält Informationen zur manuellen Ausführung von Aufträgen (ohne Zeitplan).|[Ausführen von Aufträgen](../../ssms/agent/run-jobs.md)|  
|Enthält Informationen zur Konfiguration des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents für die Reaktion auf Aufträge. Sie können den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent z. B. so konfigurieren, dass Administratoren bei der Beendigung von Aufträgen benachrichtigt werden.|[Angeben von Auftragsantworten](../../ssms/agent/specify-job-responses.md)|  
|Enthält Informationen zum Anzeigen vorhandener Aufträge, zum Auftragsverlauf nach der Ausführung und zum Ändern von Aufträgen.|[Anzeigen oder Ändern von Aufträgen](../../ssms/agent/view-or-modify-jobs.md)|  
|Enthält Informationen zum Löschen von Aufträgen.|[Löschen von Aufträgen](../../ssms/agent/delete-jobs.md)|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Implementieren der SQL Server-Agent-Sicherheit](../../ssms/agent/implement-sql-server-agent-security.md)  
  
