---
title: BaseProperty-Element (CSDLBI) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: d0f63e52-7330-4b2c-a929-7a517acc6921
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b82b9b6f137b09768fbfdadb78d98f9cd293e81e
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="baseproperty-element-csdlbi"></a>BaseProperty-Element (CSDLBI)
  Das BaseProperty-Element ist ein komplexer Typ, der als Basis für andere Elemente dient.  
  
 Seine Attribute können in den Spalten und Measures angezeigt werden.  
  
## <a name="elements-and-attributes"></a>Elemente und Attribute  
 In der folgenden Tabelle sind die Elemente und Attribute aufgeführt, die das BaseProperty-Element definieren.  
  
|Name|Ist erforderlich|Beschreibung|  
|----------|-----------------|-----------------|  
|Ausrichtung|Nein|Der Name für das Element (Spalte, Measure, Navigationseigenschaft, Hierarchie oder Ebene), das von der Implementierung des Member-Typs definiert wird.|  
|FormatString|Nein|Der Anzeigename für das Element.|  
|IsRightToLeft|Nein|Ein boolescher Wert, der angibt, ob das Feld Text enthält, der von rechts nach links gelesen werden kann.<br /><br /> Wenn dieses Attribut weggelassen wird, wird die Standardeinstellung (des Modells) verwendet.|  
|SortDirection|Nein|Ein Wert, der angibt, wie die Feldwerte normalerweise sortiert werden. Die Inhalte dieses Attributs werden vom einfachen Typ SortDirection definiert.<br /><br /> Wenn das Attribut nicht angegeben wird, wird eine Sortierrichtung auf Grundlage des Datentyps des Felds zugewiesen.|  
|Einheiten|Nein|Das Symbol, das für Feldwerte zur Darstellung von Einheiten übernommen wird.<br /><br /> Wenn kein Wert angegeben ist, sind die Einheiten unbekannt.|  
  
## <a name="alignment-element"></a>Alignment-Element  
 Mit diesem einfachen Typ wird das Namensformat definiert, das verwendet wird, um Elemente zu unterscheiden.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|Keine|Verwenden Sie den Attributnamen.|  
|Kontext|Verwenden Sie den Namen der eingehenden Beziehung.|  
|Merge|Verketten Sie den Namen der eingehenden Beziehung und den Eigenschaftsnamen gemäß den Regeln der aktuellen Grammatik.|  
  
## <a name="sortdirection-element"></a>SortDirections-Element  
 Mit diesem einfachen Typ wird das Namensformat definiert, das verwendet wird, um Elemente zu unterscheiden.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|Keine|Verwenden Sie den Attributnamen.|  
|Kontext|Verwenden Sie den Namen der eingehenden Beziehung.|  
|Merge|Verketten Sie den Namen der eingehenden Beziehung und den Namen der Eigenschaft.|  
  
## <a name="see-also"></a>Siehe auch  
 [Informationen zum tabellarischen Objektmodell auf Kompatibilität Ebenen 1050 bis 1103](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
  

