---
title: "Ausschließen einer Spalte aus einem Miningmodell | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- excluding mining model columns
- mining models [Analysis Services], columns
- columns [data mining], excluding
ms.assetid: 404fe5fe-3ba2-4b9b-8780-0d02343d467f
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a12584791ec8ea21a1338c09dbc0e5f7ef8f7a62
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="exclude-a-column-from-a-mining-model"></a>Ausschließen einer Spalte aus einem Miningmodell
  Wenn Sie ein neues Miningmodell erstellen, möchten Sie möglicherweise nicht alle Spalten verwenden, die in der Miningstruktur vorhanden sind, auf der das Modell basiert. Beispiel: Sie haben möglicherweise eine Kundennamenspalte für einen Drillthroughvorgang hinzugefügt, möchten sie jedoch nicht für Modellierungen verwenden. Unter Umständen möchten Sie auch mehrere Kopien einer Spalte mit verschiedenen Diskretisierungen erstellen und in jedem Modell nur eine Kopie verwenden und die restlichen Objekte ignorieren. Sie könnten auch Eingabespalten in mehreren verschiedenen Modellen selektiv hinzufügen, um zu erkennen, wie die hinzugefügte Variable die Ausgabespalte beeinflusst.  
  
 Sie müssen keine neue Miningstruktur für jede Kombination von Spalten erstellen, sondern es genügt, wenn Sie eine Spalte so kennzeichnen, dass sie nicht in einem bestimmten Modell verwendet wird.  
  
### <a name="to-exclude-a-column-from-a-mining-model"></a>So schließen Sie eine Spalte aus einem Miningmodell aus  
  
1.  Wählen Sie in der Registerkarte **Miningmodelle** des Data Mining-Designers in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]unter dem entsprechenden Miningmodell die Zelle aus, die der Spalte entspricht, die ausgeschlossen werden soll.  
  
2.  Wählen Sie im Dropdown-Listenfeld **Ignorieren** aus.  
  
## <a name="see-also"></a>Siehe auch  
 [Miningmodelltasks und Anweisungen](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  

