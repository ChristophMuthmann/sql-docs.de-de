---
title: ERSTELLEN VON MINING-MODELL (DMX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CREATE MINING MODEL
- CREATE
- CREATE_MINING_MODEL
dev_langs:
- DMX
helpviewer_keywords:
- RELATED TO column
- mining models [Analysis Services], creating
- column definition lists [DMX]
- parameter lists [DMX]
- SESSION clause
- CREATE MINING MODEL statement
ms.assetid: 43e4b591-7b34-494c-9b2d-7f0fe69af788
caps.latest.revision: 57
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 3c4720b0ecb2dcf3aa17f250a30f106ddd1e941f
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="create-mining-model-dmx"></a>CREATE MINING MODEL (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Erstellt sowohl ein neues Miningmodell als auch eine Miningstruktur in der Datenbank. Sie können ein Modell erstellen, indem Sie entweder das neue Modell in der Anweisung definieren oder PMML (Predictive Model Markup Language) verwenden. Diese zweite Möglichkeit empfiehlt sich nur für fortgeschrittene Benutzer.  
  
 Der Name der Miningstruktur ergibt sich, indem "_structure" an den Modellnamen angefügt wird. Dadurch ist sichergestellt, dass sich der Strukturname vom Modellnamen unterscheidet.  
  
 Verwenden Sie zum Erstellen eines Miningmodells für eine vorhandene Miningstruktur die [ALTER MINING STRUCTURE &#40; DMX &#41;](../dmx/alter-mining-structure-dmx.md) Anweisung.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CREATE [SESSION] MINING MODEL <model>  
(  
    [(<column definition list>)]  
)  
USING <algorithm> [(<parameter list>)] [WITH DRILLTHROUGH]  
CREATE MINING MODEL <model> FROM PMML <xml string>  
```  
  
## <a name="arguments"></a>Argumente  
 *model*  
 Ein eindeutiger Name für das Modell.  
  
 *spaltendefinitionsliste*  
 Eine durch Trennzeichen getrennte Liste mit Spaltendefinitionen.  
  
 *Algorithmus*  
 Der Name eines Data Mining-Algorithmus, der vom aktuellen Anbieter definiert wurde.  
  
> [!NOTE]  
>  Eine Liste der vom aktuellen Anbieter unterstützten Algorithmen kann abgerufen werden, mithilfe von [DMSCHEMA_MINING_SERVICES-Rowset](../analysis-services/schema-rowsets/data-mining/dmschema-mining-services-rowset.md). So zeigen Sie in der aktuellen Instanz der unterstützten Algorithmen an [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], finden Sie unter [Data Mining Properties](../analysis-services/server-properties/data-mining-properties.md).  
  
 *Parameterliste*  
 Optional. Eine durch Trennzeichen getrennte Liste mit anbieterdefinierten Parametern für den Algorithmus.  
  
 *XML-Zeichenfolge*  
 (Nur für fortgeschrittene Benutzer.) Ein XML-codiertes Modell (PMML). Die Zeichenfolge muss in einfache Anführungszeichen (') eingeschlossen werden.  
  
 Die **SITZUNG** -Klausel können Sie ein Miningmodell zu erstellen, die automatisch vom Server entfernt wird, wenn die Verbindung geschlossen oder das Timeout der Sitzung. **SITZUNG** -Miningmodelle sind nützlich, da den Benutzer ein Datenbankadministrator ist nicht erforderlich, und Speicherplatz für die sie nur verwenden, solange die Verbindung geöffnet ist.  
  
 Die **WITH DRILLTHROUGH** -Klausel aktiviert Drillthrough für das neue Miningmodell. Drillthrough kann nur aktiviert werden, wenn das Modell erstellt wird. Bei einigen Modelltypen ist ein Drillthrough erforderlich, um das Modell im benutzerdefinierten Viewer zu durchsuchen. Ein Drillthrough ist nicht erforderlich für Vorhersagen oder das Durchsuchen des Modells mit dem Microsoft Generic Content Tree Viewer.  
  
 Die **CREATE MINING MODEL** -Anweisung erstellt ein neues Miningmodell, das auf der spaltendefinitionsliste, dem Algorithmus und der algorithmusparameterliste basiert.  
  
### <a name="column-definition-list"></a>Spaltendefinitionsliste (Column Definition List)  
 Sie definieren die Struktur eines Modells, für das die Spaltendefinitionsliste verwendet wird, indem Sie für jede Spalte die folgenden Informationen einschließen:  
  
-   Name (obligatorisch)  
  
-   Datentyp (obligatorisch)  
  
-   Distribution  
  
-   Liste der Modellierungsflags  
  
-   Inhaltstyp (obligatorisch)  
  
-   Vorhersageanforderung, die für den Algorithmus, um vorherzusagen, diese Spalte gibt an, angegeben durch die **PREDICT** oder **PREDICT_ONLY** Klausel  
  
-   Beziehung zu einer Attributspalte (nur obligatorisch, wenn sie angewendet wird), angegeben durch die **RELATED TO** Klausel  
  
 Verwenden Sie die folgende Syntax für die spaltendefinitionsliste, um eine einzelne Spalte zu definieren:  
  
```  
<column name>    <data type>    [<Distribution>]    [<Modeling Flags>]    <Content Type>    [<prediction>]    [<column relationship>]   
```  
  
 Verwenden Sie die folgende Syntax für die spaltendefinitionsliste, um eine geschachtelte Tabellenspalte zu definieren:  
  
```  
<column name>    TABLE    [<prediction>] ( <non-table column definition list> )  
```  
  
 Zum Definieren einer Spalte können Sie jeweils nur eine Klausel aus einer bestimmten Gruppe verwenden. Die einzige Ausnahme bilden Modellierungsflags. Sie können mehrere Modellierungsflags für eine Spalte definieren.  
  
 Eine Liste der Datentypen, Inhaltstypen, Spaltendistributionen und Modellierungsflags, mit denen Sie eine Spalte definieren können, finden Sie in den folgenden Themen:  
  
-   [Datentypen &#40; Datamining &#41;](../analysis-services/data-mining/data-types-data-mining.md)  
  
-   [Content-Arten &#40; Datamining &#41;](../analysis-services/data-mining/content-types-data-mining.md)  
  
-   [Spaltenverteilungen &#40; Datamining &#41;](../analysis-services/data-mining/column-distributions-data-mining.md)  
  
-   [Modellieren von Ablaufverfolgungsflags &#40; Datamining &#41;](../analysis-services/data-mining/modeling-flags-data-mining.md)  
  
 Sie können der Anweisung eine Klausel hinzufügen, um die Beziehung zwischen zwei Spalten zu beschreiben. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]unterstützt die Verwendung der folgenden \<Column Relationship >-Klausel.  
  
 **IM ZUSAMMENHANG MIT**  
 Diese Form kennzeichnet eine Wertehierarchie. Das Ziel einer RELATED TO-Spalte kann eine Schlüsselspalte einer geschachtelten Tabelle, eine Spalte mit diskreten Werten in der Fallzeile oder eine andere Spalte mit einer RELATED TO-Klausel sein, wodurch eine tiefere Hierarchie gekennzeichnet ist.  
  
 Mit einer Vorhersageklausel können Sie beschreiben, wie die Vorhersagespalte verwendet wird. In der folgenden Tabelle sind die beiden möglichen Klauseln beschrieben.  
  
|\<Vorhersage >-Klausel|Description|  
|---------------------------|-----------------|  
|**PREDICT**|Diese Spalte kann vom Modell vorhergesagt werden, und sie kann in Eingabefällen bereitgestellt werden, um den Wert anderer vorhersagbarer Spalten vorherzusagen.|  
|**PREDICT_ONLY**|Diese Spalte kann vom Modell vorhergesagt werden, aber ihre Werte können in Eingabefällen nicht dazu verwendet werden, den Wert anderer vorhersagbarer Spalten vorherzusagen.|  
  
### <a name="parameter-definition-list"></a>Parameterdefinitionsliste (Parameter Definition List)  
 Mit der Parameterliste können Sie die Leistung und die Funktionsweise eines Miningmodells anpassen. Die Syntax der Parameterliste sieht wie folgt aus:  
  
```  
[<parameter> = <value>, <parameter> = <value>,…]  
```  
  
 Eine Liste der Parameter, die jedem Algorithmus zugeordnet sind, finden Sie unter [Data Mining-Algorithmen &#40; Analysis Services – Datamining &#41; ](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
## <a name="remarks"></a>Hinweise  
 Wenn Sie ein Modell mit einem integrierten Testdataset erstellen möchten, sollten Sie die Anweisung CREATE MINING STRUCTURE gefolgt von ALTER MINING STRUCTURE verwenden. Jedoch unterstützen nicht alle Modelltypen ein zurückgehaltenes Dataset. Weitere Informationen finden Sie unter [CREATE MINING STRUCTURE &#40;DMX&#41;](../dmx/create-mining-structure-dmx.md).  
  
 Eine exemplarische Vorgehensweise zum Erstellen eines Miningmodells mit der CREATEMODEL-Anweisung finden Sie unter [DMX-Lernprogramm für Zeitreihenvorhersagen](http://msdn.microsoft.com/library/38ea7c03-4754-4e71-896a-f68cc2c98ce2).  
  
## <a name="naive-bayes-example"></a>Beispiel für Naive Bayes-Algorithmus  
 Im folgenden Beispiel wird der [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes-Algorithmus verwendet, um ein neues Miningmodell zu erstellen. Die Bike Buyer-Spalte ist als das vorhersagbare Attribut definiert.  
  
```  
CREATE MINING MODEL [NBSample]  
(  
    CustomerKey LONG KEY,   
    Gender TEXT DISCRETE,  
    [Number Cars Owned] LONG DISCRETE,  
    [Bike Buyer] LONG DISCRETE PREDICT  
)  
USING Microsoft_Naive_Bayes  
```  
  
## <a name="association-model-example"></a>Beispiel für Association-Algorithmus  
 Im folgenden Beispiel wird der [!INCLUDE[msCoName](../includes/msconame-md.md)] Association-Algorithmus verwendet, um ein neues Miningmodell zu erstellen. Für die Anweisung wird die Möglichkeit genutzt, eine Tabelle in einer Modelldefinition zu schachteln, indem eine Tabellenspalte verwendet wird. Das Modell geändert wird, mithilfe der *MINIMUM_PROBABILITY* und *MINIMUM_SUPPORT* Parameter.  
  
```  
CREATE MINING MODEL MyAssociationModel (  
    OrderNumber TEXT KEY,  
    [Products] TABLE PREDICT (  
        [Model] TEXT KEY  
    )  
)  
USING Microsoft_Association_Rules (Minimum_Probability = 0.1, MINIMUM_SUPPORT = 0.01)  
```  
  
## <a name="sequence-clustering-example"></a>Beispiel für den Sequence Clustering-Algorithmus  
 Im folgenden Beispiel wird der [!INCLUDE[msCoName](../includes/msconame-md.md)] Sequence Clustering-Algorithmus verwendet, um ein neues Miningmodell zu erstellen. Das Modell wird mit zwei Schlüsseln definiert. Die OrderNumber-Spalte wird als Fallschlüssel verwendet und gibt einzelne Bestellungen. Die Zeilennummer-Spalte als Schlüsselspalte der geschachtelten Tabelle verwendet wird, und gibt die Reihenfolge, in der Elemente einer Bestellung hinzugefügt wurden.  
  
```  
CREATE MINING MODEL BuyingSequence (  
    [Order Number] TEXT KEY,  
    [Products] TABLE   
     (  
        [Line Number] LONG KEY SEQUENCE,  
        [Model] TEXT DISCRETE PREDICT  
    )  
)  
USING Microsoft_Sequence_Clustering  
```  
  
## <a name="time-series-example"></a>Beispiel für den Time Series-Algorithmus  
 Im folgenden Beispiel wird der [!INCLUDE[msCoName](../includes/msconame-md.md)]-Zeitreihenalgorithmus verwendet, um mit dem ARTxp-Algorithmus ein neues Miningmodell zu erstellen. Berichtsdatum ist die Schlüsselspalte für die Zeitreihe, und ModelRegion ist die Schlüsselspalte für die Datenreihe. In diesem Beispiel wird davon ausgegangen, dass die Periodizität der Daten alle 12 Monate ist. Aus diesem Grund die *PERIODICITY_HINT* -Parameter auf 12 festgelegt ist.  
  
> [!NOTE]  
>  Sie müssen angeben, die *PERIODICITY_HINT* -Parameter mit geschweiften Klammern. Darüber hinaus, da der Wert eine Zeichenfolge ist, er muss werden eingeschlossen in einfache Anführungszeichen eingeschlossen: "{\<numerischen Wert >}".  
  
```  
CREATE MINING MODEL SalesForecast (  
        ReportingDate DATE KEY TIME,  
        ModelRegion TEXT KEY,  
        Amount LONG CONTINUOUS PREDICT,  
        Quantity LONG CONTINUOUS PREDICT  
)  
USING Microsoft_Time_Series (PERIODICITY_HINT = '{12}', FORECAST_METHOD = 'ARTXP')  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datamining-Erweiterungen &#40; DMX &#41; Datendefinitionsanweisungen](../dmx/dmx-statements-data-definition.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Datenbearbeitungsanweisungen](../dmx/dmx-statements-data-manipulation.md)   
 [Data Mining-Erweiterungen &#40;DMX&#41; – Anweisungsreferenz](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
