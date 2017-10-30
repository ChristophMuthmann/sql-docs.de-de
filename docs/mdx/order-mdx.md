---
title: Order (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ORDER
dev_langs:
- kbMDX
helpviewer_keywords:
- Order function
ms.assetid: 84acff52-2443-4424-a09e-694e6f14c109
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 98037f9c56523e05a1d3af44078bf8da51cd53e5
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="order-mdx"></a>Order (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ordnet die Elemente einer angegebenen Menge an, wobei die Hierarchie optional beibehalten wird oder nicht.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Numeric expression syntax  
Order(Set_Expression, Numeric_Expression   
[ , { ASC | DESC | BASC | BDESC } ] )  
  
String expression syntax  
Order(Set_Expression, String_Expression   
[ , { ASC | DESC | BASC | BDESC } ] )  
  
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
 *Numeric_expression*  
 Ein gültiger numerischer Ausdruck, bei dem es sich in der Regel um einen MDX-Ausdruck (Multidimensional Expressions) für Zellenkoordinaten handelt, die eine Zahl zurückgeben.  
  
 *String_Expression*  
 Ein gültiger Zeichenfolgenausdruck, bei dem es sich in der Regel um einen gültigen MDX-Ausdruck (Multidimensional Expressions) für Zellenkoordinaten handelt, der eine als Zeichenfolge ausgedrückte Zahl zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Die **Reihenfolge** Funktion kann entweder hierarchisch sein (angegeben mit der **ASC** oder **"DESC"** Flag) oder hierarchisch (angegeben mit der **BASC** oder **BDESC** kennzeichnen; die **B** steht für "Break Hierarchy"). Wenn **ASC** oder **"DESC"** angegeben wird, die **Reihenfolge** Funktion zuerst ordnet die Elemente entsprechend ihrer Position in der Hierarchie, und sortiert dann jede Ebene. Wenn **BASC** oder **BDESC** angegeben wird, die **Reihenfolge** Funktion ordnet die Elemente in der Menge ungeachtet der Hierarchie. Kein Flag angegeben ist, **ASC** ist die Standardeinstellung.  
  
 Wenn die **Reihenfolge** Funktion mit einem Satz verwendet wird, in denen zwei oder mehr Hierarchien kreuzverknüpft sind, sind und die **"DESC"** Flag verwendet wird, ist nur die Elemente der letzten Hierarchie im Satz befohlen. Dies ist eine Änderung im Vergleich zu Analysis Services 2000, wo alle Hierarchien im Satz befohlen wurden.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird zurückgegeben, aus der **Adventure Works** cube die Anzahl der Bestellungen des Wiederverkäufers für alle Kalenderquartale der Kalenderhierarchie der Date-Dimension. Die **Reihenfolge** -Funktion ordnet den Satz für die ROWS-Achse neu. Die **Reihenfolge** -Funktion sortiert die Menge von `[Reseller Order Count]` hierarchische absteigend von bestimmt die `[Calendar]` Hierarchie.  
  
 `SELECT`  
  
 `Measures.[Reseller Order Count] ON COLUMNS,`  
  
 `Order(`  
  
 `[Date].[Calendar].[Calendar Quarter].MEMBERS`  
  
 `,Measures.[Reseller Order Count]`  
  
 `,DESC`  
  
 `) ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 Beachten Sie, dass in diesem Beispiel bei der **"DESC"** Flag "" wird geändert, um **BDESC**, die Hierarchie unterbrochen wird und die Liste der Kalenderquartale wird ohne Beachtung der Hierarchie zurückgegeben:  
  
 `SELECT`  
  
 `Measures.[Reseller Order Count] ON COLUMNS,`  
  
 `Order(`  
  
 `[Date].[Calendar].[Calendar Quarter].MEMBERS`  
  
 `,Measures.[Reseller Order Count]`  
  
 `,BDESC`  
  
 `) ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 Im folgenden Beispiel wird das Reseller Sales-Measure für die fünf bestverkauften Produktunterkategorien unabhängig von der Hierarchie basierend auf Reseller Gross Profit zurückgegeben. Die **Teilmenge** Funktion wird verwendet, um nur die ersten 5 Tupeln in der Menge zurück, nach dem Sortieren des Ergebnisses mithilfe der **Reihenfolge** Funktion.  
  
 `SELECT Subset`  
  
 `(Order`  
  
 `([Product].[Product Categories].[SubCategory].members`  
  
 `,[Measures].[Reseller Gross Profit]`  
  
 `,BDESC`  
  
 `)`  
  
 `,0`  
  
 `,5`  
  
 `) ON 0`  
  
 `FROM [Adventure Works]`  
  
 Im folgenden Beispiel wird die **Rang** Funktion, um die Elemente der City-Hierarchie, rank basierend auf dem Reseller Sales Amount-Measure und klicken Sie dann in der Rangreihenfolge anzeigt. Mithilfe der **Reihenfolge** -Funktion zum vorsortieren der Menge der Elemente der City-Hierarchie, die Sortierung nur einmal ausgeführt und anschließend ein linearer Scan, bevor angezeigt wird, der Sortierreihenfolge.  
  
```  
WITH   
SET OrderedCities AS Order  
   ([Geography].[City].[City].members  
   , [Measures].[Reseller Sales Amount], BDESC  
   )  
MEMBER [Measures].[City Rank] AS Rank  
   ([Geography].[City].CurrentMember, OrderedCities)  
SELECT {[Measures].[City Rank],[Measures].[Reseller Sales Amount]}  ON 0   
,Order  
   ([Geography].[City].[City].MEMBERS  
   ,[City Rank], ASC)  
    ON 1  
FROM [Adventure Works]  
```  
  
 Im folgende Beispiel gibt die Anzahl der Produkte in der Gruppe, die eindeutig sind, mithilfe der **Reihenfolge** Funktion, um die Reihenfolge der nicht leeren Tupel vor Verwendung der **Filter** Funktion. Die **CurrentOrdinal** Funktion zu vergleichen und Ausschließen von Gleichrangigkeit verwendet wird.  
  
```  
WITH MEMBER [Measures].[PrdTies] AS Count  
   (Filter  
      (Order  
        (NonEmpty  
          ([Product].[Product].[Product].Members  
          , {[Measures].[Reseller Order Quantity]}  
          )  
       , [Measures].[Reseller Order Quantity]  
       , BDESC  
       ) AS OrdPrds  
    , (OrdPrds.CurrentOrdinal < OrdPrds.Count   
       AND [Measures].[Reseller Order Quantity] =   
          ( [Measures].[Reseller Order Quantity]  
            , OrdPrds.Item  
               (OrdPrds.CurrentOrdinal  
               )  
            )  
         )  
         OR (OrdPrds.CurrentOrdinal > 1   
            AND [Measures].[Reseller Order Quantity] =   
               ([Measures].[Reseller Order Quantity]  
               , OrdPrds.Item  
                  (OrdPrds.CurrentOrdinal-2)  
                )  
             )  
          )  
       )  
SELECT {[Measures].[PrdTies]} ON 0  
FROM [Adventure Works]  
```  
  
 Um zu verstehen, wie die **"DESC"** flag mit Sätzen von Tupeln funktioniert, betrachten Sie zuerst die Ergebnisse der folgenden Abfrage:  
  
```  
  
SELECT  
{[Measures].[Tax Amount]} ON 0,  
ORDER(  
[Sales Territory].[Sales Territory].[Group].MEMBERS  
,[Measures].[Tax Amount], DESC)  
ON 1  
FROM [Adventure Works]  
  
```  
  
 Auf der Zeilenachse sehen Sie, dass die Vertriebsgebietsgruppen in absteigender Reihenfolge des Steuerbetrags wie folgt sortiert wurden: Nordamerika, Europa, Pazifik, NA. Sehen Sie sich nun was geschieht, wenn wir Crossjoin aus dem Satz der Vertriebsgebietsgruppen mit dem Satz von Produktunterkategorien und Anwenden der **Reihenfolge** -Funktion auf die gleiche Weise wie folgt:  
  
```  
  
SELECT  
{[Measures].[Tax Amount]} ON 0,  
ORDER(  
[Sales Territory].[Sales Territory].[Group].MEMBERS  
*  
{[Product].[Product Categories].[subCategory].Members}  
,[Measures].[Tax Amount], DESC)  
ON 1  
FROM [Adventure Works]  
  
```  
  
 Während der Satz von Produktunterkategorien in absteigender, hierarchischer Reihenfolge angeordnet wurde, werden die Vertriebsgebietsgruppen jetzt nicht sortiert und werden in der Reihenfolge angezeigt, in der sie auf der Hierarchie angezeigt werden: Europa, NA, Nordamerika und Pazifik. Das liegt daran, dass nur die letzte Hierarchie im Satz von Tupeln, Produktunterkategorien, sortiert ist. Um das Verhalten von Analysis Services 2000 zu reproduzieren, verwenden Sie eine Reihe von geschachtelten **generieren** Funktionen für jeden Satz zu sortieren, bevor er kreuzverknüpft sind, z. B. ist:  
  
```  
  
SELECT  
{[Measures].[Tax Amount]} ON 0,  
GENERATE(  
ORDER(  
[Sales Territory].[Sales Territory].[Group].MEMBERS  
,[Measures].[Tax Amount], DESC)  
,  
ORDER(  
[Sales Territory].[Sales Territory].CURRENTMEMBER  
*  
{[Product].[Product Categories].[subCategory].Members}  
,[Measures].[Tax Amount], DESC))  
ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

