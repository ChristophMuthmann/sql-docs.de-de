---
title: Definieren und Identifizieren von Objekten (XMLA) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e01c07842d2a8597967e4a26fc7fd8ea1d363b66
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="defining-and-identifying-objects-xmla"></a>Definieren und Identifizieren von Objekten (XMLA)
  Objekte werden in XMLA-Befehlen (XML for Analysis) mithilfe von Objektbezeichnern und Objektverweisen identifiziert und mithilfe von ASSL-Elementen (Analysis Services Scripting Language) definiert.  
  
## <a name="object-identifiers"></a>Objektbezeichner  
 Ein Objekt wird mithilfe den eindeutigen Bezeichner des Objekts gemäß der Definition in einer Instanz von identifiziert [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Objektbezeichner können entweder explizit angegeben oder durch die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Instanz bestimmt werden, wenn [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] das Objekt erstellt. Können Sie die [Discover](../../analysis-services/xmla/xml-elements-methods-discover.md) Methode zum Abrufen der Objektbezeichner für nachfolgende **Discover** oder [Execute](../../analysis-services/xmla/xml-elements-methods-execute.md) Methodenaufrufe.  
  
## <a name="object-references"></a>Objektverweise  
 Zahlreiche XMLA-Befehle wie z. B. [löschen](../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md) oder [Prozess](../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md), verwenden Sie einen Objektverweis zum Verweisen auf ein Objekt auf eindeutige Weise. Ein Objektverweis enthält den Objektbezeichner des Objekts, für das ein Befehl ausgeführt wird, sowie die Objektbezeichner der Vorgänger dieses Objekts. Beispielsweise enthält der Objektverweis für eine Partition den Objektbezeichner der Partition sowie die Objektbezeichner der übergeordneten Measuregruppe, des übergeordneten Cubes und der übergeordneten Datenbank dieser Partition.  
  
## <a name="object-definitions"></a>Objektdefinitionen  
 Die [erstellen](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md) und [Alter](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md) Befehle in XMLA erstellen bzw. ändern, Objekte auf einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Instanz. Die Definitionen für diese Objekte werden durch dargestellt ein [ObjectDefinition](../../analysis-services/xmla/xml-elements-properties/objectdefinition-element-xmla.md) Element, das Elemente aus ASSL enthält. Objektbezeichner können explizit für alle Haupt- und nebenobjekte angegeben werden, mithilfe der [ID](../../analysis-services/xmla/xml-elements-properties/id-element-xmla.md) Element. Wenn die **ID** Element nicht verwendet wird, die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Instanz stellt einen eindeutigen Bezeichner, mit einer Benennungskonvention, die von dem zu identifizierenden Objekt abhängt. Weitere Informationen zur Verwendung der **erstellen** und **Alter** Befehle zum Definieren von Objekten finden Sie unter [erstellen und Ändern von Objekten &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/creating-and-altering-objects-xmla.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Object-Element & #40; XMLA & #41;](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)   
 [ParentObject-Element &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-properties/parentobject-element-xmla.md)   
 [Source-Element &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md)   
 [Target-Element & #40; XMLA & #41;](../../analysis-services/xmla/xml-elements-properties/target-element-xmla.md)   
 [Entwickeln mit XMLA in Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
