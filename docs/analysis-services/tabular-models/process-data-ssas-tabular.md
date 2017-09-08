---
title: "Verarbeiten von Daten (SSAS – tabellarisch) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d88f2dc9-2933-4be5-9bf3-48ffbc2d0a1a
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6fc5d0e934ae7fe4d7f9a00594c2f1ffd21bda1c
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="process-data-ssas-tabular"></a>Verarbeiten von Daten (SSAS – tabellarisch)
  Wenn Sie Daten im Modus mit Zwischenspeicherung in ein Tabellenmodell importieren, zeichnen Sie eine Momentaufnahme der Daten zum Zeitpunkt des Imports auf. In einigen Fällen ändern sich diese Daten möglicherweise nie und müssen im Modell nicht aktualisiert werden. Es ist jedoch wahrscheinlicher, dass sich die Daten, aus denen Daten importiert werden, regelmäßig ändern. Damit das Modell jedoch immer die neuesten Daten aus den Datenquellen widerspiegelt, ist es erforderlich, die Daten zu verarbeiten (zu aktualisieren) und berechnete Daten neu zu berechnen. Um die Daten im Modell zu aktualisieren, führen Sie eine Verarbeitungsaktion für alle Tabellen, eine einzelne Tabelle, eine Partition oder eine Datenquellenverbindung aus.  
  
 Beim Erstellen des Modellprojekts müssen alle Verarbeitungsaktionen manuell in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]initiiert werden. Nachdem ein Modell bereitgestellt wurde, können Verarbeitungsvorgänge mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ausgeführt oder mit einem Skript geplant werden. Die hier beschriebenen Tasks beziehen sich auf Verarbeitungsaktionen, die Sie während der Modellerstellung in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]ausführen können. Weitere Informationen zu Verarbeitungsaktionen für ein bereitgestelltes Modell finden Sie unter [Verarbeiten von Datenbank, Tabelle oder Partition &#40;Analysis Services&#41;](../../analysis-services/tabular-models/process-database-table-or-partition-analysis-services.md).  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
|Thema|Description|  
|-----------|-----------------|  
|[Manuelle Verarbeitung von Daten &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/manually-process-data-ssas-tabular.md)|Beschreibt, wie Arbeitsbereichsdaten eines Modells manuell verarbeitet werden.|  
|[Problembehandlung von Verarbeitungsdaten &#40;SSAS – tabellarisch&#41;](../../analysis-services/troubleshoot-process-data-ssas-tabular.md)|Beschreibt die Problembehandlung für Verarbeitungsvorgänge.|  
  
  
