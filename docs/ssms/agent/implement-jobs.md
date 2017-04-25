---
title: "Implementieren von Aufträgen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
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
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 30b61e4aa32828763d4531c53cb7f308a926798b
ms.lasthandoff: 04/11/2017

---
# <a name="implement-jobs"></a>Implementieren von Aufträgen
Sie können [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-Agent-Aufträge verwenden, um regelmäßig anfallende administrative Tasks zu automatisieren und periodisch ausführen, sodass die Effizienz der Verwaltung verbessert wird.  
  
Ein Auftrag besteht aus einer festgelegten Folge von Operationen, die der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent der Reihenfolge nach ausführt. Ein Auftrag kann eine Reihe von Aktivitäten ausführen, z. B. das Ausführen von [!INCLUDE[tsql](../../includes/tsql_md.md)] -Skripts, Befehlszeilenanwendungen, Microsoft ActiveX-Skripts, Integration Services-Paketen, Analysis Services-Befehlen und -Abfragen sowie Replikationstasks. Aufträge können wiederkehrende oder planbare Tasks ausführen, und sie können Benutzer durch Generieren von Warnungen automatisch über den Auftragsstatus informieren, sodass die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Verwaltung erheblich vereinfacht wird.  
  
Sie können einen Auftrag manuell ausführen oder ihn so konfigurieren, dass er gemäß einem Zeitplan oder als Reaktion auf Warnungen ausgeführt wird.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
|||  
|-|-|  
|**Description**|**Thema**|  
|Enthält Informationen zum Erstellen von Aufträgen und Zuweisen des Besitz.|[Erstellen von Aufträgen](../../ssms/agent/create-jobs.md)|  
|Enthält Informationen zum Organisieren von Aufträgen in Kategorien.|[Organisieren von Aufträgen](../../ssms/agent/organize-jobs.md)|  
|Enthält Informationen zu den verschiedenen Auftragsschritten, die Sie erstellen können, und beschreibt, wie Sie diese Auftragsschritte verwalten.|[Verwalten von Auftragsschritten](../../ssms/agent/manage-job-steps.md)|  
|Enthält Informationen zur Definition des Auftragsbeginns sowie der Häufigkeit der Ausführung.|[Anlegen und Zuweisen von Zeitplänen zu Aufträgen](../../ssms/agent/create-and-attach-schedules-to-jobs.md)|  
|Enthält Informationen zur manuellen Ausführung von Aufträgen (ohne Zeitplan).|[Ausführen von Aufträgen](../../ssms/agent/run-jobs.md)|  
|Enthält Informationen zur Konfiguration des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents für die Reaktion auf Aufträge. Sie können den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent z. B. so konfigurieren, dass Administratoren bei der Beendigung von Aufträgen benachrichtigt werden.|[Angeben von Auftragsantworten](../../ssms/agent/specify-job-responses.md)|  
|Enthält Informationen zum Anzeigen vorhandener Aufträge, zum Auftragsverlauf nach der Ausführung und zum Ändern von Aufträgen.|[Anzeigen oder Ändern von Aufträgen](../../ssms/agent/view-or-modify-jobs.md)|  
|Enthält Informationen zum Löschen von Aufträgen.|[Löschen von Aufträgen](../../ssms/agent/delete-jobs.md)|  
  
## <a name="see-also"></a>Siehe auch  
[Implementieren der SQL Server-Agent-Sicherheit](../../ssms/agent/implement-sql-server-agent-security.md)  
  

