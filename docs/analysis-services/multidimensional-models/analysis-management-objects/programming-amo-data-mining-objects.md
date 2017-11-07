---
title: Programmieren von AMO, Datamining-Objekte | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- programming [AMO]
- data mining [AMO]
- AMO, data mining
- Analysis Management Objects, data mining
ms.assetid: d27f58b9-91be-449c-8403-439aa6dd1ff9
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3c4c398dbda7bc898d62ea16122ccfba02ea7d5b
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="programming-amo-data-mining-objects"></a>Programmieren von AMO-Data Mining-Objekten
  Das Programmieren von Data Mining-Objekten mithilfe von AMO ist unkompliziert und einfach. Der erste Schritt ist, das Datenstrukturmodell zu erstellen, um das Miningprojekt zu unterstützen. Anschließend erstellen Sie das Data Mining-Modell, das den Miningalgorithmus unterstützt, den Sie für die Vorhersage oder für die Ermittlung der Ihren Daten zugrundeliegenden unsichtbaren Beziehungen verwenden möchten. Nachdem Sie Ihr Miningprojekt erstellt haben (einschließlich Struktur und Algorithmus), können Sie die Miningmodelle verarbeiten, um die trainierten Modelle abzurufen, die Sie später verwenden, wenn Sie Abfragen und Vorhersagen über die Clientanwendung ausführen.  
  
 Dabei ist zu beachten, dass AMO nicht der Abfrage dient, sondern der Verwaltung und der Administration Ihrer Miningstrukturen und Modelle. Um die Daten abzufragen, verwenden Sie [Entwickeln mit ADOMD.NET](../../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md).  
  
 Dieses Thema enthält folgende Abschnitte:  
  
-   [MiningStructure-Objekte](#MiningStructure)  
  
-   [MiningModel-Objekte](#MiningModel)  
  
##  <a name="MiningStructure"></a>MiningStructure-Objekte  
 Eine Miningstruktur ist die Definition der Datenstruktur, die für die Erstellung aller Miningmodelle verwendet wird. Eine Miningstruktur enthält eine Bindung an eine Datenquellensicht, die in der Datenbank definiert ist, und Definitionen für alle Spalten, die am Miningmodell beteiligt sind. Eine Miningstruktur kann mehr als ein Miningmodell besitzen.  
  
 Erstellen einer <xref:Microsoft.AnalysisServices.MiningStructure> Objekt erfordert die folgenden Schritte aus:  
  
1.  Erstellen Sie das <xref:Microsoft.AnalysisServices.MiningStructure>-Objekt, und füllen Sie die grundlegenden Attribute auf. Grundlegende Attribute sind unter anderem Objektname, Objekt-ID (interne Identifikation) und Datenquellenbindung.  
  
2.  Erstellen Sie Spalten für das Modell. Spalten können entweder skalar oder Tabellendefinitionen sein.  
  
     Jede Spalte benötigt einen Namen und eine interne ID, einen Typ, eine Inhaltsdefinition und eine Bindung.  
  
3.  Aktualisieren Sie das <xref:Microsoft.AnalysisServices.MiningStructure>-Objekt auf dem Server, indem Sie die Update-Methode des Objekts verwenden.  
  
     Miningstrukturen können verabeitet werden und wenn Sie verarbeitet sind, werden die untergeordneten Miningmodelle verarbeitet oder erneut trainiert.  
  
 Der folgende Beispielcode erstellt eine Miningstruktur, um Verkäufe in einer Zeitreihe zu prognostizieren. Stellen Sie vor dem Ausführen des Beispielcodes, sicher, dass die Datenbank *Db*, als Parameter übergeben `CreateSalesForecastingMiningStructure`, enthält in `db.DataSourceViews[0]` einen Verweis auf die Ansicht *dbo.vTimeSeries* in der [!INCLUDE[ssAWDWsp](../../../includes/ssawdwsp-md.md)]-Beispieldatenbank.  
  
```  
public static MiningStructure CreateSalesForecastingMiningStructure(Database db)  
{  
    MiningStructure ms = db.MiningStructures.FindByName("Forecasting Sales Structure");  
    if (ms != null)  
        ms.Drop();  
    ms = db.MiningStructures.Add("Forecasting Sales Structure", "Forecasting Sales Structure");  
    ms.Source = new DataSourceViewBinding(db.DataSourceViews[0].ID);  
  
    ScalarMiningStructureColumn amount = ms.Columns.Add("Amount", "Amount");  
    amount.Type = MiningStructureColumnTypes.Double;  
    amount.Content = MiningStructureColumnContents.Continuous;  
    amount.KeyColumns.Add("vTimeSeries", "Amount", OleDbType.Currency);  
  
    ScalarMiningStructureColumn modelRegion = ms.Columns.Add("Model Region", "Model Region");  
    modelRegion.IsKey = true;  
    modelRegion.Type = MiningStructureColumnTypes.Text;  
    modelRegion.Content = MiningStructureColumnContents.Key;  
    modelRegion.KeyColumns.Add("vTimeSeries", "ModelRegion", OleDbType.WChar, 56);  
  
    ScalarMiningStructureColumn qty = ms.Columns.Add("Quantity", "Quantity");  
    qty.Type = MiningStructureColumnTypes.Long;  
    qty.Content = MiningStructureColumnContents.Continuous;  
    qty.KeyColumns.Add("vTimeSeries", "Quantity", OleDbType.Integer);  
  
    ScalarMiningStructureColumn timeIndex = ms.Columns.Add("TimeIndex", "TimeIndex");  
    timeIndex.IsKey = true;  
    timeIndex.Type = MiningStructureColumnTypes.Long;  
    timeIndex.Content = MiningStructureColumnContents.KeyTime;  
    timeIndex.KeyColumns.Add("vTimeSeries", "TimeIndex", OleDbType.Integer);  
  
    ms.Update();  
    return ms;  
}  
```  
  
##  <a name="MiningModel"></a>MiningModel-Objekte  
 Ein Miningmodell ist ein Repository für alle Spalten und Spaltendefinitionen, die in dem Miningalgorithmus verwendet werden.  
  
 Erstellen einer <xref:Microsoft.AnalysisServices.MiningModel> Objekt erfordert die folgenden Schritte aus:  
  
1.  Erstellen Sie das <xref:Microsoft.AnalysisServices.MiningModel>-Objekt, und füllen Sie die grundlegenden Attribute auf.  
  
     Grundlegende Attribute sind unter anderem Objektname, Objekt-ID (interne Identifikation) und Spezifikation des Miningalgorithmus.  
  
2.  Fügen Sie die Spalten dem Miningmodell hinzu. Eine der Spalten muss als Fallschlüssel definiert werden.  
  
3.  Aktualisieren Sie das <xref:Microsoft.AnalysisServices.MiningModel>-Objekt auf dem Server, indem Sie die Update-Methode des Objekts verwenden.  
  
     <xref:Microsoft.AnalysisServices.MiningModel>-Objekte können unabhängig von anderen Modellen der übergeordneten <xref:Microsoft.AnalysisServices.MiningStructure> verarbeitet werden.  
  
 Der folgende Beispielcode erstellt ein Microsoft Time Series-Planungsmodell auf der Grundlage der Miningstruktur "Forecasting Sales Structure".  
  
```  
public static MiningModel CreateSalesForecastingMiningModel(MiningStructure ms)  
{  
    if (ms.MiningModels.ContainsName("Sales Forecasting Model"))  
    {  
        ms.MiningModels["Sales Forecasting Model"].Drop();  
    }  
    MiningModel mm = ms.CreateMiningModel(true, "Sales Forecasting Model");  
    mm.Algorithm = MiningModelAlgorithms.MicrosoftTimeSeries;  
    mm.AlgorithmParameters.Add("PERIODICITY_HINT", "{12}");  
  
    MiningModelColumn amount = new MiningModelColumn();  
    amount.SourceColumnID = "Amount";  
    amount.Usage = MiningModelColumnUsages.Predict;  
  
    MiningModelColumn modelRegion = new MiningModelColumn();  
    modelRegion.SourceColumnID = "Model Region";  
    modelRegion.Usage = MiningModelColumnUsages.Key;  
  
    MiningModelColumn qty = new MiningModelColumn();  
    qty.SourceColumnID = "Quantity";  
    qty.Usage = MiningModelColumnUsages.Predict;  
  
    MiningModelColumn ti = new MiningModelColumn();  
    ti.SourceColumnID = "TimeIndex";  
    ti.Usage = MiningModelColumnUsages.Key;  
  
    mm.Update();  
    mm.Process(ProcessType.ProcessFull);  
    return mm;  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 <xref:Microsoft.AnalysisServices>   
 [Grundlegende AMO-Klassen](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-fundamental-classes.md)   
 [Einführung in AMO-Klassen](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [AMO-Klassen für Datamining](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-data-mining-classes.md)   
 [Logische Architektur &#40; Analysis Services – mehrdimensionale Daten &#41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [Datenbankobjekte &#40; Analysis Services – mehrdimensionale Daten &#41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  

