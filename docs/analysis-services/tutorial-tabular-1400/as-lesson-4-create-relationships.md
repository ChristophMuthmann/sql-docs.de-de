---
title: 'Analysis Services Tutorial Lektion 4: Erstellen von Beziehungen | Microsoft Docs'
description: Beschreibt, wie Beziehungen in der Analysis Services Tutorial-Projekt zu erstellen.
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: 
author: Minewiskan
manager: kfile
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 02/20/2018
ms.author: owend
ms.openlocfilehash: 2776649b049254e27851a9d4ce95e8d6dea81067
ms.sourcegitcommit: 7ed8c61fb54e3963e451bfb7f80c6a3899d93322
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/20/2018
---
# <a name="create-relationships"></a>Erstellen von Beziehungen

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

In dieser Lektion überprüfen Sie die Beziehungen, die automatisch erstellt wurden, wenn Sie Daten importiert und Hinzufügen neuer Beziehungen zwischen verschiedenen Tabellen. Eine Beziehung ist eine Verbindung zwischen zwei Tabellen, die festlegt, wie die Daten in diesen Tabellen miteinander in Beziehung gesetzt werden sollen. Die DimProduct-Tabelle und die DimProductSubcategory-Tabelle haben beispielsweise eine Beziehung, die darauf beruht, dass jedes Produkt zu einer Unterkategorie gehört. Weitere Informationen finden Sie unter [Beziehungen](../tabular-models/relationships-ssas-tabular.md).
  
Geschätzte Zeit zum Bearbeiten dieser Lektion: **10 Minuten**  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  

Dieser Artikel ist Teil eines Lernprogramms zur tabellenmodellierung, das in Reihenfolge absolviert werden sollte. Vor dem Ausführen der Aufgaben in dieser Lektion, Sie sollten haben die vorherige Lektion abgeschlossen: [Lektion 3: Markieren als Datumstabelle](../tutorial-tabular-1400/as-lesson-3-mark-as-date-table.md). 
  
## <a name="review-existing-relationships-and-add-new-relationships"></a>Überprüfen vorhandener Beziehungen und Hinzufügen neuer Beziehungen  

Beim Importieren von Daten mithilfe von Daten abrufen, erhalten Sie sieben Tabellen aus der AdventureWorksDW-Datenbank haben. Wenn Sie Daten aus einer relationalen Quelle importieren, werden im Allgemeinen vorhandene Beziehungen automatisch zusammen mit den Daten importiert. Damit Daten abrufen, um die automatische Erstellung von Beziehungen im Datenmodell können muss Beziehungen zwischen Tabellen in der Datenquelle vorhanden sein.

Bevor Sie mit der Erstellung des Modells fortfahren, sollten Sie überprüfen, dass die Beziehungen zwischen Tabellen ordnungsgemäß erstellt wurden. In diesem Lernprogramm fügen Sie auch drei neue Beziehungen hinzu.  

  
#### <a name="to-review-existing-relationships"></a>So überprüfen Sie vorhandene Beziehungen  
  
1.  Klicken Sie auf die **Modell** Menü > **Modellansicht** > **Diagrammsicht**.  

    Der Modell-Designer wird jetzt in der Diagrammsicht angezeigt importiert ein grafisches Format alle Tabellen Linien dazwischen. Die Zeilen zwischen den Tabellen geben die Beziehungen an, die automatisch beim Importieren der Daten erstellt wurden.
    
    ![Diagramm als lesson4](../tutorial-tabular-1400/media/as-lesson4-diagram.png)
  
    > [!NOTE]
    > Wenn Beziehungen zwischen Tabellen nicht angezeigt wird, bedeutet es wahrscheinlich, dass keine Beziehungen zwischen diesen Tabellen in der Datenquelle vorhanden sind.

    Beliebig viele Tabellen wie möglich enthalten Sie, mithilfe der miniaturkarte-Steuerelemente in der unteren rechten Ecke des Modell-Designer. Sie können auch mittels Klick und Ziehen Tabellen verschieben, näher zu einander positionieren oder in einer bestimmten Reihenfolge anordnen. Verschieben von Tabellen wirkt sich nicht auf die Beziehungen zwischen den Tabellen. Um alle Spalten in einer bestimmten Tabelle anzuzeigen, klicken Sie auf, und ziehen Sie eine Tabellenkante zu erweitern oder verkleinern Sie es aus.  
  
2.  Klicken Sie auf die durchgezogene Linie zwischen den **DimCustomer** Tabelle und die **DimGeography** Tabelle. Die durchgezogene Linie zwischen diesen beiden Tabellen wird gezeigt, dass diese Beziehung aktiv ist, d. h. es bei der Berechnung der DAX-Formeln standardmäßig verwendet wird.  
  
    Beachten Sie, dass die **GeographyKey** Spalte in der **DimCustomer** Tabelle und die **GeographyKey** Spalte in der **DimGeography** Tabelle jetzt jeweils innerhalb eines Felds angezeigt werden. Diese Spalten werden in der Beziehung verwendet. Die Eigenschaften der Beziehung werden jetzt auch im Fenster **Eigenschaften** angezeigt.  
  
    > [!TIP]  
    > Das Dialogfeld "Beziehungen verwalten" können auch die Beziehungen zwischen allen Tabellen in einem Tabellenformat anzuzeigen. Im tabellarischen Modell-Explorer mit der Maustaste **Beziehungen** > **Beziehungen verwalten**.
  
3.  Überprüfen Sie die folgenden Beziehungen erstellt wurden, als jede der Tabellen aus der AdventureWorksDW-Datenbank importiert wurden:  
  
    |Active|Tabelle|Verknüpfte Suchtabelle|  
    |----------|---------|------------------------|  
    |ja|**DimCustomer [GeographyKey]**|**DimGeography [GeographyKey]**|  
    |ja|**DimProduct [ProductSubcategoryKey]**|**DimProductSubcategory [ProductSubcategoryKey]**|  
    |ja|**DimProductSubcategory [ProductCategoryKey]**|**DimProductCategory [ProductCategoryKey]**|  
    |ja|**FactInternetSales [CustomerKey]**|**DimCustomer [CustomerKey]**|  
    |ja|**FactInternetSales [ProductKey]**|**DimProduct [ProductKey]**|  
  
    Wenn die Beziehungen fehlen, überprüfen Sie Ihr Modell enthält die folgenden Tabellen: DimCustomer, DimDate, DimGeography, DimProduct, DimProductCategory, DimProductSubcategory und FactInternetSales. Wenn an unterschiedlichen Zeitpunkten, Beziehungen zwischen Tabellen aus derselben Datenquelle Verbindung importiert werden, diese Tabellen werden nicht erstellt werden und müssen manuell erstellt werden. Wenn keine Beziehungen angezeigt werden, bedeutet dies, dass keine Beziehungen in der Datenquelle vorhanden sind. Sie können sie manuell in das Datenmodell erstellen.

### <a name="take-a-closer-look"></a>Nehmen Sie eine genauere Betrachtung

Beachten Sie in der Diagrammsicht einen Pfeil ein Sternchen und eine Zahl auf die Zeilen, die die Beziehung zwischen Tabellen veranschaulichen.

![Zeile als lesson4](../tutorial-tabular-1400/media/as-lesson4-line.png)

Der Pfeil zeigt die filterrichtung. Das Sternchen zeigt diese Tabelle ist die *viele* Seite in der Kardinalität der Beziehung, und die enthält diese Tabelle ist die *eine* Seite der Beziehung. Wenn Sie eine Beziehung bearbeiten müssen. z. B. ändern Sie die Beziehung filterrichtung oder Kardinalität zu, doppelklicken Sie auf die Beziehungslinie, um das Dialogfeld "Beziehung bearbeiten" zu öffnen.

![as-lesson4-edit](../tutorial-tabular-1400/media/as-lesson4-edit.png)

Diese Funktionen für die erweiterte Modellieren von Daten vorgesehen sind und über den Rahmen dieses Lernprogramms sind. Weitere Informationen finden Sie unter [bidirektionale kreuzfilter für tabellarische Modelle in Analysis Services](../tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md).

In einigen Fällen müssen Sie möglicherweise zusätzliche Beziehungen zwischen Tabellen im Modell erstellen, um eine bestimmte Geschäftslogik zu unterstützen. Für dieses Lernprogramm müssen Sie drei zusätzliche Beziehungen zwischen der FactInternetSales-Tabelle und der DimDate-Tabelle zu erstellen.  
  
#### <a name="to-add-new-relationships-between-tables"></a>So fügen Sie neue Beziehungen zwischen Tabellen hinzu  
  
1.  Im Modell-Designer in der **FactInternetSales** Tabelle auf, und warten Sie, die **OrderDate** Spalte ziehen Sie dann den Cursor an die **Datum** Spalte in der **DimDate** Tabelle, und lassen Sie anschließend.  

    Eine durchgezogene Linie wird angezeigt, mit der Sie erstellt haben, eine aktive Beziehung zwischen der **OrderDate** Spalte in der **Internet Sales** Tabelle, und die **Datum** Spalte in der **Datum** Tabelle. 
  
      ![als-lesson4-neu](../tutorial-tabular-1400/media/as-lesson4-new.png) 
  
    > [!NOTE]  
    > Beim Erstellen von Beziehungen wird die Richtung "Kardinalität" und "Filtern" zwischen der primären Tabelle und der zugehörigen Nachschlagetabelle automatisch ausgewählt.  
  
2.  In der **FactInternetSales** Tabelle, klicken Sie auf, und warten Sie, die **DueDate** Spalte ziehen Sie dann den Cursor an die **Datum** Spalte in der **DimDate** Tabelle, und lassen Sie anschließend.  
  
    Eine gepunktete Linie wird angezeigt, mit der Sie erstellt haben, eine inaktive Beziehung zwischen der **DueDate** Spalte in der **FactInternetSales** Tabelle, und die **Datum** Spalte in der **DimDate** Tabelle. Mehrere Beziehungen zwischen Tabellen sind möglich. Doch nur eine Beziehung kann jeweils aktiv sein. Inaktive Beziehungen können aktive zur Durchführung von spezieller Aggregationen in benutzerdefinierten DAX-Ausdrücken erfolgen.  
  
3.  Erstellen Sie abschließend eine weitere Beziehung. In der **FactInternetSales** Tabelle, klicken Sie auf, und warten Sie, die **ShipDate** Spalte ziehen Sie dann den Cursor an die **Datum** Spalte in der **DimDate** Tabelle, und lassen Sie anschließend.  
    
     ![as-lesson4-newinactive](../tutorial-tabular-1400/media/as-lesson4-newinactive.png)
  
## <a name="whats-next"></a>Wie geht es weiter?

[Lektion 5: Erstellen von berechneten Spalten](../tutorial-tabular-1400/as-lesson-5-create-calculated-columns.md).
  
  
  
