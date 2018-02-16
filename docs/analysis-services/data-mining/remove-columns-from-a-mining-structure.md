---
title: Entfernen Sie Spalten aus einer Miningstruktur | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mining structures [Analysis Services], columns
- removing columns
- deleting columns
- columns [data mining], mining structure columns
ms.assetid: 41073ffe-9351-416b-9f0c-62634bc213f9
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e9ef642c3d82331b3bbf9443a0f65181566dfe8c
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="remove-columns-from-a-mining-structure"></a>Entfernen von Spalten aus einer Miningstruktur
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Sie können mit dem Data Mining-Designer Spalten aus einer Miningstruktur entfernen, nachdem die Struktur bereits erstellt worden ist. Folgende Gründe könnten dafür sprechen, eine Miningstrukturspalte zu entfernen:  
  
-   Die Miningstruktur enthält mehrere Kopien einer Spalte, und Sie möchten die Verwendung doppelter Daten in einem Modell vermeiden.  
  
-   Die Daten sollten geschützt werden, doch Drillthrough wurde aktiviert.  
  
-   Die Daten werden nicht für Modellierungen verwendet und sollten nicht verarbeitet werden.  
  
 Durch Löschen einer Spalte aus der Miningstruktur wird die Spalte in der Datenquellensicht oder in den externen Daten nicht geändert. Nur Metadaten werden gelöscht. Wenn Sie jedoch die Spalten ändern, die in einer Miningstruktur verwendet werden, müssen Sie die Struktur und alle darauf basierenden Modelle erneut verarbeiten.  
  
### <a name="to-remove-a-column-from-the-mining-structure"></a>So entfernen Sie eine Spalte aus der Miningstruktur  
  
1.  Wählen Sie im Data Mining-Designer die Registerkarte **Miningstruktur** aus.  
  
2.  Erweitern Sie die Struktur für die Miningstruktur, um alle Spalten anzuzeigen.  
  
3.  Klicken Sie mit der rechten Maustaste auf die Spalte, die Sie löschen möchten, und wählen Sie anschließend **Löschen**aus.  
  
4.  Klicken Sie im Dialogfeld **Objekte löschen** auf **OK**.  
  
## <a name="see-also"></a>Siehe auch  
 [Tasks und Anweisungen für Miningstrukturen](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  
