---
title: 'Lektion 5: Erstellen von Beziehungen | Microsoft Docs'
ms.custom: 
ms.date: 03/27/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: abac1a00-f827-4c3e-a473-6db5c8a3a66f
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 096f19dc25973b2d515c6ccfb9961e7b0fe07c21
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-4-create-relationships"></a>Lektion 4: Erstellen von Beziehungen
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

In dieser Lektion werden Sie Vergewissern Sie sich die Beziehungen, die automatisch erstellt wurden, wenn Sie Daten importiert und Hinzufügen neuer Beziehungen zwischen verschiedenen Tabellen. Eine Beziehung ist eine Verbindung zwischen zwei Tabellen, die festlegt, wie die Daten in diesen Tabellen miteinander in Beziehung gesetzt werden sollen. Die DimProduct-Tabelle und die DimProductSubcategory-Tabelle haben beispielsweise eine Beziehung, die darauf beruht, dass jedes Produkt zu einer Unterkategorie gehört. Weitere Informationen finden Sie unter [Beziehungen](../analysis-services/tabular-models/relationships-ssas-tabular.md).
  
Geschätzte Zeit zum Bearbeiten dieser Lektion: **10 Minuten**  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
Dieses Thema ist Teil eines Lernprogramms zur Tabellenmodellierung, das in der entsprechenden Reihenfolge bearbeitet werden sollte. Vor dem Ausführen der Aufgaben in dieser Lektion, Sie sollten haben die vorherige Lektion abgeschlossen: [Lektion 3: Markieren als Datumstabelle](../analysis-services/lesson-3-mark-as-date-table.md). 
  
## <a name="review-existing-relationships-and-add-new-relationships"></a>Überprüfen vorhandener Beziehungen und Hinzufügen neuer Beziehungen  
Wenn Sie Daten mithilfe des Tabellenimport-Assistenten importiert haben, können Sie sieben Tabellen aus der AdventureWorksDW-Datenbank haben. Wenn Sie Daten aus einer relationalen Quelle importieren, werden im Allgemeinen vorhandene Beziehungen automatisch zusammen mit den Daten importiert. Bevor Sie jedoch mit der Erstellung des Modells fortfahren, überprüfen Sie, ob die Beziehungen zwischen den Tabellen ordnungsgemäß erstellt wurden. In diesem Lernprogramm fügen Sie auch drei neue Beziehungen hinzu.  
  
#### <a name="to-review-existing-relationships"></a>So überprüfen Sie vorhandene Beziehungen  
  
1.  Klicken Sie auf die **Modell** Menü > **Modellansicht** > **Diagrammsicht**.  

    Der Modell-Designer wird jetzt in der Diagrammsicht angezeigt. Hierbei handelt es sich um ein grafisches Format, in dem alle von Ihnen importierten Tabellen mit Zeilen zwischen den Tabellen angezeigt werden. Die Zeilen zwischen den Tabellen geben die Beziehungen an, die automatisch beim Importieren der Daten erstellt wurden.
    
    ![als-tabellarische-lesson4-Diagramm](../analysis-services/media/as-tabular-lesson4-diagram.png)
  
    Verwenden Sie die Steuerelemente der Miniaturkarte unten rechts im Modell-Designer, um die Sicht so anzupassen, dass so viele Tabellen wie möglich berücksichtigt werden. Sie können auch mittels Klick und Ziehen Tabellen verschieben, näher zu einander positionieren oder in einer bestimmten Reihenfolge anordnen. Das Verschieben von Tabellen beeinflusst nicht die bereits zwischen den Tabellen bestehenden Beziehungen. Klicken Sie zum Anzeigen aller Spalten in einer bestimmten Tabelle auf einen Tabellenrand, und ziehen Sie diesen, um die Tabelle zu erweitern oder zu verkleinern.  
  
2.  Klicken Sie auf die durchgezogene Linie zwischen den **DimCustomer** Tabelle und die **DimGeography** Tabelle. Die durchgezogene Linie zwischen diesen zwei Tabellen zeigt an, dass diese Beziehung aktiv ist. Sie wird folglich bei der Berechnung von DAX-Formeln standardmäßig verwendet.  
  
    Beachten Sie, dass die **GeographyKey** Spalte in der **DimCustomer** Tabelle und die **GeographyKey** Spalte in der **DimGeography** Tabelle jetzt jeweils innerhalb eines Felds angezeigt werden. Dies gibt an, dass es sich hierbei um die in der Beziehung verwendeten Spalten handelt. Die Eigenschaften der Beziehung werden jetzt auch im Fenster **Eigenschaften** angezeigt.  
  
    > [!TIP]  
    > Zusätzlich zur Verwendung im Modell-Designers in der Diagrammsicht können können Sie auch im Dialogfeld "Beziehungen verwalten" Sie die Beziehungen zwischen allen Tabellen in einem Tabellenformat anzuzeigen. Mit der rechten Maustaste **Beziehungen** in tabellarischen Modell-Explorer, und klicken Sie dann auf **Beziehungen verwalten**. Das Dialogfeld "Beziehungen verwalten" zeigt der Beziehungen, die beim Importieren von Daten automatisch erstellt wurden.  
  
3.  Verwenden die Modell-Designer in Diagrammsicht oder das Dialogfeld "Beziehungen verwalten", um sicherzustellen, dass die folgenden Beziehungen erstellt wurden, die jede der Tabellen aus der AdventureWorksDW-Datenbank importiert wurde:  
  
    |Active|Tabelle|Verknüpfte Suchtabelle|  
    |----------|---------|------------------------|  
    |ja|**DimCustomer [GeographyKey]**|**DimGeography [GeographyKey]**|  
    |ja|**DimProduct [ProductSubcategoryKey]**|**DimProductSubcategory [ProductSubcategoryKey]**|  
    |ja|**DimProductSubcategory [ProductCategoryKey]**|**DimProductCategory [ProductCategoryKey]**|  
    |ja|**FactInternetSales [CustomerKey]**|**DimCustomer [CustomerKey]**|  
    |ja|**FactInternetSales [ProductKey]**|**DimProduct [ProductKey]**|  
  
    Wenn die Beziehungen in der obigen Tabelle nicht vorhanden sind, stellen Sie sicher, dass Ihr Modell in den folgenden Tabellen enthält: DimCustomer, DimDate, DimGeography, DimProduct, DimProductCategory, DimProductSubcategory und FactInternetSales. Werden Tabellen über die gleiche Datenquellenverbindung zu unterschiedlichen Zeitpunkten importiert, werden Beziehungen zwischen diesen Tabellen nicht automatisch erstellt, sondern sind manuell zu erstellen.  

### <a name="take-a-closer-look"></a>Nehmen Sie eine genauere Betrachtung
In der Diagrammsicht sehen Sie sich ein Pfeil ein Sternchen und eine Zahl auf die Zeilen, die die Beziehung zwischen Tabellen veranschaulichen.

![als tabellarische-lesson4-einzeilige](../analysis-services/media/as-tabular-lesson4-line.png)

Der Pfeil zeigt der filterrichtung das Sternchen zeigt diese Tabelle ist der n-Seite in der Kardinalität der Beziehung, und die 1 wird veranschaulicht, dass diese Tabelle auf der 1-Seite der Beziehung ist. Wenn Sie eine Beziehung bearbeiten müssen. z. B. ändern Sie die Beziehung filterrichtung oder Kardinalität zu, doppelklicken klicken Sie auf die Beziehungslinie in der Diagrammsicht, um das Dialogfeld "Beziehung bearbeiten" zu öffnen.

![als tabellarische-lesson4-bearbeiten](../analysis-services/media/as-tabular-lesson4-edit.png)

In den meisten Fällen müssen Sie nie eine Beziehung zu bearbeiten. Diese Funktionen für die erweiterte Modellieren von Daten vorgesehen sind und über den Rahmen dieses Lernprogramms sind. Weitere Informationen finden Sie unter [bidirektionale kreuzfilter für tabellarische Modelle in SQL Server 2016 Analysis Services](../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md).

In einigen Fällen müssen Sie möglicherweise zusätzliche Beziehungen zwischen Tabellen im Modell erstellen, um eine bestimmte Geschäftslogik zu unterstützen. Für dieses Lernprogramm müssen Sie drei zusätzliche Beziehungen zwischen der FactInternetSales-Tabelle und der DimDate-Tabelle zu erstellen.  
  
#### <a name="to-add-new-relationships-between-tables"></a>So fügen Sie neue Beziehungen zwischen Tabellen hinzu  
  
1.  Im Modell-Designer in der **FactInternetSales** Tabelle, klicken Sie auf, und warten Sie, den **OrderDate** Spalte ziehen Sie dann den Cursor an die **Datum** Spalte in der  **DimDate** Tabelle, und klicken Sie dann freigeben.  

    Eine durchgezogene Linie wird angezeigt, mit der Sie erstellt haben, eine aktive Beziehung zwischen der **OrderDate** Spalte in der **Internetverkäufe** Tabelle und die **Datum** Spalte in der **Datum** Tabelle. 
  
      ![als tabellarische-lesson4-neue](../analysis-services/media/as-tabular-lesson4-new.png) 
  
    > [!NOTE]  
    > Beim Erstellen von Beziehungen wird die Richtung "Kardinalität" und "Filtern" zwischen der primären Tabelle und der zugehörigen Nachschlagetabelle automatisch ausgewählt.  
  
2.  In der **FactInternetSales** Tabelle, klicken Sie auf, und warten Sie, die **DueDate** Spalte ziehen Sie dann den Cursor an die **Datum** Spalte in der **DimDate** Tabelle, und lassen Sie anschließend.  
  
    Eine gepunktete Linie wird angezeigt, mit der Sie erstellt haben, eine inaktive Beziehung zwischen der **DueDate** Spalte in der **FactInternetSales** Tabelle und die **Datum** Spalte in der  **DimDate** Tabelle. Mehrere Beziehungen zwischen Tabellen sind möglich. Doch nur eine Beziehung kann jeweils aktiv sein.  
  
3.  Erstellen Sie schließlich eine weitere Beziehung. in der **FactInternetSales** Tabelle, klicken Sie auf, und warten Sie, den **ShipDate** Spalte ziehen Sie dann den Cursor an die **Datum** Spalte in der **DimDate** Tabelle, und lassen Sie.  
    
     ![als-tabellarische-lesson4-newinactive](../analysis-services/media/as-tabular-lesson4-newinactive.png)
  
## <a name="whats-next"></a>Wie geht es weiter?
Wechseln Sie zur nächsten Lektion: [Lektion 5: Erstellen von berechneten Spalten](../analysis-services/lesson-5-create-calculated-columns.md).
  
  
  

