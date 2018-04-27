---
title: Statistiken aktualisieren (Task) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/04/2017
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
- sql13.dts.designer.updatestatisticstask.f1
helpviewer_keywords:
- updating statistics
- Update Statistics task [Integration Services]
ms.assetid: 0247483b-f092-4511-8fa8-3610108bd1bc
caps.latest.revision: 45
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6a457cb267f78b5694cbb2d0bb0359a41097acd6
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="update-statistics-task"></a>Statistiken aktualisieren (Task)
  Der Task "Statistiken aktualisieren" aktualisiert Informationen zur Verteilung von Schlüsselwerten für eine oder mehrere Statistikgruppen (Auflistungen) in der angegebenen Tabelle oder indizierten Sicht. Weitere Informationen finden Sie unter [Statistics](../../relational-databases/statistics/statistics.md).  
  
 Mithilfe des Tasks Statistiken aktualisieren kann ein Paket Statistiken für eine einzelne Datenbank oder mehrere Datenbanken aktualisieren. Falls mit dem Task nur die Statistiken in einer einzelnen Datenbank aktualisiert werden, können Sie die Sichten oder Tabellen auswählen, deren Statistiken aktualisiert werden. Sie können das Update so konfigurieren, dass alle Statistiken, nur Spaltenstatistiken oder nur Indexstatistiken aktualisiert werden.  
  
 Dieser Task kapselt eine UPDATE STATISTICS-Anweisung, einschließlich der folgenden Argumente und Klauseln:  
  
-   Das Argument *table_name* oder *view_name* .  
  
-   Wenn alle Statistiken aktualisiert werden, wird die WITH ALL-Klausel verwendet.  
  
-   Wenn nur Spalten aktualisiert werden, wird die WITH COLUMN-Klausel verwendet.  
  
-   Wenn nur Indizes aktualisiert werden, wird die WITH INDEX-Klausel verwendet.  
  
 Wenn der Task Statistiken aktualisieren Statistiken in mehreren Datenbanken aktualisiert, werden mehrere UPDATE STATISTICS-Anweisungen ausgeführt, wobei pro Tabelle oder Sicht eine Anweisung ausgeführt wird. Alle Instanzen von UPDATE STATISTICS verwenden dieselbe Klausel aber unterschiedliche Werte für *table_name* oder *view_name*. Weitere Informationen finden Sie unter [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md) und [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md).  
  
> [!IMPORTANT]  
>  Die Zeit, die der Task zum Erstellen der vom Task ausgeführten Transact-SQL-Anweisung benötigt, ist proportional zur Anzahl der vom Task aktualisierten Statistiken. Falls für den Task konfiguriert ist, dass die Statistiken in allen Tabellen und Sichten in einer Datenbank mit vielen Indizes aktualisiert werden, oder dass Statistiken in mehreren Datenbanken aktualisiert werden, kann das Generieren der Transact-SQL-Anweisung lange dauern.  
  
## <a name="configuration-of-the-update-statistics-task"></a>Konfiguration des Tasks "Statistiken aktualisieren"  
 Eigenschaften können Sie mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen. Dieser Task ist im **-Designer in der** Toolbox **im Abschnitt** Wartungsplantasks [!INCLUDE[ssIS](../../includes/ssis-md.md)] enthalten.  
  
 Klicken Sie auf das folgende Thema, um Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [Task „Statistiken aktualisieren“ &#40;Wartungsplan&#41;](../../relational-databases/maintenance-plans/update-statistics-task-maintenance-plan.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum Festlegen dieser Eigenschaften im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer zu erhalten:  
  
-   [Festlegen der Eigenschaften eines Tasks oder Containers](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Integration Services-Tasks](../../integration-services/control-flow/integration-services-tasks.md)   
 [Ablaufsteuerung](../../integration-services/control-flow/control-flow.md)  
  
  
