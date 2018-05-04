---
title: Benutzerdefinierte Elementeigenschaften (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: mdx
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 26139ee397c9dbaca27eb3ef8236c3e242b98890
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-member-properties---user-defined-member-properties"></a>MDX - Elementeigenschaften: benutzerdefinierte Elementeigenschaften
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Benutzerdefinierte Elementeigenschaften können einer bestimmten benannten Ebene in einer Dimension als Attributbeziehungen hinzugefügt werden. Benutzerdefinierte Elementeigenschaften können weder der **(Alle)** -Ebene einer Hierarchie noch der Hierarchie selbst hinzugefügt werden.  
  
## <a name="creating-user-defined-member-properties"></a>Erstellen von benutzerdefinierten Elementeigenschaften  
 Benutzerdefinierte Elementeigenschaften können serverbasierten Dimensionen oder Cubes entweder über die Benutzeroberfläche oder programmgesteuert hinzugefügt werden.  
  
-   Um benutzerdefinierte Elementeigenschaften über die Benutzeroberfläche hinzuzufügen, verwenden Sie den Dimensions-Designer in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]. Weitere Informationen finden Sie unter [Definieren von Attributbeziehungen](../../../analysis-services/multidimensional-models/attribute-relationships-define.md).  
  
-   Um benutzerdefinierte Elementeigenschaften programmgesteuert hinzuzufügen, kann Ihre Anwendung entweder Analysis Management Objects (AMO) oder eine Kombination aus XMLA (XML for Analysis) und ASSL (Analysis Services Scripting Language) verwenden. Weitere Informationen finden Sie unter [Attributbeziehungen](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md).  
  
## <a name="retrieving-user-defined-member-properties"></a>Abrufen von benutzerdefinierten Elementeigenschaften  
 Sie können benutzerdefinierte Elementeigenschaften abrufen, indem Sie entweder das **PROPERTIES** -Schlüsselwort oder die [Properties](../../../mdx/properties-mdx.md) -Funktion verwenden.  
  
### <a name="using-the-properties-keyword-to-retrieve-user-defined-member-properties"></a>Verwenden des PROPERTIES-Schlüsselworts zum Abrufen von benutzerdefinierten Elementeigenschaften  
 Die Syntax für das Abrufen von benutzerdefinierten Elementeigenschaften gleicht der Syntax, mit der systeminterne Eigenschaften von Ebenenelementen abgerufen werden. Die folgende Syntax verdeutlicht dies:  
  
 `DIMENSION PROPERTIES [Dimension.]Level.<Custom_Member_Property>`  
  
 Das **PROPERTIES** -Schlüsselwort steht hinter dem Mengenausdruck der Achsenspezifikation. In der folgende MDX-Abfrage ruft das **PROPERTIES** -Schlüsselwort beispielsweise die benutzerdefinierten Elementeigenschaften `List Price` und `Dealer Price` ab und wird nach dem Mengenausdruck angegeben, der die im Januar verkauften Produkte identifiziert:  
  
```  
SELECT   
   CROSSJOIN([Ship Date].[Calendar].[Calendar Year].Members,   
             [Measures].[Sales Amount]) ON COLUMNS,  
   NON EMPTY Product.Product.MEMBERS  
   DIMENSION PROPERTIES   
              Product.Product.[List Price],  
              Product.Product.[Dealer Price]  ON ROWS  
FROM [Adventure Works]  
WHERE ([Date].[Month of Year].[January])   
```  
  
### <a name="using-the-properties-function-to-retrieve-user-defined-member-properties"></a>Verwenden der Properties-Funktion zum Abrufen von benutzerdefinierten Elementeigenschaften  
 Für das Zugreifen auf benutzerdefinierte Elementeigenschaften kann auch die **Properties** -Funktion verwendet werden. Die folgende MDX-Abfrage verwendet beispielsweise das **WITH**-Schlüsselwort, um ein berechnetes Element zu erstellen, das aus der `List Price`-Elementeigenschaft besteht:  
  
```  
WITH   
   MEMBER [Measures].[Product List Price] AS  
   [Product].[Product].CurrentMember.Properties("List Price")  
SELECT   
   [Measures].[Product List Price] on COLUMNS,  
   [Product].[Product].MEMBERS  ON Rows  
FROM [Adventure Works]  
```  
  
 Weitere Informationen zum Erstellen berechneter Elemente finden Sie unter [Erstellen von berechneten Elementen in MDX &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-building-calculated-members.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von Elementeigenschaften & #40; MDX & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-member-properties.md)   
 [Datenbankeigenschaften & #40; MDX & #41;](../../../mdx/properties-mdx.md)  
  
  
