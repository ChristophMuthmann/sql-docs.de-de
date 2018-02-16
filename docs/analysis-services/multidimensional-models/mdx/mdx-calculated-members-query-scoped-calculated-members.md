---
title: Erstellen im Bereich einer Abfrage berechnete Elemente (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
- WITH keyword
- query-scoped calculated members [MDX]
ms.assetid: c4507149-e67b-4e5d-9192-cc911acd9adc
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 2ba34cb6af554bb958c8754a9971f3ff4ba5b9a6
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="mdx-calculated-members---query-scoped-calculated-members"></a>MDX berechnete Elemente - Bereich einer Abfrage berechnete Elemente
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
Wenn ein berechnetes Element nur für eine einzelne MDX-Abfrage (Multidimensional Expressions) benötigt wird, können Sie das berechnete Element mit dem WITH-Schlüsselwort definieren. Ein berechnetes Element, das mit dem WITH-Schlüsselwort erstellt wird, ist nach der Ausführung der Abfrage nicht länger vorhanden.  
  
 Wie in diesem Thema erläutert wird, ist die Syntax des WITH-Schlüsselworts sehr flexibel und ermöglicht sogar die Definition berechneter Elemente auf der Grundlage eines anderen berechneten Elements.  
  
> [!NOTE]  
>  Weitere Informationen zu berechneten Elementen finden Sie unter [Erstellen von berechneten Elementen in MDX &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-building-calculated-members.md).  
  
## <a name="with-keyword-syntax"></a>WITH-Schlüsselwort (Syntax)  
 Verwenden Sie die folgende Syntax, um einer SELECT-Anweisung von MDX das WITH-Schlüsselwort hinzuzufügen:  
  
```  
[ WITH <SELECT WITH clause> [ , <SELECT WITH clause> ... ] ] SELECT [ * | ( <SELECT query axis clause> [ , <SELECT query axis clause> ... ] ) ]FROM <SELECT subcube clause> [ <SELECT slicer axis clause> ][ <SELECT cell property list clause> ]  
<SELECT WITH clause> ::=  
   ( [ CALCULATED ] MEMBER <CREATE MEMBER body clause>) | <CREATE MEMBER body clause> ::= Member_Identifier AS 'MDX_Expression'  
   [ <CREATE MEMBER property clause> [ , <CREATE MEMBER property clause> ... ] ]  
<CREATE MEMBER property clause> ::=  
   ( MemberProperty_Identifier = Scalar_Expression )  
  
```  
  
 In der Syntax für das WITH-Schlüsselwort entspricht der `Member_Identifier` -Wert dem vollgekennzeichneten Namen des berechneten Elements. Dieser vollgekennzeichnete Name enthält die Dimension oder Ebene, der das berechnete Element zugeordnet ist. Der `MDX_Expression` -Wert gibt den Wert des berechneten Elements zurück, nachdem der Wert des Ausdrucks ausgewertet wurde. Die Werte systeminterner Zelleneigenschaften für ein berechnetes Element können optional angegeben werden, indem der Name der Zelleneigenschaft im `MemberProperty_Identifier` -Wert und der Wert der Zelleneigenschaft im `Scalar_Expression` -Wert angegeben wird.  
  
## <a name="with-keyword-examples"></a>WITH-Schlüsselwort (Beispiele)  
 Der folgende MDX-Ausdruck definiert ein berechnetes Element, `[Measures].[Special Discount]`, durch das ein bestimmter Rabatt, basierend auf dem ursprünglichen Rabattbetrag, berechnet wird.  
  
```  
WITH   
   MEMBER [Measures].[Special Discount] AS  
   [Measures].[Discount Amount] * 1.5  
SELECT   
   [Measures].[Special Discount] on COLUMNS,  
   NON EMPTY [Product].[Product].MEMBERS  ON Rows  
FROM [Adventure Works]  
WHERE [Product].[Category].[Bikes]  
```  
  
 Sie können berechnete Elemente an jedem beliebigen Punkt in einer Hierarchie erstellen. Die folgende MDX-Abfrage definiert beispielsweise das berechnete Element `[BigSeller]` für einen hypothetischen Sales-Cube. Dieses berechnete Element bestimmt, ob ein bestimmtes Geschäft mindestens 100,00 Stück der Produkte Bier und Wein umgesetzt hat. Die Abfrage erstellt jedoch das berechnete Element `[BigSeller]` nicht als untergeordnetes Element der `[Product]` -Dimension, sondern als untergeordnetes Element des `[Beer and Wine]` -Elements.  
  
```  
WITH   
   MEMBER [Product].[Beer and Wine].[BigSeller] AS  
  IIf([Product].[Beer and Wine] > 100, "Yes","No")  
SELECT  
   {[Product].[BigSeller]} ON COLUMNS,  
   Store.[Store Name].Members ON ROWS  
FROM Sales  
  
```  
  
 Berechnete Elemente müssen nicht nur von vorhandenen Elementen in einem Cube abhängen. Berechnete Elemente können auch auf anderen berechneten Elementen basieren, die in demselben MDX-Ausdruck definiert sind. Die folgende MDX-Abfrage verwendet beispielsweise den Wert, der im ersten berechneten Element, `[Measures].[Special Discount]`, erstellt wird, um den Wert des zweiten berechneten Elements, `[Measures].[Special Discounted Amount]`, zu generieren.  
  
```  
WITH   
   MEMBER [Measures].[Special Discount] AS  
   [Measures].[Discount Percentage] * 1.5,   
   FORMAT_STRING = 'Percent'  
  
   MEMBER [Measures].[Special Discounted Amount] AS  
   [Measures].[Reseller Average Unit Price] * [Measures].[Special Discount],   
   FORMAT_STRING = 'Currency'  
  
SELECT   
   {[Measures].[Special Discount], [Measures].[Special Discounted Amount]} on COLUMNS,  
   NON EMPTY [Product].[Product].MEMBERS  ON Rows  
FROM [Adventure Works]  
WHERE [Product].[Category].[Bikes]  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../../../mdx/mdx-function-reference-mdx.md)   
 [SELECT-Anweisung &#40; MDX &#41;](../../../mdx/mdx-data-manipulation-select.md)   
 [Erstellen im Bereich einer Sitzung berechnete Elemente &#40; MDX &#41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-session-scoped-calculated-members.md)  
  
  
