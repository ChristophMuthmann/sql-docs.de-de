---
title: Verarbeiten von Objekten (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 02/14/2018
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- errors [XML for Analysis]
- objects [XML for Analysis]
- XML for Analysis, objects
- XMLA, partitions
- partitions [Analysis Services], XML for Analysis
- XML for Analysis, partitions
- writeback [Analysis Services], XML for Analysis
- out-of-line bindings
- processing objects [XML for Analysis]
- XMLA, objects
ms.assetid: a65b3249-303d-49c6-98af-6ac6eed11a03
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: dffffec4424ed00921d2c9150330c6293c6f77da
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="processing-objects-xmla"></a>Verarbeiten von Objekten (XMLA)
  In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], Verarbeitung den Schritt bzw. Reihe von Schritten, durch Daten in Informationen für Geschäftsanalysen umgewandelt. Die Verarbeitung ist je nach Objekttyp unterschiedlich, aber immer Teil einer Umwandlung von Daten in Informationen.  
  
 Prozess ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Objekt können Sie die [Prozess](../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md) Befehl. Die **Prozess** Befehl kann die folgenden Objekte verarbeiten, auf eine [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Instanz:  
  
-   Cubes  
  
-   Datenbanken  
  
-   Dimensionen  
  
-   Measuregruppen  
  
-   Miningmodelle  
  
-   Miningstrukturen  
  
-   Partitionen  
  
 Zum Steuern der Verarbeitung von Objekten, die **Prozess** Befehl verfügt über verschiedene Eigenschaften, die festgelegt werden können. Die **Prozess** Befehl verfügt über Eigenschaften, mit denen gesteuert: wie viel Verarbeitung stattfinden wird, welche Objekte verarbeitet werden, ob Out-of-Line-Bindungen verwendet, wie Fehler behandelt und wie Rückschreibetabellen verwaltet.  
  
## <a name="specifying-processing-options"></a>Angeben von Verarbeitungsoptionen  
 Die [Typ](../../analysis-services/xmla/xml-elements-properties/type-element-xmla.md) Eigenschaft von der **Prozess** Befehl gibt die Verarbeitungsoption zu verwenden, wenn das Objekt zu verarbeiten. Weitere Informationen zu Verarbeitungsoptionen finden Sie unter [Verarbeitungsoptionen und -einstellungen &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md).  
  
 Die folgende Tabelle enthält die Konstanten für die **Typ** -Eigenschaft und die verschiedenen Objekte, die über die Konstanten verarbeitet werden können.  
  
|**Typ** Wert|Anwendbare Objekte|  
|--------------------|------------------------|  
|*"ProcessFull"*|Cube, Datenbank, Dimension, Measuregruppe, Miningmodell, Miningstruktur, Partition|  
|*"Processadd"*|Dimension, Partition|  
|*ProcessUpdate*|Dimension|  
|*ProcessIndexes*|Dimension, Cube, Measuregruppe, Partition|  
|*ProcessData*|Dimension, Cube, Measuregruppe, Partition|  
|*ProcessDefault*|Cube, Datenbank, Dimension, Measuregruppe, Miningmodell, Miningstruktur, Partition|  
|*ProcessClear*|Cube, Datenbank, Dimension, Measuregruppe, Miningmodell, Miningstruktur, Partition|  
|*ProcessStructure*|Cube, Miningstruktur|  
|*' ProcessClearStructureOnly '*|Miningstruktur|  
|*ProcessScriptCache*|Cube|  
  
 Weitere Informationen zur Verarbeitung [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] anzuzeigen, [Verarbeiten eines mehrdimensionalen Modells &#40; Analysis Services &#41; ](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
## <a name="specifying-objects-to-be-processed"></a>Angeben zu verarbeitender Objekte  
 Die [Objekt](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md) Eigenschaft von der **Prozess** Befehl enthält den Objektbezeichner des Objekts, das verarbeitet werden. Kann nur ein Objekt angegeben werden, einem **Prozess** -Befehl, aber die Verarbeitung eines Objekts verarbeitet auch alle untergeordneten Objekte. Beispielsweise werden bei der Verarbeitung einer Measuregruppe in einem Cube alle Partitionen für diese Measuregruppe verarbeitet, während bei der Verarbeitung einer Datenbank alle Objekte, die in der Datenbank enthalten sind, verarbeitet werden, einschließlich Cubes, Dimensionen und Miningstrukturen.  
  
 Wenn Sie festlegen, die **ProcessAffectedObjects** Attribut der **Prozess** auf "true", Befehl werden alle verwandten Objekts, das durch die Verarbeitung des angegebenen Objekts betroffen sind, ebenfalls verarbeitet. Angenommen, eine Dimension mit inkrementell aktualisiert wird die *ProcessUpdate* Verarbeitungsoption in der **Prozess** -Befehl eine Partition, deren Aggregationen sind Elementen für ungültig erklärt, werden Hinzufügen oder löschen, wird auch vom verarbeitet [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Wenn **ProcessAffectedObjects** festgelegt ist auf "true". In diesem Fall kann ein einzelner **Prozess** Befehl kann mehrere Objekte verarbeiten, auf ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Instanz, jedoch [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] bestimmt, welche neben das einzelne Objekt im angegebenen Objekte die **Prozess** Befehl muss ebenfalls verarbeitet werden.  
  
 Allerdings können Sie mehrere Objekte, z. B. Dimensionen, gleichzeitig mit mehreren verarbeiten **Prozess** Befehle innerhalb einer **Batch** Befehl. Batchvorgänge bieten eine feinere Maß an Kontrolle für serielle oder parallele Verarbeitung von Objekten auf einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Instanz als die Verwendung der **ProcessAffectedObjects** Attribut, und ermöglichen es Ihnen so optimieren Sie Ihren verarbeitungsansatz für größere [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Datenbanken. Weitere Informationen zum Ausführen von Batchvorgängen finden Sie unter [Durchführen von Batchvorgängen &#40; XMLA &#41; ](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/performing-batch-operations-xmla.md).  
  
## <a name="specifying-out-of-line-bindings"></a>Angeben von Out-of-Line-Bindungen  
 Wenn die **Prozess** Befehl nicht enthalten ist ein **Batch** Befehl, Sie können optional angeben, Out-of-Line-Bindungen in der [Bindungen](../../analysis-services/xmla/xml-elements-properties/bindings-element-xmla.md), [DataSource](../../analysis-services/xmla/xml-elements-properties/datasource-element-xmla.md), und [DataSourceView](../../analysis-services/xmla/xml-elements-properties/datasourceview-element-xmla.md) Eigenschaften der **Prozess** Befehl für die Objekte verarbeitet werden. Out-of-Line-Bindungen sind Verweise auf Datenquellen, Datenquellensichten und andere Objekte in der Bindung vorhanden, nur während der Ausführung ist der **Prozess** Befehl und dem zugeordneten alle vorhandenen Bindungen überschreiben die Objekte, die verarbeitet werden. Wenn keine Out-of-Line-Bindungen angegeben sind, werden die Bindungen verwendet, die aktuell dem zu verarbeitenden Objekt zugeordnet sind.  
  
 Out-of-Line-Bindungen werden in den folgenden Situationen verwendet:  
  
-   Inkrementelle Verarbeitung einer Partition, bei der eine alternative Faktentabelle oder ein Filter auf der vorhandenen Faktentabelle angegeben sein muss, um sicherzustellen, dass die Zeilen nicht zweimal gezählt werden.  
  
-   Mit einem Datenflusstask in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Daten bereitstellen, bei der Verarbeitung einer Dimension, die Mining-Modell oder die Partition.  
  
 Out-of-Line-Bindungen werden als Teil der Analysis Services Scripting Language (ASSL) beschrieben. Weitere Informationen über Out-of-Line-Bindungen in ASSL finden Sie unter [&#40; Datenquellen und Bindungen SSAS – mehrdimensional &#41; ](../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
### <a name="incrementally-updating-partitions"></a>Inkrementelles Update von Partitionen  
 Das inkrementelle Update einer bereits verarbeiteten Partition erfordert in der Regel eine Out-of-Line-Bindung, da die für die Partition angegebene Bindung auf Faktentabellendaten verweist, die bereits in der Partition aggregiert wurden. Beim inkrementellen Aktualisieren von einer bereits verarbeiteten Partitions mithilfe der **Prozess** Befehl [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] führt die folgenden Aktionen aus:  
  
-   Erstellt eine temporäre Partition mit einer Struktur, die mit der Struktur der Partition identisch ist, die inkrementell aktualisiert werden soll.  
  
-   Verarbeitet die temporäre Partition über die Out-of-Line-Bindung angegeben, der **Prozess** Befehl.  
  
-   Führt die temporäre Partition mit der vorhandenen, ausgewählten Partition zusammen.  
  
 Weitere Informationen zum Zusammenführen von Partitionen mithilfe von XML for Analysis (XMLA) finden Sie unter [Zusammenführen von Partitionen &#40; XMLA &#41; ](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/merging-partitions-xmla.md).  
  
## <a name="handling-processing-errors"></a>Behandeln von Verarbeitungsfehlern  
 Die [ErrorConfiguration](../../analysis-services/xmla/xml-elements-properties/errorconfiguration-element-xmla.md) Eigenschaft von der **Prozess** Befehl können Sie angeben, wie Fehler bei der Verarbeitung eines Objekts behandelt werden sollen. Beispielsweise ermittelt [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] bei der Verarbeitung einer Dimension einen doppelten Wert in der Schlüsselspalte des Schlüsselattributs. Da Attributschlüssel eindeutig sein müssen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] verwirft die doppelten Datensätze. Auf der Grundlage der [KeyDuplicate](../../analysis-services/scripting/properties/keyduplicate-element-assl.md) Eigenschaft **ErrorConfiguration**, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] konnte:  
  
-   den Fehler ignorieren und die Verarbeitung der Dimension fortsetzen;  
  
-   eine Meldung ausgeben, die besagt, dass [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] einen doppelten Schlüssel ermittelt hat und die Verarbeitung fortgeführt wird.  
  
 Es gibt viele ähnliche Bedingungen für die **ErrorConfiguration** bietet Optionen während einer **Prozess** Befehl.  
  
## <a name="managing-writeback-tables"></a>Verwalten von Rückschreibetabellen  
 Wenn die **Prozess** Befehl gefunden wird, eine Partition mit aktiviertem Schreibzugriff oder eine Gruppe Cubes oder Measures für solche eine Partition, die noch nicht vollständig verarbeitet wird, eine Rückschreibetabelle kann für diese Partition nicht bereits vorhanden. Die [WritebackTableCreation](../../analysis-services/xmla/xml-elements-properties/writebacktablecreation-element-xmla.md) Eigenschaft von der **Prozess** Befehl wird bestimmt, ob [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] eine Rückschreibetabelle erstellen sollte.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="description"></a>Description  
 Im folgenden Beispiel wird die [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Beispieldatenbank vollständig verarbeitet.  
  
### <a name="code"></a>Code  
  
```  
<Process xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
  <Object>  
    <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
  </Object>  
  <Type>ProcessFull</Type>  
  <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
</Process>  
```  
  
### <a name="description"></a>Description  
 Im folgenden Beispiel wird inkrementell verarbeitet die **Internet_Sales_2004** -Partition in der **Internetverkäufe** -Measuregruppe des der **Adventure Works DW** Cube in der [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] Beispiel [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Datenbank. Die **Prozess** Befehl ist fügt Aggregationen für Bestelldaten Datumsangaben nach dem 31. Dezember 2006 zur Partition mit einer Out-of-Line-abfragebindung in der **Bindungen** Eigenschaft von der **Prozess**  Befehl zum Abrufen von Zeilen der Faktentabelle aus der zum Generieren von Aggregationen der Partition hinzugefügt.  
  
### <a name="code"></a>Code  
  
```  
<Process ProcessAffectedObjects="true" xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
  <Object>  
    <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
    <CubeID>Adventure Works DW</CubeID>  
    <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
    <PartitionID>Internet_Sales_2006</PartitionID>  
  </Object>  
  <Bindings>  
    <Binding>  
      <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2006</PartitionID>  
      <Source xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="QueryBinding">  
        <DataSourceID>Adventure Works DW</DataSourceID>  
        <QueryDefinition>  
          SELECT  
            [dbo].[FactInternetSales].[ProductKey],  
            [dbo].[FactInternetSales].[OrderDateKey],  
            [dbo].[FactInternetSales].[DueDateKey],  
            [dbo].[FactInternetSales].[ShipDateKey],   
            [dbo].[FactInternetSales].[CustomerKey],   
            [dbo].[FactInternetSales].[PromotionKey],  
            [dbo].[FactInternetSales].[CurrencyKey],  
            [dbo].[FactInternetSales].[SalesTerritoryKey],  
            [dbo].[FactInternetSales].[SalesOrderNumber],  
            [dbo].[FactInternetSales].[SalesOrderLineNumber],  
            [dbo].[FactInternetSales].[RevisionNumber],  
            [dbo].[FactInternetSales].[OrderQuantity],  
            [dbo].[FactInternetSales].[UnitPrice],  
            [dbo].[FactInternetSales].[ExtendedAmount],  
            [dbo].[FactInternetSales].[UnitPriceDiscountPct],  
            [dbo].[FactInternetSales].[DiscountAmount],  
            [dbo].[FactInternetSales].[ProductStandardCost],  
            [dbo].[FactInternetSales].[TotalProductCost],  
            [dbo].[FactInternetSales].[SalesAmount],  
            [dbo].[FactInternetSales].[TaxAmt],  
            [dbo].[FactInternetSales].[Freight],  
            [dbo].[FactInternetSales].[CarrierTrackingNumber],  
            [dbo].[FactInternetSales].[CustomerPONumber]  
          FROM [dbo].[FactInternetSales]  
          WHERE OrderDateKey > '1280'  
        </QueryDefinition>  
      </Source>  
    </Binding>  
  </Bindings>  
  <Type>ProcessAdd</Type>  
  <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
</Process>  
```  
  
  
