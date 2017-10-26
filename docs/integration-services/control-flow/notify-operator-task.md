---
title: Benachrichtigen Sie die Task "Operator" | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.notifyoperatortask.f1
helpviewer_keywords:
- Notify Operator task
- notifications [Integration Services]
- SQL Server Agent [Integration Services]
ms.assetid: 6c816c68-c6d6-44e4-bb34-c8e060a958a1
caps.latest.revision: 43
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fb791195dccb44add2d1b196e33e03d3a45d7049
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="notify-operator-task"></a>Operator benachrichtigen (Task)
  Der Task Operator benachrichtigen sendet Benachrichtigungsmeldungen an [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agentoperatoren. Bei einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agentoperator handelt es sich um einen Alias für eine Person oder Gruppe, die elektronische Benachrichtigungen empfangen kann. Weitere Informationen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Operatoren finden Sie unter [Operatoren](http://msdn.microsoft.com/library/38e8488f-2669-4cea-b9c3-5f394a663678).  
  
 Mit dem Task „Operator benachrichtigen“ kann ein Paket mindestens einen Operator per E-Mail, Pager oder **net send**benachrichtigen. Jeder Operator kann mit verschiedenen Methoden benachrichtigt werden. Beispielsweise wird OperatorA per E-Mail und Pager benachrichtigt, OperatorB dagegen per Pager und **net send**. Die Operatoren, die Benachrichtigungen vom Task erhalten, müssen Mitglieder der **OperatorNotify** -Auflistung im Task Operator benachrichtigen sein.  
  
 Der Task "Operator benachrichtigen" ist der einzige Datenbankwartungstask, der keine Transact-SQL-Anweisung und keinen DBCC-Befehl kapselt.  
  
## <a name="configuration-of-the-notify-operator-task"></a>Konfiguration des Tasks "Operator benachrichtigen"  
 Eigenschaften können Sie mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen. Dieser Task ist im **-Designer in der** Toolbox **im Abschnitt** Wartungsplantasks [!INCLUDE[ssIS](../../includes/ssis-md.md)] enthalten.  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [Task „Operator benachrichtigen“ &#40;Wartungsplan&#41;](../../relational-databases/maintenance-plans/notify-operator-task-maintenance-plan.md)  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum Festlegen dieser Eigenschaften im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer zu erhalten:  
  
-   [Festlegen der Eigenschaften eines Tasks oder Containers](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
  

