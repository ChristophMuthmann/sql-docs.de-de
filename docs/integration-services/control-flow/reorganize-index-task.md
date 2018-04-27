---
title: Index neu organisieren (Task) | Microsoft-Dokumentation
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
- sql13.dts.designer.reorganizeindextask.f1
helpviewer_keywords:
- reorganizing indexes
- Reorganize Index task [Integration Services]
- indexes [Integration Services]
ms.assetid: 9ed87861-e5c3-4fcd-8760-d112f4c0af0c
caps.latest.revision: 43
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cc44085d2fa5724729e5fd6d4a0968587155e664
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="reorganize-index-task"></a>Index neu organisieren (Task)
  Mit dem Task Index neu organisieren werden Indizes in Tabellen und Sichten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbanken neu organisiert. Weitere Informationen zum Verwalten von Indizes finden Sie unter [Neuorganisieren und Neuerstellen von Indizes](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).  
  
 Mithilfe des Tasks Index neu organisieren kann ein Paket Indizes in einer einzelnen Datenbank oder mehreren Datenbanken neu organisieren. Falls mit dem Task nur die Indizes in einer einzelnen Datenbank neu organisiert werden, können Sie die Sichten oder Tabellen auswählen, deren Indizes neu organisiert werden. Der Task Index neu organisieren schließt außerdem eine Option zum Komprimieren von großen Objekten ein. Große Objekte (LOB; Large Object) sind Daten mit dem Datentyp **image**, **text**, **ntext**, **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, oder **xml**. Weitere Informationen finden Sie unter [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md).  
  
 Der Task Index neu organisieren kapselt die ALTER INDEX-Anweisung von Transact-SQL. Wenn Sie große Objekte komprimieren möchten, verwendet die Anweisung die REORGANIZE WITH (LOB_COMPACTION = ON)-Klausel. Andernfalls ist LOB_COMPACTION auf OFF festgelegt. Weitere Informationen finden Sie unter [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).  
  
> [!IMPORTANT]  
>  Die Zeit, die der Task zum Erstellen der vom Task ausgeführten Transact-SQL-Anweisung benötigt, ist proportional zur Anzahl der vom Task neu organisierten Indizes. Falls für den Task konfiguriert ist, dass die Indizes in allen Tabellen und Sichten in einer Datenbank mit vielen Indizes neu organisiert werden, oder dass Indizes in mehreren Datenbanken neu organisiert werden, kann das Generieren der Transact-SQL-Anweisung lange dauern.  
  
## <a name="configuration-of-the-reorganize-index-task"></a>Konfiguration des Tasks "Index neu organisieren"  
 Eigenschaften können Sie mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen. Dieser Task ist im **-Designer in der** Toolbox **im Abschnitt** Wartungsplantasks [!INCLUDE[ssIS](../../includes/ssis-md.md)] enthalten.  
  
 Klicken Sie auf das folgende Thema, um Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [Task „Index neu organisieren“ &#40;Wartungsplan&#41;](../../relational-databases/maintenance-plans/reorganize-index-task-maintenance-plan.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Weitere Informationen zum Anzeigen dieser Eigenschaften im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer finden Sie unter [Festlegen der Eigenschaften eines Tasks oder Containers](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Integration Services-Tasks](../../integration-services/control-flow/integration-services-tasks.md)   
 [Ablaufsteuerung](../../integration-services/control-flow/control-flow.md)  
  
  
