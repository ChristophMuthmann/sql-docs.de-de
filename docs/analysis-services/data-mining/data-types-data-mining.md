---
title: Datentypen (Datamining) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
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
- data types [data mining]
- columns [data mining], data types
- data mining [Analysis Services], data types
ms.assetid: 4af5b7db-790b-459c-b2b4-00f0cf6b5ce4
caps.latest.revision: "47"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7e5d09435546cf0605bb7b70a685021612fd2f9b
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="data-types-data-mining"></a>Datentypen (Data Mining)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Beim Erstellen eines Miningmodells oder einer Miningstruktur in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], müssen Sie die Datentypen für jede Spalte in der Miningstruktur definieren. Anhand des Datentyps erkennt das Analysemodul, ob es sich bei den Daten in der Datenquelle um numerische Daten oder um Text handelt und wie die Daten verarbeitet werden sollen. Wenn die Datenquelle beispielsweise numerische Daten enthält, können Sie angeben, ob die Zahlen als ganze Zahlen oder durch Verwendung von Dezimalstellen verarbeitet werden sollen.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] unterstützt die folgenden Datentypen für Miningstrukturspalten:  
  
|Datentyp|Unterstützte Inhaltstypen|  
|---------------|-----------------------------|  
|**Text**|Zyklisch, Diskret, Diskretisiert, Key Sequence, Sortiert, Sequenz|  
|**Long**|Kontinuierlich, Zyklisch, Diskret, Diskretisiert, Schlüssel, Key Sequence, Key Time, Sortiert, Sequenz, Zeit<br /><br /> Classified|  
|**Boolean**|Zyklisch, Diskret, Sortiert|  
|**Double**|Kontinuierlich, Zyklisch, Diskret, Diskretisiert, Schlüssel, Key Sequence, Key Time, Sortiert, Sequenz, Zeit<br /><br /> Classified|  
|**Datum**|Kontinuierlich, Zyklisch, Diskret, Diskretisiert, Schlüssel, Key Sequence, Key Time, Sortiert|  
  
> [!NOTE]  
>  Die Time- und Sequence-Inhaltstypen werden nur von Algorithmen von Drittanbietern unterstützt. Die Inhaltstypen Zyklisch und Sortiert  werden unterstützt, die meisten Algorithmen behandeln sie jedoch als diskrete Werte und führen keine spezielle Verarbeitung durch.  
  
 Die Tabelle zeigt auch die für jeden Datentyp unterstützten *Inhaltstypen* an.  
  
 Die Angabe des Inhaltstyp ist für Data Mining spezifisch, und Sie können damit die Art und Weise, wie Daten im Miningmodell verarbeitet oder berechnet werden, anpassen. Wenn Ihre Spalte z.B. Zahlen enthält, müssen Sie diese möglicherweise als diskrete Werte modellieren. Wenn die Spalte Zahlen enthält, können Sie auch angeben, dass diese klassifiziert oder diskretisiert werden. Alternativ können Sie angeben, dass das Modell sie als kontinuierliche Werte behandeln soll. Folglich kann der Inhaltstyp einen enormen Einfluss auf das Modell haben. Eine Liste aller Inhaltstypen finden Sie unter [Inhaltstypen &#40;Data Mining&#41;](../../analysis-services/data-mining/content-types-data-mining.md).  
  
> [!NOTE]  
>  In anderen Computerlernsystemen treten möglicherweise die Begriffe *nominale Daten*, *Faktoren* oder *Kategorien*, *ordinale Daten*oder *Sequenzdaten*auf. Im Allgemeinen entsprechen diese den Inhaltstypen. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]bestimmt der Datentyp nur die Art und Weise der Speicherung des Datenwerts und nicht dessen Verwendung im Modell.  
  
## <a name="specifying-a-data-type"></a>Angeben eines Datentyps  
 Wenn Sie das Miningmodell direkt mithilfe der Data Mining-Erweiterungen (DMX) erstellen, können Sie den Datentyp für die einzelnen Spalten zusammen mit dem Modell definieren. Analysis Services erstellt dann gleichzeitig die entsprechende Miningstruktur mit den angegebenen Datentypen. Wenn Sie das Miningmodell oder die Miningstruktur mit einem Assistenten erstellen, schlägt Analysis Services einen Datentyp vor, oder Sie können einen Datentyp in einer Liste auswählen.  
  
## <a name="changing-a-data-type"></a>Ändern eines Datentyps  
 Wenn Sie den Datentyp einer Spalte ändern, müssen die Miningstruktur und alle auf dieser Struktur basierenden Miningmodelle neu verarbeitet werden. Beim Ändern des Datentyps kann es vorkommen, dass die jeweilige Spalte nicht mehr in einem bestimmten Modell verwendet werden kann. In diesem Fall gibt Analysis Services beim erneuten Verarbeiten entweder einen Fehler aus, oder das Modell wird unter Auslassung der Spalte verarbeitet.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Inhaltstypen &#40;Data Mining&#41;](../../analysis-services/data-mining/content-types-data-mining.md)   
 [Inhaltstypen &#40;DMX&#41;](../../dmx/content-types-dmx.md)   
 [Data Mining-Algorithmen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Miningstrukturen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [Datentypen &#40; DMX &#41;](../../dmx/data-types-dmx.md)   
 [Miningmodellspalten](../../analysis-services/data-mining/mining-model-columns.md)   
 [Miningstrukturspalten](../../analysis-services/data-mining/mining-structure-columns.md)  
  
  
