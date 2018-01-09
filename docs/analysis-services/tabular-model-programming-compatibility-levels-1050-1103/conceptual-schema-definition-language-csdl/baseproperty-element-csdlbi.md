---
title: BaseProperty-Element (CSDLBI) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: d0f63e52-7330-4b2c-a929-7a517acc6921
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7f28d100ef59df6fe73b8dd93d1fbfebdb87bbb7
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="baseproperty-element-csdlbi"></a>BaseProperty-Element (CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Das BaseProperty-Element ist ein komplexer Typ, der als Basis für andere Elemente dient.  
  
 Seine Attribute können in den Spalten und Measures angezeigt werden.  
  
## <a name="elements-and-attributes"></a>Elemente und Attribute  
 In der folgenden Tabelle sind die Elemente und Attribute aufgeführt, die das BaseProperty-Element definieren.  
  
|Name|Ist erforderlich|Description|  
|----------|-----------------|-----------------|  
|Ausrichtung|nein|Der Name für das Element (Spalte, Measure, Navigationseigenschaft, Hierarchie oder Ebene), das von der Implementierung des Member-Typs definiert wird.|  
|FormatString|nein|Der Anzeigename für das Element.|  
|IsRightToLeft|nein|Ein boolescher Wert, der angibt, ob das Feld Text enthält, der von rechts nach links gelesen werden kann.<br /><br /> Wenn dieses Attribut weggelassen wird, wird die Standardeinstellung (des Modells) verwendet.|  
|SortDirection|nein|Ein Wert, der angibt, wie die Feldwerte normalerweise sortiert werden. Die Inhalte dieses Attributs werden vom einfachen Typ SortDirection definiert.<br /><br /> Wenn das Attribut nicht angegeben wird, wird eine Sortierrichtung auf Grundlage des Datentyps des Felds zugewiesen.|  
|Einheiten|nein|Das Symbol, das für Feldwerte zur Darstellung von Einheiten übernommen wird.<br /><br /> Wenn kein Wert angegeben ist, sind die Einheiten unbekannt.|  
  
## <a name="alignment-element"></a>Alignment-Element  
 Mit diesem einfachen Typ wird das Namensformat definiert, das verwendet wird, um Elemente zu unterscheiden.  
  
|value|Description|  
|-----------|-----------------|  
|InclusionThresholdSetting|Verwenden Sie den Attributnamen.|  
|Kontext|Verwenden Sie den Namen der eingehenden Beziehung.|  
|Merge|Verketten Sie den Namen der eingehenden Beziehung und den Eigenschaftsnamen gemäß den Regeln der aktuellen Grammatik.|  
  
## <a name="sortdirection-element"></a>SortDirections-Element  
 Mit diesem einfachen Typ wird das Namensformat definiert, das verwendet wird, um Elemente zu unterscheiden.  
  
|value|Description|  
|-----------|-----------------|  
|InclusionThresholdSetting|Verwenden Sie den Attributnamen.|  
|Kontext|Verwenden Sie den Namen der eingehenden Beziehung.|  
|Merge|Verketten Sie den Namen der eingehenden Beziehung und den Namen der Eigenschaft.|  
  
## <a name="see-also"></a>Siehe auch  
 [Informationen zum tabellarischen Objektmodell auf Kompatibilität Ebenen 1050 bis 1103](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
  
