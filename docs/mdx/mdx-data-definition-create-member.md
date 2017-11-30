---
title: CREATE MEMBER-Anweisung (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_MEMBER
- CREATE MEMBER
- Member
- CREATE
dev_langs: kbMDX
helpviewer_keywords:
- CREATE MEMBER statement
- calculated members [MDX]
ms.assetid: 49379217-be2c-4139-a206-1168078b9b76
caps.latest.revision: "55"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 44a329213b7bbe39167e8f0c6b85e473d2d58411
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="mdx-data-definition---create-member"></a>MDX-Datendefinition - Element zu erstellen
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Erstellt ein berechnetes Element.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CREATE [ SESSION ] [HIDDDEN] [ CALCULATED ] MEMBER CURRENTCUBE | Cube_Name.Member_Name   
   AS MDX_Expression  
      [,Property_Name = Property_Value, ...n]  
......[,SCOPE_ISOLATION = CUBE]  
```  
  
## <a name="arguments"></a>Argumente  
 *Cube_Name*  
 Ein gültiger Zeichenfolgenausdruck, der den Namen des Cubes bereitstellt, in dem das Element erstellt wird.  
  
 *Member_Name*  
 Ein gültiger Zeichenfolgenausdruck, der einen Elementnamen bereitstellt. Geben Sie einen vollqualifizierten Namen an, um ein Element in einer anderen Dimension als der Measures-Dimension zu erstellen. Wenn Sie keinen vollqualifizierten Elementnamen angeben, wird das Element in der Measures-Dimension erstellt.  
  
 *MDX_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions).  
  
 *Eigenschaftsname*  
 Eine gültige Zeichenfolge, die den Namen der Eigenschaft eines berechneten Elements bereitstellt.  
  
 *Property_Value*  
 Ein gültiger Skalarausdruck, der den Wert der Eigenschaft eines berechneten Elements definiert.  
  
## <a name="remarks"></a>Hinweise  
 Die CREATE MEMBER-Anweisung definiert berechnete Elemente, die während der gesamten Sitzung verfügbar sind und somit in mehreren Abfragen im Verlauf der Sitzung verwendet werden können. Weitere Informationen finden Sie unter [Creating Session-Scoped berechnete Elemente &#40; MDX &#41; ](../analysis-services/multidimensional-models/mdx/mdx-calculated-members-session-scoped-calculated-members.md).  
  
 Sie können auch ein berechnetes Element definieren, das in einer einzelnen Abfrage verwendet wird. Wenn Sie ein berechnetes Element definieren möchten, das auf eine einzelne Abfrage beschränkt ist, verwenden Sie die WITH-Klausel in der SELECT-Anweisung. Weitere Informationen finden Sie unter [Creating Query-Scoped berechnete Elemente &#40; MDX &#41; ](../analysis-services/multidimensional-models/mdx/mdx-calculated-members-query-scoped-calculated-members.md).  
  
 *Property_name* auf entweder standard oder optionale berechnete Elementeigenschaften verweisen. Standardelementeigenschaften sind in diesem Thema weiter unten aufgelistet. Berechnete Elemente erstellen, die mit CREATE MEMBER ohne einen **SITZUNG** Indexschlüsselwert Sitzungsbereich. Außerdem müssen Zeichenfolgen, die in der Definition eines berechneten Elements stehen, in doppelte Anführungszeichen gesetzt werden. Dies unterscheidet sich von der für OLE DB definierten Methode, die angibt, dass Zeichenfolgen in einfachen Anführungszeichen stehen müssen.  
  
 Die Angabe eines anderen als des aktuell verbundenen Cubes verursacht einen Fehler. Daher sollten Sie den aktuellen Cube mithilfe von CURRENTCUBE statt mit dem Cubenamen angeben.  
  
 Weitere Informationen zu Elementeigenschaften, die durch OLE DB definiert sind, finden Sie in der OLE DB-Dokumentation.  
  
## <a name="scope"></a>Scope  
 Ein berechnetes Element kann in einem der Gültigkeitsbereiche auftreten, die in der folgenden Tabelle aufgeführt sind.  
  
 Bereich einer Abfrage  
 Die Sichtbarkeit und Lebensdauer des berechneten Elements ist auf die Abfrage beschränkt. Das berechnete Element ist in einer einzelnen Abfrage definiert. Der Abfragebereich hat Vorrang vor dem Sitzungsbereich. Weitere Informationen finden Sie unter [Creating Query-Scoped berechnete Elemente &#40; MDX &#41; ](../analysis-services/multidimensional-models/mdx/mdx-calculated-members-query-scoped-calculated-members.md).  
  
 Bereich einer Sitzung  
 Die Sichtbarkeit und Lebensdauer des berechneten Elements ist auf die Sitzung beschränkt, in der das Element erstellt wurde. (Die Lebensdauer ist geringer als die Dauer der Sitzung, wenn eine DROP MEMBER-Anweisung für das berechnete Element ausgegeben wird.) Die CREATE MEMBER-Anweisung erstellt ein berechnetes Element im Sitzungsbereich.  
  
### <a name="scope-isolation"></a>Bereichsisolation  
 Wenn ein MDX-Cubeskript (Multidimensional Expressions) berechnete Elemente enthält, werden die berechneten Elemente standardmäßig aufgelöst, bevor Berechnungen im Sitzungsbereich aufgelöst werden und bevor abfragedefinierte Berechnungen aufgelöst werden.  
  
> [!NOTE]  
>  In bestimmten Szenarien die [Aggregate (MDX)](../mdx/aggregate-mdx.md) Funktion und die [VisualTotals (MDX)](../mdx/visualtotals-mdx.md) Funktion tritt dieses Verhalten nicht auf.  
  
 Durch das Verhalten können in generischen Clientanwendungen Cubes mit komplexen Berechnungen verwendet werden, ohne dass die spezielle Implementierung der Berechnungen berücksichtigt werden muss. Allerdings sollten Sie in bestimmten Szenarien, Sitzung oder im Bereich einer Abfrage berechnete Elemente vor bestimmten Berechnungen in den Cube, und weder ausgeführt der **aggregieren** Funktion noch die **VisualTotals** -Funktion sind anwendbar. Um das zu erreichen, verwenden Sie die SCOPE_ISOLATION-Berechnungseigenschaft.  
  
#### <a name="example"></a>Beispiel  
 Das folgende Skript stellt ein Beispiel für ein Szenario dar, in dem die SCOPE_ISOLATION-Berechnungseigenschaft erforderlich ist, damit das richtige Ergebnis entsteht.  
  
 **MDX-Skript des Cubes:**  
  
```  
CREATE MEMBER CURRENTCUBE.Measures.ProfitRatio AS 'Measures.[Store Sales]/Measures.[Store Cost]', SOLVE_ORDER = 10  
```  
  
 **MDX-Abfrage:**  
  
```  
WITH MEMBER [Customer].[Customers].[USA]. USAWithoutWA AS  
[Customer].[Customers].[Country].&[USA] - [Customer].[Customers].[State Province.&[WA], SOLVE_ORDER=5  
SELECT {USAWithoutWA} ON 0 FROM SALES  
WHERE ProfitRatio  
```  
  
 Das gewünschte Ergebnis der vorherigen Abfrage entspricht dem Verhältnis für die Verkäufe der USA ohne WA, damit die Kosten für die USA ohne WA gespeichert werden können. Die vorherige Abfrage gibt nicht das gewünschte Ergebnis zurück, sondern das Verhältnis für die USA abzüglich des Verhältnisses für WA. Dies stellt ein bedeutungsloses Ergebnis dar. Wenn das gewünschte Ergebnis erzielt werden soll, können Sie die SCOPE_ISOLATION-Berechnungseigenschaft verwenden.  
  
 **MDX-Abfrage mit SCOPE_ISOLATION-Berechnungseigenschaft:**  
  
```  
WITH MEMBER [Customer].[Customers].[USA]. USAWithoutWA AS  
[Customer].[Customers].[Country].&[USA] - [Customer].[Customers].[State Province.&[WA], SOLVE_ORDER=5  
,SCOPE_ISOLATION=CUBE  
SELECT {USAWithoutWA} ON 0 FROM SALES  
WHERE ProfitRatio  
```  
  
## <a name="standard-properties"></a>Standardeigenschaften  
 Jedes berechnete Element hat eine Reihe von Standardeigenschaften. Wenn eine Clientanwendung mit verbunden ist [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], die Standardeigenschaften sind entweder unterstützt oder verfügbar ist, unterstützt werden müssen, wie der Administrator wählt.  
  
 Abhängig von der Cubedefinition sind möglicherweise weitere Elementeigenschaften verfügbar. Die folgenden Eigenschaften enthalten Informationen, die für die Dimensionsebene im Cube relevant sind.  
  
|Eigenschaftsbezeichner|Bedeutung|  
|-------------------------|-------------|  
|SOLVE_ORDER|Die Reihenfolge, in der das berechnete Element in Fällen gelöst wird, in denen ein berechnetes Element auf ein anderes berechnetes Element verweist (also in Fällen, in denen berechnete Elemente sich überschneiden).|  
|FORMAT_STRING|Eine Formatzeichenfolge im [!INCLUDE[msCoName](../includes/msconame-md.md)] Office-Stil, die die Clientanwendung für das Anzeigen von Zellwerten verwenden kann.|  
|VISIBLE|Ein Wert, der bestimmt, ob das berechnete Element in einem Schemarowset sichtbar ist. Sichtbare berechnete Elemente hinzugefügt werden können, um eine Gruppe, die [AddCalculatedMembers](../mdx/addcalculatedmembers-mdx.md) Funktion. Ein Wert ungleich 0 zeigt an, dass das berechnete Element sichtbar ist. Der Standardwert für diese Eigenschaft ist *Visible*.<br /><br /> Berechnete Elemente, die nicht sichtbar sind (für die dieser Wert auf 0 festgelegt ist), werden üblicherweise als Zwischenschritte in komplexeren berechneten Elementen verwendet. Auf diese berechneten Elemente können auch andere Arten von Elementen (z. B. Measures) verweisen.|  
|NON_EMPTY_BEHAVIOR|Das Measure oder die Menge, mit dem oder der beim Auflösen leerer Zellen das Verhalten berechneter Elemente bestimmt wird.<br /><br /> **\*\*Warnung \* \***  diese Eigenschaft ist veraltet. Vermeiden Sie es, sie festzulegen. Weitere Informationen finden Sie unter [Veraltete Analysis Services-Funktionen in SQL Server 2016](../analysis-services/deprecated-analysis-services-features-in-sql-server-2016.md).|  
|CAPTION|Eine Zeichenfolge, die von der Clientanwendung als Beschriftung für das Element verwendet wird.|  
|DISPLAY_FOLDER|Eine Zeichenfolge, die den Pfad des Anzeigeordners angibt, der von der Clientanwendung zum Anzeigen des Elements verwendet wird. Das Trennzeichen für Ordnerebenen wird von der Clientanwendung definiert. Zu den Tools und Clients, die vom [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], den umgekehrten Schrägstrich (\\) ebenentrennzeichen ist. Um mehrere Anzeigeordner für ein definiertes Element bereitzustellen, verwenden Sie ein Semikolon (;) als Trennzeichen für die Ordner.|  
|ASSOCIATED_MEASURE_GROUP|Der Name der Measuregruppe, der dieses Element zugeordnet wird.|  
  
## <a name="see-also"></a>Siehe auch  
 [DROP MEMBER-Anweisung &#40; MDX &#41;](../mdx/mdx-data-definition-drop-member.md)   
 [UPDATE MEMBER-Anweisung &#40; MDX &#41;](../mdx/mdx-data-definition-update-member.md)   
 [MDX-Datendefinitionsanweisungen &#40; MDX &#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
