---
title: Aktualisieren von Zellen (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- modifying cells
- XMLA, cells
- updating cells
- cells [Analysis Services]
- XML for Analysis, cells
ms.assetid: a1c61496-36ee-4bce-98d9-d13440d349aa
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 57edea50d67fa52de99f92b85b40bcd5caf307fb
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="updating-cells-xmla"></a>Aktualisieren von Zellen (XMLA)
  Sie können die [UpdateCells](../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md) Befehl zum Ändern des Werts von einer oder mehrerer Zellen in einem Cube für die Cube-Rückschreiben aktiviert. [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] speichert die aktualisierten Informationen in einer separaten Rückschreibetabelle für jede Partition, die zu aktualisierende Zellen enthält.  
  
> [!NOTE]  
>  Die **UpdateCells** Befehl unterstützt während des Rückschreibens keine Zuordnungen. Um zugeordnetes Rückschreiben zu verwenden, sollten Sie verwenden die [Anweisung](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md) Befehl aus, um eine MDX (Multidimensional Expressions) UPDATE-Anweisung zu senden. Weitere Informationen finden Sie unter [UPDATE CUBE-Anweisung &#40; MDX &#41; ](../../mdx/mdx-data-manipulation-update-cube.md).  
  
## <a name="specifying-cells"></a>Angeben von Zellen  
 Die [Zelle](../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md) Eigenschaft von der **UpdateCells** -Befehl enthält, die zu aktualisierenden Zellen. Sie identifizieren jede Zelle in der **Zelle** Eigenschaft mithilfe der Ordinalzahl dieser Zelle. Im Prinzip [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Zellen in einem Cube nummeriert, als sei der Cube eine *p*-dimensionales Array, in dem *p* ist die Anzahl der Achsen. Die Zellen werden in zeilengerichteter Reihenfolge adressiert. Die folgende Abbildung zeigt die Formel für die Berechnung der Ordinalzahl einer Zelle.  
  
 ![Formel zum Berechnen der Ordnungsposition der Zelle](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/media/cellordinalformula.gif "Formel zum Berechnen der Ordnungsposition der Zelle")  
  
 Sobald Sie die Ordinalzahl einer Zelle kennen, können Sie angeben, den beabsichtigten Wert der Zelle in der [Wert](../../analysis-services/xmla/xml-elements-properties/value-element-xmla.md) Eigenschaft von der [Zelle](../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md) Eigenschaft.  
  
## <a name="see-also"></a>Siehe auch  
 [Update-Element &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [Entwickeln mit XMLA in Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  

