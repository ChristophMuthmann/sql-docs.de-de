---
title: NamingTemplate-Element (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: NamingTemplate Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: NamingTemplate
helpviewer_keywords: NamingTemplate element
ms.assetid: d68d765c-f012-40c1-acd4-32741ee2eadf
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1a4e48c3c66aab602ed8f76f39da952aa85f9a9c
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="namingtemplate-element-assl"></a>NamingTemplate-Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Definiert, wie Ebenen in einer über-/ unterordnungshierarchie aus erstellter benannt werden die [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md) übergeordneten Elements.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<DimensionAttribute>  
   ...  
      <NamingTemplate>...</NamingTemplate>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Description|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge|  
|Standardwert|InclusionThresholdSetting|  
|Cardinality|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|Untergeordnete Elemente|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Hinweise  
 Den Wert des der **NamingTemplate** Element wird nur von übergeordneten Attributen verwendet (also der Wert der die [Verwendung](../../../analysis-services/scripting/properties/usage-element-dimensionattribute-assl.md) Element des der **DimensionAttribute** übergeordnetes Element wird festgelegt, um *übergeordneten*).  
  
 Wenn ein übergeordnetes Attribut zum Erstellen einer Hierarchie verwendet wird, werden die Ebenen der Hierarchie durch die Über-/Unterordnungsbeziehungen zwischen den Elementen, die im übergeordneten Attribut enthalten sind, bestimmt. Daher können die Ebenennamen nicht wie in anderen Dimensionen von den Attributnamen, die für die Hierarchie verwendet werden, abgeleitet werden.  
  
 Stattdessen wird eine Benennungsvorlage verwendet, um Ebenennamen für Über-/Unterordnungshierarchien zu generieren. Das im übergeordneten Attribut definierte **NamingTemplate** -Element enthält einen Zeichenfolgenausdruck, der verwendet wird, um Ebenennamen zu definieren. Es gibt zwei Möglichkeiten, eine Benennungsvorlage für ein übergeordnetes Attribut zu definieren. Sie können entweder ein Benennungsmuster entwerfen, oder Sie können eine Namensliste angeben.  
  
 Ein Benennungsmuster enthält ein Sternchen (`*`) als Platzhalterzeichen für einen Indikator, der mit jeder neuen und tieferen Ebene gesteigert und in den Namen eingefügt wird. Beispielsweise führt die Verwendung von `Level *` zu den Ebenennamen `Level 01`, `Level 02`, `Level 03`usw., wenn keine (ALL) Ebene definiert ist. Wenn ein Benennungsmuster kein Platzhalterzeichen enthält, wird es zunächst in seiner ursprünglichen Form verwendet. Danach werden dann alle folgenden Ebenen durch Anhängen eines Leerzeichens und einer Zahl an das Ende des Musters gebildet. Beispielsweise führt die Verwendung von `Level` zu den Ebenennamen `Level`, `Level 01`, `Level 02`usw.  
  
 Um einen bestimmten Namenssatz für die Benennung zu verwenden, muss der Wert des **NamingTemplate** -Elements auf eine durch Semikolons getrennte Liste von Ebenennamen festgelegt werden. Jeder Name in der Liste wird für einen nachfolgenden Ebenennamen verwendet. Wenn die Anzahl der Ebenen die Anzahl der Namen in der Liste überschreitet, wird der letzte Name in der Liste als Vorlage für etwaige zusätzliche Ebenennamen verwendet, wobei ein Leerzeichen und eine Ordnungszahl gemäß der Beschreibung oben an den letzten Namen angehängt wird. Beispielsweise führt die Verwendung von `Division;Group;Unit` zu den Ebenennamen `Division`, `Group`, `Unit`, `Unit 01`, `Unit 02`usw. Dagegen führt die Verwendung von `Division;Group;Unit *` zu den Ebenennamen `Division`, `Group`, `Unit 03`, `Unit 04`usw.  
  
 Jeder Name in der Liste wird als Vorlage behandelt, um die Eindeutigkeit von Ebenennamen sicherzustellen. Beispielsweise führt die Verwendung von `Manager;Team Lead;Manager;Team Lead;Worker *` zu den Ebenennamen `Manager`, `Team Lead`, `Manager 01`, `Team Lead 01`, `Worker 05`, `Worker 06`.  
  
 Verwenden Sie zwei Sternchen (*), um das Sternchen aufzunehmen (\*) Zeichen in einen Ebenennamen als Teil einer benennungsvorlage.  
  
 Das Element, das das übergeordnete Element des entspricht **NamingTemplate** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.DimensionAttribute>.  
  
## <a name="see-also"></a>Siehe auch  
 [Namingtemplatetranslation-Element &#40; ASSL &#41;](../../../analysis-services/scripting/collections/namingtemplatetranslations-element-assl.md)   
 [DimensionAttribute-Datentyp &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)   
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
