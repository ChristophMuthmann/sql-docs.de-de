---
title: "Task T-SQL-Anweisung ausführen | Microsoft Docs"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.executetsqlstatementtask.f1
helpviewer_keywords:
- Transact-SQL statements, SSIS
- statements [Integration Services]
- Execute T-SQL Statement task [Integration Services]
ms.assetid: 7e9086ca-d27e-46c0-bfad-d61333ebd55e
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 94fd411504f1781041e8d36f3f1cf41f6082aa09
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="execute-t-sql-statement-task"></a>T-SQL-Anweisung ausführen (Task)
  Mit dem Task T-SQL-Anweisung ausführen werden Transact-SQL-Anweisungen ausgeführt. Weitere Informationen finden Sie unter [Transact-SQL-Referenz &#40;Datenbankmodul&#41;](../../t-sql/transact-sql-reference-database-engine.md) und [Integration Services-Abfragen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-queries.md).  
  
 Dieser Task ist mit dem Task SQL ausführen vergleichbar. Der Task T-SQL-Anweisung ausführen unterstützt jedoch nur die Transact-SQL-Version der SQL-Sprache und kann nicht zum Ausführen von Anweisungen auf Servern verwendet werden, die andere Dialekte der SQL-Sprache verwenden. Falls Sie parametrisierte Abfragen ausführen müssen, speichern Sie die Abfrageergebnisse in Variablen, oder verwenden Sie Eigenschaftsausdrücke. Sie sollten den Task SQL ausführen anstelle des Tasks T-SQL-Anweisung ausführen verwenden. Weitere Informationen finden Sie unter [Execute SQL Task](../../integration-services/control-flow/execute-sql-task.md).  
  
## <a name="configuration-of-the-execute-t-sql-task"></a>Konfiguration des Tasks "T-SQL-Anweisung ausführen"  
 Eigenschaften können Sie mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen. Dieser Task ist im **-Designer in der** Toolbox **im Abschnitt** Wartungsplantasks [!INCLUDE[ssIS](../../includes/ssis-md.md)] enthalten.  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [Task „T-SQL-Anweisung ausführen“ &#40;Wartungsplan&#41;](../../relational-databases/maintenance-plans/execute-t-sql-statement-task-maintenance-plan.md)  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum Festlegen dieser Eigenschaften im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer zu erhalten:  
  
-   [Festlegen der Eigenschaften eines Tasks oder Containers](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="see-also"></a>Siehe auch  
 [Integration Services-Tasks](../../integration-services/control-flow/integration-services-tasks.md)   
 [Ablaufsteuerung](../../integration-services/control-flow/control-flow.md)   
 [MERGE in Integrationsservices-Paketen](../../integration-services/control-flow/merge-in-integration-services-packages.md)  
  
  

