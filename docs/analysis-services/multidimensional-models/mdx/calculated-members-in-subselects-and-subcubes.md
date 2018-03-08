---
title: "Berechnete Elemente in untergeordneten SELECT-Ausdrücken und Teilcubes | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6e35e8f7-ae1c-4549-8432-accf036d2373
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 95a989d092a5b69662fc9f7f542792d9c2895b47
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="calculated-members-in-subselects-and-subcubes"></a>Berechnete Elemente in untergeordneten SELECT-Ausdrücken und Teilcubes
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
Ein berechnetes Element ist ein Dimensionselement, dessen Wert zur Laufzeit aus einem Ausdruck berechnet wird und das in untergeordneten SELECT-Ausdrücken und in Teilcubes verwendet werden kann, um den Cubebereich einer Abfrage genauer zu definieren.  
  
## <a name="enabling-calculated-members-in-the-subspace"></a>Aktivieren berechneter Elemente im Teilbereich  
 Die Verbindungszeichenfolgen-Eigenschaft **SubQueries** unter <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> oder die **DBPROPMSMDSUBQUERIES** -Eigenschaft unter [Unterstützte XMLA-Eigenschaften &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md) definiert das Verhalten oder die Zulässigkeit von berechneten Elementen oder berechneten Sätzen in Unterauswahlen oder Teilcubes. Im weiteren Verlauf dieses Dokuments bezieht sich der Begriff "untergeordneter SELECT-Ausdruck" auf untergeordnete SELECT-Ausdrücke UND auf Teilcubes, sofern nichts anderes angegeben ist.  
  
 Die SubQueries-Eigenschaft lässt die folgenden Werte zu.  
  
|||  
|-|-|  
|Wert|Beschreibung|  
|0|Berechnete Elemente sind in untergeordneten SELECT-Ausdrücken oder Teilcubes nicht zulässig.<br /><br /> Beim Auswerten des untergeordneten SELECT-Ausdrucks oder des Teilcubes wird ein Fehler ausgelöst, wenn auf ein berechnetes Element verwiesen wird.|  
|1|Berechnete Elemente in untergeordneten SELECT-Ausdrücken oder Teilcubes sind zulässig, in den zurückgebenden Teilbereich werden jedoch keine Vorgänger der Elemente eingeführt.|  
|2|Berechnete Elemente in untergeordneten SELECT-Ausdrücken oder Teilcubes sind zulässig und in den zurückgebenden Teilbereich werden Vorgänger der Elemente eingeführt. Zudem ist eine gemischte Granularität in der Auswahl berechneter Elemente zulässig.|  
  
 Werte von 1 oder 2 in der SubQueries-Eigenschaft ermöglichen, berechnete Elemente zum Filtern des zurückgebenden Teilbereichs der untergeordneten SELECT-Ausdrücke zu verwenden.  
  
 Dieses Konzept soll an einem Beispiel verdeutlicht werden. Zunächst muss ein berechnetes Element erstellt werden. anschließend wird eine untergeordnete SELECT-Abfrage ausgegeben, um obiges Verhalten zu demonstrieren.  
  
 Im folgenden Beispiel wird ein berechnetes Element erstellt, das der Hierarchie [Geography].[Geography] unterhalb des Bundesstaates Washington die Stadt [Seattle Metro] hinzufügt.  
  
 Um das Beispiel auszuführen, muss die Verbindungszeichenfolge die SubQueries-Eigenschaft mit einem Wert von 1 enthalten und alle MDX-Anweisungen müssen in der gleichen Sitzung ausgeführt werden.  
  
> [!IMPORTANT]  
>  Wenn Sie Management Studio zum Testen von Abfragen verwenden, klicken Sie im Verbindungs-Manager auf die Schaltfläche „Optionen“, um auf den Bereich mit den zusätzlichen Eigenschaften der Verbindungszeichenfolge zuzugreifen. Dort können Sie für „subqueries“ entweder 1 oder 2 angeben, um berechnete Elemente im Teilbereich zuzulassen.  
  
 Geben Sie zunächst den folgenden MDX-Ausdruck aus:  
  
```  
  
CREATE MEMBER [Adventure Works].[Geography].[Geography].[State-Province].&[WA]&[US].[Seattle Metro Agg]   
   AS  AGGREGATE(   
                 {   
                   [Geography].[Geography].[City].&[Bellevue]&[WA]  
                 , [Geography].[Geography].[City].&[Issaquah]&[WA]  
                 , [Geography].[Geography].[City].&[Redmond]&[WA]  
                 , [Geography].[Geography].[City].&[Seattle]&[WA]  
                 }  
                )    
```  
  
 Geben Sie dann die folgende MDX-Abfrage aus, um die in untergeordneten SELECT-Ausdrücken zulässigen berechneten Elemente anzuzeigen:  
  
```  
Select [Date].[Calendar Year].members on 0,  
       [Geography].[Geography].allmembers on 1  
from (Select {[Geography].[Geography].[State-Province].&[WA]&[US].[Seattle Metro Agg]} on 0 from [Adventure Works])  
Where [Measures].[Reseller Sales Amount]  
```  
  
 Sie erhalten folgende Ergebnisse:  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|KJ 2011|KJ 2012|KJ 2013|KJ 2014|  
|Seattle Metro Agg|$2.383.545,69|1$291.248,93|$763.557,02|$915.832,36|$412.907,37|  
  
 Wie bereits erläutert, sind die Vorgänger von [Seattle Metro] im zurückgegebenen Teilbereich nicht enthalten, wenn SubQueries=1 festgelegt ist. Aus diesem Grund enthält [Geography].[Geography].allmembers nur das berechnete Element.  
  
 Wenn das Beispiel mit der Einstellung SubQueries=2 in der Verbindungszeichenfolge ausgeführt wird, werden folgende Ergebnisse zurückgegeben:  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|KJ 2001|KJ 2002|KJ 2003|KJ 2004|  
|All Geographies|(null)|(null)|(null)|(null)|(null)|  
|United States|(null)|(null)|(null)|(null)|(null)|  
|Washington|(null)|(null)|(null)|(null)|(null)|  
|Seattle Metro Agg|$2.383.545,69|$291.248,93|$763.557,02|$915.832,36|$412.907,37|  
  
 Wie zuvor erläutert, sind die Vorgänger von [Seattle Metro] bei Verwendung von SubQueries=2 in dem zurückgegebenen Teilbereich enthalten. Für diese Elemente sind jedoch keine Werte verfügbar, da keine regulären Elemente vorhanden sind, die für die Aggregationen bereitgestellt werden. Aus diesem Grund werden für alle Vorgänger der berechneten Elemente in diesem Beispiel NULL-Werte zurückgegeben.  
  
 Um das oben beschriebene Verhalten zu verstehen, sollten Sie sich verdeutlichen, dass berechnete Elemente nicht wie reguläre Elemente zu den Aggregationen der übergeordneten Elemente beitragen. Dies bedeutet, dass eine Filterung ausschließlich nach berechneten Elementen leere Vorgänger zur Folge hat, da keine regulären Elemente vorhanden sind, die zu den aggregierten Werten des resultierenden Teilbereichs beitragen. Wenn Sie dem Filterausdruck reguläre Elemente hinzufügen, werden die aggregierten Werte aus diesen regulären Elementen genutzt. Fahren Sie mit obigem Beispiel fort und fügen Sie die Städte Portland in Oregon und Spokane in Washington zu der gleichen Achse hinzu, in der das berechnete Element angezeigt wird, wie im folgenden MDX-Ausdruck gezeigt:  
  
```  
Select [Date].[Calendar Year].members on 0,  
       [Geography].[Geography].allmembers on 1  
from (Select {  
               [Seattle Metro Agg]  
             , [Geography].[Geography].[City].&[Portland]&[OR]  
             , [Geography].[Geography].[City].&[Spokane]&[WA]  
             } on 0 from [Adventure Works]  
     )  
Where [Measures].[Reseller Sales Amount]  
```  
  
 Sie erhalten die folgenden Ergebnisse:  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|KJ 2001|KJ 2002|KJ 2003|KJ 2004|  
|All Geographies|$235.171,62|$419,46|$4.996,25|$131.788,82|$97.967,09|  
|United States|$235.171,62|$419,46|$4.996,25|$131.788,82|$97.967,09|  
|Oregon|$30.968,25|$419,46|$4.996,25|$17.442,97|$8.109,56|  
|Portland|$30.968,25|$419,46|$4.996,25|$17.442,97|$8.109,56|  
|97205|$30.968,25|$419,46|$4.996,25|$17.442,97|$8.109,56|  
|Washington|$204.203,37|(null)|(null)|$114.345,85|$89.857,52|  
|Spokane|$204.203,37|(null)|(null)|$114.345,85|$89.857,52|  
|99202|$204.203,37|(null)|(null)|$114.345,85|$89.857,52|  
|Seattle Metro Agg|$2.383.545,69|$291.248,93|$763.557,02|$915.832,36|$412.907,37|  
  
 In den obigen Ergebnissen werden die aggregierten Werte für [All Geographies], [United States], [Oregon] und [Washington] durch Aggregation der Nachfolger von &[Portland]&[OR] und &[Spokane]&[WA] erzeugt. Aus dem berechneten Element werden keine Werte abgerufen.  
  
### <a name="remarks"></a>Hinweise  
 In untergeordneten SELECT-Ausdrücken und Teilcubes sind nur globale oder in der Sitzung berechnete Elemente zulässig. Wenn der MDX-Ausdruck in einer Abfrage berechnete Elemente enthält, wird bei der Auswertung des untergeordneten SELECT-Ausdrucks oder Teilcubes ein Fehler ausgelöst.  
  
## <a name="see-also"></a>Siehe auch  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>   
 [Untergeordnete SELECT-Ausdrücke in Abfragen](../../../analysis-services/multidimensional-models/mdx/subselects-in-queries.md)   
 [Unterstützte XMLA-Eigenschaften &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md)  
  
  
