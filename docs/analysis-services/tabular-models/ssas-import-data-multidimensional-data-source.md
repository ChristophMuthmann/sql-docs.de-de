---
title: "Importieren aus einer mehrdimensionalen Datenquelle (SSAS – tabellarisch) | Microsoft Docs"
ms.custom: 
ms.date: 05/22/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7f0793ea-a4c7-42e9-b722-2164a454ebca
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4aaa43e745c86cd493279fe8bd875d376f8185c0
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="import-data---multidimensional-data-source"></a>Importieren von Daten per Push – mehrdimensionalen Datenquelle
  Sie können eine Analysis Services-Cubedatenbank als Datenquelle für ein tabellarisches Modell verwenden. Um Daten aus einem Analysis Services-Cube zu importieren, müssen Sie eine MDX-Abfrage zur Auswahl der zu importierenden Daten definieren.  
  
 Alle Daten, die in einer SQL Server Analysis Services-Datenbank enthalten sind, können in ein Modell importiert werden. Sie können die gesamte oder einen Teil einer Dimension extrahieren oder Slices und Aggregate aus dem Cube abrufen, z. B. die Summe der monatlichen Verkäufe für das aktuelle Jahr usw. Beachten Sie jedoch, dass alle Daten, die Sie aus einem Cube importieren, vereinfacht werden. Wenn Sie eine Abfrage definieren, die Measures aus mehreren Dimensionen abruft, werden die Daten daher für jede Dimension in eine separate Spalte importiert.  
  
 Analysis Services-Cubes müssen die Version SQL Server 2005, SQL Server 2008, SQL Server 2008 R2, [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]oder [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]aufweisen.  
  
### <a name="to-import-data-from-an-analysis-services-cube"></a>So importieren Sie Daten aus einem Analysis Services-Cube  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]auf das Menü **Modell** und dann auf **Aus Datenquelle importieren**.  
  
2.  Wählen Sie auf der Seite **Mit einer Datenquelle verbinden** die Option **Microsoft Analysis Services**aus, und klicken Sie dann auf **Weiter**.  
  
3.  Führen Sie die Schritte im Tabellenimport-Assistenten aus. Auf der Seite **MDX-Abfrage angeben** können Sie eine MDX-Abfrage angeben. Zur Verwendung des MDX-Abfrage-Designers klicken Sie auf der Seite **MDX-Abfrage angeben**auf Entwurf.  
  
## <a name="see-also"></a>Siehe auch  
 [Importieren von Daten &#40;SSAS – tabellarisch&#41;](http://msdn.microsoft.com/library/6617b2a2-9f69-433e-89e0-4c5dc92982cf)   
 [Unterstützte Datenquellen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)  
  
  
