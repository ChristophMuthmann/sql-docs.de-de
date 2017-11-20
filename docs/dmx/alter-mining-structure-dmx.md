---
title: ALTER MINING STRUCTURE (DMX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_MINING_STRUCTURE
- ALTER MINING STRUCTURE
dev_langs:
- DMX
helpviewer_keywords:
- mining structures [DMX], creating
- WITH DRILLTHROUGH clause
- column definition lists [DMX]
- parameter lists [DMX]
- ALTER MINING STRUCTURE statement
ms.assetid: d1efd2a8-1a4d-47bc-ba7f-73a7c61e2fde
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 7ad24d223012bb301abc57f2fb48f34e112a7647
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="alter-mining-structure-dmx"></a>ALTER MINING STRUCTURE (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Erstellt ein neues Miningmodell, das auf einer vorhandenen Miningstruktur basiert.  Bei Verwendung der **ALTER MINING STRUCTURE** -Anweisung zum Erstellen eines neuen Miningmodells, die Struktur muss bereits vorhanden sein. Im Gegensatz dazu werden bei Verwendung die Anweisung [CREATE MINING MODEL &#40; DMX &#41;](../dmx/create-mining-model-dmx.md), erstellen Sie ein Modell und die zugrunde liegende Struktur automatisch zur gleichen Zeit zu generieren.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
ALTER MINING STRUCTURE <structure>  
ADD MINING MODEL <model>  
(  
    <column definition list>  
  [(<nested column definition list>) [WITH FILTER (<nested filter criteria>)]]  
)  
USING <algorithm> [(<parameter list>)]   
[WITH DRILLTHROUGH]  
[,FILTER(<filter criteria>)]  
```  
  
## <a name="arguments"></a>Argumente  
 *Struktur*  
 Der Name der Miningstruktur, der das Miningmodell hinzugefügt wird.  
  
 *model*  
 Ein eindeutiger Name für das Miningmodell.  
  
 *spaltendefinitionsliste*  
 Eine durch Trennzeichen getrennte Liste mit Spaltendefinitionen.  
  
 *geschachtelte spaltendefinitionsliste*  
 Eine durch Trennzeichen getrennte Liste der Spalten einer geschachtelten Tabelle, falls zutreffend.  
  
 *geschachtelte Filterkriterien*  
 Ein Filterausdruck, der für die Spalten in einer geschachtelten Tabelle übernommen wird.  
  
 *Algorithmus*  
 Der Name eines Data Mining-Algorithmus, der vom Anbieter definiert wurde.  
  
> [!NOTE]  
>  Eine Liste der vom aktuellen Anbieter unterstützten Algorithmen kann abgerufen werden, mithilfe von [DMSCHEMA_MINING_SERVICES-Rowset](../analysis-services/schema-rowsets/data-mining/dmschema-mining-services-rowset.md). So zeigen Sie in der aktuellen Instanz der unterstützten Algorithmen an [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], finden Sie unter [Data Mining Properties](../analysis-services/server-properties/data-mining-properties.md).  
  
 *Parameterliste*  
 Optional. Eine durch Trennzeichen getrennte Liste mit anbieterdefinierten Parametern für den Algorithmus.  
  
 *Filterkriterien*  
 Ein Filterausdruck, der für die Spalten in der Falltabelle übernommen wird.  
  
## <a name="remarks"></a>Hinweise  
 Wenn die Miningstruktur zusammengesetzte Schlüssel enthält, muss das Miningmodell alle Schlüsselspalten einschließen, die in der Struktur definiert sind.  
  
 Wenn für das Modell keine vorhersagbare Spalte erforderlich ist (z. B. bei Modellen, die mit dem [!INCLUDE[msCoName](../includes/msconame-md.md)] Clustering- oder dem [!INCLUDE[msCoName](../includes/msconame-md.md)] Sequence Clustering-Algorithmus erstellt wurden), müssen Sie in der Anweisung keine Spaltendefinition einschließen. Alle Attribute in dem sich ergebenden Modell werden als Eingaben behandelt.  
  
 In der **WITH** -Klausel, die für die Falltabelle angewendet wird. Sie können Optionen zum Filtern und Drillthrough angeben:  
  
-   Hinzufügen der **FILTER** -Schlüsselwort und eine filterbedingung. Der Filter wird auf die Fälle im Miningmodell angewendet.  
  
-   Hinzufügen der **DRILLTHROUGH** Schlüsselwort, um die Benutzer des Miningmodells einen Drilldown von modellergebnissen in die Falldaten ausführen können. In Data Mining Extensions (DMX), kann nur beim Erstellen des Modells Drillthrough aktiviert werden.  
  
 Um sowohl das Filtern als auch Drillthrough zu verwenden, kombinieren Sie die Schlüsselwörter in einer einzelnen **WITH** -Klausel, indem Sie die Syntax, die im folgenden Beispiel gezeigt:  
  
 `WITH DRILLTHROUGH, FILTER(Gender = 'Male')`  
  
## <a name="column-definition-list"></a>Spaltendefinitionsliste (Column Definition List)  
 Sie definieren die Struktur eines Modells, indem Sie eine Spaltendefinitionsliste angeben, die die folgenden Informationen für jede Spalte enthält:  
  
-   Name (obligatorisch)  
  
-   Alias (optional)  
  
-   Modellierungsflags  
  
-   Vorhersageanforderung, die für den Algorithmus anzeigt, ob die Spalte einen vorhersagbaren Wert enthält, angegeben durch die **PREDICT** oder **PREDICT_ONLY** Klausel  
  
 Verwenden Sie die folgende Syntax für die Spaltendefinitionsliste, wenn Sie eine einzelne Spalte definieren möchten:  
  
```  
<structure column name>  [AS <model column name>]  [<modeling flags>]    [<prediction>]  
```  
  
### <a name="column-name-and-alias"></a>Spaltenname und Alias  
 Der Spaltenname, den Sie in der Spaltendefinitionsliste verwenden, muss mit dem in der Miningstruktur verwendeten Spaltennamen identisch sein. Sie können jedoch optional einen Alias definieren, um die Strukturspalte im Miningmodell darzustellen. Außerdem können Sie mehrere Spaltendefinitionen für dieselbe Strukturspalte erstellen und jeder Kopie der Spalte einen anderen Alias und eine andere Vorhersageverwendung zuweisen. Standardmäßig wird der Name der Strukturspalte verwendet, falls Sie keinen Alias definieren. Weitere Informationen finden Sie unter [Erstellen eines Alias für eine Modellspalte](../analysis-services/data-mining/create-an-alias-for-a-model-column.md).  
  
 Für geschachtelte Tabellenspalten, Sie geben Sie den Namen der geschachtelten Tabelle, geben Sie die Daten als **Tabelle**, und geben Sie dann die Liste der geschachtelten Spalten im Modell eingeschlossen in Klammern eingeschlossen.  
  
 Sie können einen Filterausdruck definieren, der auf die geschachtelte Tabelle angewendet wird, indem Sie nach der Definition für die Spalte der geschachtelten Tabelle einen Filterkriterienausdruck anhängen.  
  
### <a name="modeling-flags"></a>Modellierungsflags  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] unterstützt die folgenden Modellierungsflags zur Verwendung in Miningmodellspalten:  
  
> [!NOTE]  
>  Das NOT NULL-Modellierungsflag gilt für die Miningstrukturspalte. Weitere Informationen finden Sie unter [CREATE MINING STRUCTURE &#40;DMX&#41;](../dmx/create-mining-structure-dmx.md).  
  
|||  
|-|-|  
|Begriff|Definition|  
|**REGRESSOR**|Zeigt an, dass der Algorithmus die angegebene Spalte in der Regressionsformel von Regressionsalgorithmen verwenden kann.|  
|**MODEL_EXISTENCE_ONLY**|Gibt an, dass die Werte für die Attributspalte weniger wichtig sind als das Vorhandensein der Attribute.|  
  
 Sie können mehrere Modellierungsflags für eine Spalte definieren. Weitere Informationen zur Verwendung von Modellierungsflags finden Sie unter [Modellierungsflags &#40; DMX &#41;](../dmx/modeling-flags-dmx.md).  
  
### <a name="prediction-clause"></a>Vorhersageklausel  
 Die Vorhersageklausel beschreibt, wie die Vorhersagespalte verwendet wird. In der folgenden Tabelle sind die möglichen Klauseln aufgelistet.  
  
|||  
|-|-|  
|**VORHERSAGEN**|Diese Spalte kann vom Modell vorhergesagt werden, und ihre Werte können als Eingabe verwendet werden, um den Wert anderer vorhersagbarer Spalten vorherzusagen.|  
|**PREDICT_ONLY**|Diese Spalte kann vom Modell vorhergesagt werden, aber ihre Werte können in Eingabefällen nicht dazu verwendet werden, den Wert anderer vorhersagbarer Spalten vorherzusagen.|  
  
## <a name="filter-criteria-expressions"></a>Filterkriterienausdrücke  
 Sie können einen Filter definieren, der die im Miningmodell verwendeten Fälle einschränkt. Der Filter kann auf die Spalten der Falltabelle, auf die Zeilen der geschachtelten Tabelle oder auf beides angewendet werden.  
  
 Filterkriterienausdrücke sind vereinfachte DMX-Prädikate und ähneln einer WHERE-Klausel. Filterausdrücke werden auf Formeln reduziert, die grundlegende mathematische Operatoren, Skalare und Spaltennamen verwenden. Eine Ausnahme bildet der EXISTS-Operator. Seine Auswertung ergibt TRUE, wenn mindestens eine Zeile für die Unterabfrage zurückgegeben wird. Prädikate können mit den allgemeinen logischen Operatoren kombiniert werden: AND, OR und NOT.  
  
 Weitere Informationen zu filtern, die mit Miningmodellen verwendet werden, finden Sie unter [Filter für Miningmodelle &#40; Analysis Services – Datamining &#41; ](../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md).  
  
> [!NOTE]  
>  Spalten in einem Filter müssen Miningstrukturspalten sein. Sie können keinen Filter für eine Modellspalte oder eine Spalte mit einem Alias erstellen.  
  
 Weitere Informationen zur DMX-Operatoren und Syntax finden Sie unter [Mining Model Columns](../analysis-services/data-mining/mining-model-columns.md).  
  
## <a name="parameter-definition-list"></a>Parameterdefinitionsliste (Parameter Definition List)  
 Durch Hinzufügen von Algorithmusparametern zur Parameterliste können Sie die Leistung und die Funktionsweise eines Modells anpassen. Die Parameter, die Sie verwenden können, hängen vom Algorithmus ab, den Sie in der USING-Klausel angeben. Eine Liste der Parameter, die jedem Algorithmus zugeordnet sind, finden Sie unter [Data Mining-Algorithmen &#40; Analysis Services – Datamining &#41; ](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
 Die Syntax der Parameterliste sieht wie folgt aus:  
  
```  
[<parameter> = <value>, <parameter> = <value>,…]  
```  
  
## <a name="example-1-add-a-model-to-a-structure"></a>Beispiel 1: Hinzufügen eines Modells zu einer Struktur  
 Im folgenden Beispiel wird ein Naive Bayes-Miningmodell, das **New Mailing** Miningstruktur und Grenzwerte für die maximale Anzahl der Attributstatus auf 50.  
  
```  
ALTER MINING STRUCTURE [New Mailing]  
ADD MINING MODEL [Naive Bayes]  
(  
    CustomerKey,   
    Gender,  
    [Number Cars Owned],  
    [Bike Buyer] PREDICT  
)  
USING Microsoft_Naive_Bayes (MAXIMUM_STATES = 50)  
```  
  
## <a name="example-2-add-a-filtered-model-to-a-structure"></a>Beispiel 2: Hinzufügen eines gefilterten Modells zu einer Struktur  
 Im folgenden Beispiel wird ein Miningmodell `Naive Bayes Women`, zu der **New Mailing** Miningstruktur. Das neue Modell verfügt über dieselbe grundlegende Struktur wie das Miningmodell, das in Beispiel 1 hinzugefügt wurde. Dieses Modell beschränkt die Fälle aus der Miningstruktur allerdings auf weibliche Kunden über 50 Jahre.  
  
```  
ALTER MINING STRUCTURE [New Mailing]  
ADD MINING MODEL [Naive Bayes Women]  
(  
    CustomerKey,   
    Gender,  
    [Number Cars Owned],  
    [Bike Buyer] PREDICT  
)  
USING Microsoft_Naive_Bayes  
WITH FILTER([Gender] = 'F' AND [Age] >50)  
```  
  
## <a name="example-3-add-a-filtered-model-to-a-structure-with-a-nested-table"></a>Beispiel 3: Hinzufügen eines gefilterten Modells zu einer Struktur mit einer geschachtelten Tabelle  
 Im folgenden Beispiel wird ein Miningmodell einer geänderten Version der Warenkorbminingstruktur hinzugefügt. Im Beispiel verwendete Miningstruktur wurde geändert, um das Hinzufügen einer **Region** Spalte, die Attribute für die Kundenregion enthält, und ein **Einkommensgruppe** Spalte, die Einkommen der Kunden mit den Werten kategorisiert **hohe**, **Moderate**, oder **niedrig**.  
  
 Die Miningstruktur schließt auch eine geschachtelte Tabelle ein, in der die Elemente, die der Kunde gekauft hat, aufgelistet werden.  
  
 Da die Miningstruktur eine geschachtelte Tabelle enthält, können Sie einen Filter auf die Falltabelle, die geschachtelte Tabelle oder beides anwenden. In diesem Beispiel werden ein Fallfilter und ein geschachtelter Zeilenfilter kombiniert, um die Fälle auf wohlhabende europäische Kunden zu beschränken, die eines der "Road"-Reifenmodelle gekauft haben.  
  
```  
ALTER MINING STRUCTURE [Market Basket with Region and Income]  
ADD MINING MODEL [Decision Trees]  
(  
    CustomerKey,   
    Region,  
    [Income Group],  
    [Product] PREDICT (Model)   
WITH FILTER (EXISTS (SELECT * FROM [v Assoc Seq Line Items] WHERE   
 [Model] = 'HL Road Tire' OR  
 [Model] = 'LL Road Tire' OR  
 [Model] = 'ML Road Tire' )  
)  
) WITH FILTER ([Income Group] = 'High' AND [Region] = 'Europe')  
USING Microsoft_Decision Trees  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datamining-Erweiterungen &#40; DMX &#41; Datendefinitionsanweisungen](../dmx/dmx-statements-data-definition.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Datenbearbeitungsanweisungen](../dmx/dmx-statements-data-manipulation.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; -Anweisungsreferenz](../dmx/data-mining-extensions-dmx-statements.md)  
  
  

