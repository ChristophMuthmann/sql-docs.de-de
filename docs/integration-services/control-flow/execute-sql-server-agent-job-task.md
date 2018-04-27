---
title: Auftrag des SQL Server-Agents ausführen (Task) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: control-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.designer.executesqlserveragentjobtask.f1
helpviewer_keywords:
- Execute SQL Server Agent Job task [Integration Services]
- jobs [Integration Services]
- SQL Server Agent [Integration Services]
ms.assetid: 3aa3bc0e-1a1c-452e-81b8-b4e3422ea053
caps.latest.revision: 44
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5218978c138dde2aea4a32b26d6ed5cd50e1b307
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="execute-sql-server-agent-job-task"></a>Auftrag des SQL Server-Agents ausführen (Task)
  Mit dem Task Auftrag des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents ausführen werden Aufträge des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents ausgeführt. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent ist ein [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Dienst, der in einer Instanz von SQL Server definierte Aufträge ausführt. Sie können Aufträge erstellen, die Transact-SQL-Anweisungen, ActiveX-Skripts, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] - und Replikationswartungstasks sowie Pakete ausführen. Sie können auch einen Auftrag zum Überwachen von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und zum Auslösen von Warnungen konfigurieren. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agentaufträge werden in der Regel zum Automatisieren von Tasks verwendet, die Sie wiederholt ausführen. Weitere Informationen finden Sie unter [Implementieren von Aufträgen](http://msdn.microsoft.com/library/69e06724-25c7-4fb3-8a5b-3d4596f21756).  
  
 Mithilfe des Tasks Auftrag des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents ausführen kann ein Paket administrative Tasks im Zusammenhang mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Komponenten ausführen. Beispielsweise kann mit einem Auftrag des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents eine gespeicherte Systemprozedur, wie z.B. **sp_enum_dtspackages** , ausgeführt werden, um eine Liste der Pakete in einem Ordner abzurufen.  
  
> [!NOTE]  
>  Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent muss ausgeführt werden, damit lokale oder Multiserververwaltungsaufgaben automatisch ausgeführt werden können.  
  
 Dieser Task kapselt die Systemprozedur **sp_start_job** und übergibt den Namen des Auftrags des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents als Argument an die Prozedur. Weitere Informationen finden Sie unter [sp_start_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md).  
  
## <a name="configuring-the-execute-sql-server-agent-job-task"></a>Konfigurieren des Tasks Auftrag des SQL Server-Agents ausführen  
 Eigenschaften können Sie mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen. Dieser Task ist im **-Designer in der** Toolbox **im Abschnitt** Wartungsplantasks [!INCLUDE[ssIS](../../includes/ssis-md.md)] enthalten.  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [Task „Auftrag des SQL Server-Agents ausführen“ &#40;Wartungsplan&#41;](../../relational-databases/maintenance-plans/execute-sql-server-agent-job-task-maintenance-plan.md)  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum Festlegen dieser Eigenschaften im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer zu erhalten:  
  
-   [Festlegen der Eigenschaften eines Tasks oder Containers](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
  
