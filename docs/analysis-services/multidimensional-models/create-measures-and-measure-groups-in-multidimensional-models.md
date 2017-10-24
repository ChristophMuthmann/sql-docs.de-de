---
title: Erstellen von Measures und Measuregruppen in mehrdimensionalen Modellen | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- measure groups [Analysis Services], defining
ms.assetid: 1018bb2e-b89b-489e-aead-450dec5dca3b
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8dc45f7d47484dbc3b1d5e7684f4e3a5d3075dc2
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-measures-and-measure-groups-in-multidimensional-models"></a>Erstellen von Measures und Measuregruppen in mehrdimensionalen Modellen
  Ein *Measure* ist eine Aggregation numerischer Datenwerten, z. B. Summe, Anzahl, Minimum, Maximum, Mittelwert, oder eines benutzerdefinierten MDX-Ausdrucks, den Sie erstellen. Eine *Measuregruppe* ist ein Container für ein oder mehrere Measures. Alle Measures befinden sich in einer Measuregruppe, auch wenn es nur ein Measure gibt. Ein Cube muss über mindestens ein Measure und eine Measuregruppe verfügen.  
  
 Dieses Thema enthält folgende Abschnitte:  
  
-   [Ansätze zum Erstellen von Measures](#bkmk_create)  
  
-   [Komponenten eines Measures](#bkmk_comps)  
  
-   [Modellierung von Measures und Measuregruppen zu Fakten und Faktentabellen](#bkmk_modeling)  
  
-   [Granularität einer Measuregruppe](#bkmk_grain)  
  
##  <a name="bkmk_create"></a> Ansätze zum Erstellen von Measures  
 Measures können ein statisches Element des Cubes sein, die zur Entwurfszeit erstellt werden und immer vorhanden sind, wenn auf den Cube zugegriffen wird. Sie können ein Measure aber auch als *berechnetes Element* mithilfe eines MDX-Ausdrucks definieren, um einen berechneten Wert für ein Measure basierend auf anderen Measures im Cube bereitzustellen. Ein berechnetes Element kann auf die Sitzung oder den Benutzer begrenzt werden.  
  
 Verwenden Sie einen der folgenden Ansätze, um ein Measure oder eine Measuregruppe zu erstellen:  
  
|||  
|-|-|  
|Cube-Assistent|Führen Sie den Cube-Assistenten in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] aus, um einen Cube zu erstellen.<br /><br /> Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf **Cubes**, und wählen Sie **Neuer Cube** aus. Hilfe zu diesen Schritten finden Sie unter [Mehrdimensionale Modellierung &#40;Adventure Works-Tutorial&#41;](../../analysis-services/multidimensional-modeling-adventure-works-tutorial.md).<br /><br /> Wenn Sie einen Cube anhand von Tabellen aus einem vorhandenen Data Warehouse erstellen, materialisieren sich Definitionen für die Measures und Measuregruppen als Teil des Erstellungsprozesses des Cube. Im Assistenten können Sie auswählen, welche Fakten und Faktentabellen als Grundlage für das Measure und Measuregruppenobjekte im Cube verwendet werden sollen.|  
|Dialogfeld "Neues Measure"|Vorausgesetzt, dass der Cube bereits in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]vorhanden ist, doppelklicken Sie auf den Cubenamen im Projektmappen-Explorer, um ihn im Cube-Designer zu öffnen. Klicken Sie im Bereich der Measures mit der rechten Maustaste auf den obersten Knoten, um eine neue Measuregruppe oder neue Measures zu erstellen, indem Sie eine Quelltabelle, eine Spalte und einen Aggregationstyp angeben. Bei diesem Ansatz müssen Sie die Aggregationsmethode aus einer festen Liste mit vorgefertigten Funktionen auswählen. Unter [Use Aggregate Functions](../../analysis-services/multidimensional-models/use-aggregate-functions.md) finden Sie eine Erläuterung der häufiger verwendeten Aggregationen.|  
|berechnetes Element|Berechnete Elemente fügen einem Cube in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Flexibilität und Analysefunktionen hinzu, da Sie steuern können, wann und wie sie erstellt werden. Manchmal benötigen Sie ein Measure nur vorübergehend für die Dauer einer Benutzersitzung oder in Management Studio als Teil einer Untersuchung.<br /><br /> Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]die Registerkarte Berechnungen, um ein neues berechnetes Element zu erstellen.<br /><br /> Wählen Sie diesen Ansatz, um ein Measure auf Grundlage eines MDX-Ausdrucks zu erstellen. Weitere Informationen finden Sie in den folgenden Themen: [Erstellen von Measures in MDX](../../analysis-services/multidimensional-models/mdx/mdx-building-measures.md), [Berechnungen](../../analysis-services/multidimensional-models-olap-logical-cube-objects/calculations.md), [Berechnungen in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md) und [Grundlegendes zu MDX-Skripts &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md).|  
|MDX oder XMLA|In SQL Server Management Studio können Sie MDX oder XMLA ausführen, um eine Datenbank zu ändern und ein neues berechnetes Measure einzubeziehen. Dieser Ansatz eignet sich für Ad-hoc-Tests von Daten, nachdem die Projektmappe auf einem Server bereitgestellt wurde. Siehe [Document and Script an Analysis Services Database](../../analysis-services/multidimensional-models/document-and-script-an-analysis-services-database.md).|  
  
##  <a name="bkmk_comps"></a> Komponenten eines Measures  
 Ein Measure ist ein Objekt mit Eigenschaften. Neben dem Namen benötigt ein Measure einen Aggregationstyp und eine Quellspalte oder einen Ausdruck, um das Measure mit Daten zu laden. Sie können die Measuredefinition durch Einstellen der Eigenschaften ändern.  
  
|||  
|-|-|  
|**Quelle**|Die meisten Measures stammen aus numerischen Spalten in Faktentabellen in einem externen Data Warehouse, z. B. die Spalte "Betrag der Verkäufe" in den Tabellen "Internetverkäufe" und "Verkäufe des Wiederverkäufers" im AdventureWorks-Data Warehouse. Sie können aber auch neue Measures erstellen, die vollkommen auf von Ihnen definierten Berechnungen basieren.<br /><br /> Attributspalten aus Dimensionstabellen können zum Definieren von Measures verwendet werden. Diese Measures sind jedoch im Allgemeinen hinsichtlich ihres Aggregationsverhaltens semiadditiv oder nicht additiv. Weitere Informationen zum semiadditiven Aggregationsverhalten finden Sie unter [Semiadditives Verhalten definieren](../../analysis-services/multidimensional-models/define-semiadditive-behavior.md).|  
|**Aggregation**|Standardmäßig werden Measures über die einzelnen Dimensionen hinweg summiert. Die **AggregateFunction** -Eigenschaft bietet Ihnen jedoch die Möglichkeit, dieses Verhalten zu ändern. Eine Liste finden Sie unter [Use Aggregate Functions](../../analysis-services/multidimensional-models/use-aggregate-functions.md) .|  
|**Eigenschaften**|Zusätzliche Beschreibungen der Eigenschaften finden Sie unter [Configure Measure Properties](../../analysis-services/multidimensional-models/configure-measure-properties.md) .|  
  
##  <a name="bkmk_modeling"></a> Modellierung von Measures und Measuregruppen zu Fakten und Faktentabellen  
 Bevor Sie einen Assistenten ausführen, sollten Sie die Modellierungsprinzipien hinter der Measuredefinition kennen.  
  
 Measures und Measuregruppen sind die mehrdimensionalen Objekte, die Fakten und Faktentabellen in einem externen Data Warehouse darstellen. In den meisten Fällen basieren Measures und Measuregruppen auf Objekten in einer Datenquellensicht, die wiederum aus dem zugrundeliegenden Data Warehouse erstellt werden.  
  
 Das folgende Diagramm stellt die **FactSalesQuota** -Faktentabelle und die beiden zugehörigen Dimensionstabellen **DimTime** und **DimEmployee**dar. Diese Tabellen werden im Adventure Works-Beispielcube als Grundlage für die "Sales Quotas"-Measuregruppe und die Dimensionen "Time" und "Employee" verwendet.  
  
 ![FactSalesQuota-Tabelle mit zwei Dimensionstabellen](../../analysis-services/multidimensional-models/media/factsalesquota.gif "FactSalesQuota-Tabelle mit zwei Dimensionstabellen")  
  
 Die Faktentabelle enthält zwei grundlegende Spaltentypen: Attributspalten und Measurespalten.  
  
-   Attributspalten werden verwendet, um Fremdschlüsselbeziehungen zu Dimensionstabellen zu erstellen, damit die quantifizierbaren Daten in den Measurespalten nach den Daten in den Dimensionstabellen organisiert werden können. Attributspalten werden auch verwendet, um die Granularität einer Faktentabelle und der zugehörigen Measuregruppe zu definieren.  
  
-   Measurespalten definieren die in einer Measuregruppe enthaltenen Measures.  
  
 Wenn Sie den Cube-Assistenten ausführen, werden die Fremdschlüssel herausgefiltert. In der Liste der verbleibenden Spalten, aus denen Sie auswählen können, sehen Sie Measurespalten sowie Attributspalten, die nicht als Fremdschlüssel gekennzeichnet sind. Im Beispiel **FactSalesQuote** beispielsweise bietet der Assistent neben **SalesAmountQuota** die Optionen **CalendarYear** und **CalendarQuarter**. Nur die Measurespalte **SalesAmountQuota** ergibt eine praktikable Maßnahme für Ihr mehrdimensionales Modell. Durch die anderen datenbasierten Spalten werden die einzelnen Kontingentmengen qualifiziert. Sie sollten die anderen Spalten **CalendarYear** und **CalendarQuarter**aus der Liste der Measures im Cube-Assistenten ausschließen (oder sie später im Designer aus der Measuregruppe entfernen).  
  
 Vorweg sei darauf hingewiesen, dass sich nicht alle vom Assistenten angebotenen Spalten als Measure eignen. Verlassen Sie sich auf Ihre Kenntnisse der Daten und ihrer Verwendung, wenn Sie entscheiden, welche Spalten Sie als Measures verwenden. Denken Sie daran, dass Sie mit der rechten Maustaste auf eine Tabelle in der Datenquellensicht klicken können, um die Daten anzuzeigen. Dies kann Ihnen helfen, zu bestimmen, welche Spalten als Measures verwendet werden sollten. Weitere Informationen finden Sie unter [Durchsuchen von Daten in einer Datenquellensicht &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/explore-data-in-a-data-source-view-analysis-services.md).  
  
> [!NOTE]  
>  Nicht alle Measures werden direkt aus einem in einer Spalte der Faktentabelle gespeicherten Wert abgeleitet. So basiert beispielsweise das **Sales Person Count** -Measure, das in der **Sales Quota** -Measuregruppe des Adventure Works-Beispielcubes definiert ist, tatsächlich auf der Anzahl eindeutiger Werte (oder Distinct Count) in der Spalte **EmployeeKey** der Faktentabelle **FactSalesQuota** .  
  
##  <a name="bkmk_grain"></a> Granularität einer Measuregruppe  
 Measuregruppen verfügen über eine zugeordnete Granularität, die auf die von einer Faktentabelle unterstützte Detailebene verweist. Die Granularität ist über die Fremdschlüssel-Beziehung zu einer Dimension festgelegt.  
  
 Beispielsweise hat die Faktentabelle **FactSalesQuota** eine Fremdschlüsselbeziehung zur Tabelle **DimEmployee** , jeder Datensatz in der Tabelle **FactSalesQuota** steht in Beziehung zu einem Mitarbeiter. Die Granularität der Measuregruppe befindet sich aus Sicht der Employee-Dimension also auf der Ebene einzelner Mitarbeiter.  
  
 Die Granularität einer Measuregruppe kann nicht stärker differenziert werden als die unterste Ebene der Dimension, von der die Measuregruppe betrachtet wird. Mithilfe zusätzlicher Attribute kann jedoch eine gröbere Granularität festgelegt werden. Die **FactSalesQuota** -Faktentabelle verwendet beispielsweise drei Spalten, **TimeKey**, **CalendarYear**und **CalendarQuarter**, um die Granularität einer Beziehung mit der **DimTime** -Tabelle festzulegen. Als Folge davon befindet sich die Granularität der Measuregruppe aus Sicht der Zeitdimension auf der Ebene des Kalenderquartals und nicht des Tages, der niedrigsten Ebene der Zeitdimension.  
  
 Sie können die Granularität einer Measuregruppe in Bezug auf eine bestimmte Dimension mithilfe der Registerkarte **Dimensionsverwendung** des Cube-Designers angeben. Weitere Informationen zu Dimensionsbeziehungen finden Sie unter [Dimension Relationships](../../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Cubes in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/cubes-in-multidimensional-models.md)   
 [Measures und Measuregruppen](../../analysis-services/multidimensional-models/measures-and-measure-groups.md)  
  
  

