---
title: "Datenquellen und Bindungen (SSAS – mehrdimensional) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
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
- data source views [Analysis Services], bindings
- DSO, bindings
- Analysis Services Scripting Language, data sources
- cubes [Analysis Services], bindings
- OLAP mining models [Analysis Services Scripting Language]
- bindings [Analysis Services Scripting Language]
- rebindings [Analysis Services Scripting Language]
- ASSL, bindings
- relational mining models [ASSL]
- data sources [Analysis Services Scripting Language]
- ASSL, data sources
- dimensions [Analysis Services], bindings
- measures [Analysis Services], bindings
- relational data sources [Analysis Services Scripting Language]
- Analysis Services Scripting Language, bindings
- chaptered rowsets
- granularity
- mining models [Analysis Services], data sources
- inline bindings [ASSL]
- out-of-line bindings
- measure groups [Analysis Services], bindings
- partitions [Analysis Services], bindings
ms.assetid: bc028030-dda2-4660-b818-c3160d79fd6d
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0a182451583f04bd52a4f720c4cc057226261e21
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="data-sources-and-bindings-ssas-multidimensional"></a>Datenquellen und Bindungen (SSAS – mehrdimensional)
  Cubes, Dimensionen und andere [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Objekte können an eine Datenquelle gebunden werden. Eine Datenquelle kann eines der folgenden Objekte sein:  
  
-   Eine relationale Datenquelle.  
  
-   Eine [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Pipeline, die ein Rowset (oder Kapitelrowsets) ausgibt.  
  
 Die Möglichkeiten zum Ausdrücken der Datenquelle sind vom Typ der Datenquelle abhängig. Beispielsweise wird eine relationale Datenquelle durch die Verbindungszeichenfolge gekennzeichnet. Weitere Informationen zu Datenquellen finden Sie unter [Datenquellen in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/data-sources-in-multidimensional-models.md).  
  
 Unabhängig von der verwendeten Datenquelle enthält die Datenquellensicht (DSV) die Metadaten für die Datenquelle. Daher werden die Bindungen für einen Cube oder andere [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Objekte als Bindungen zur DSV ausgedrückt. Diese Bindungen können Bindungen zu logischen Objekten einschließen, beispielsweise Sichten, berechnete Spalten und Beziehungen, die physisch in der Datenquelle nicht vorhanden sind. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fügt eine berechnete Spalte hinzu, die den Ausdruck für die DSV kapselt, und anschließend wird das entsprechende OLAP-Measure an diese Spalte in der DSV gebunden. Weitere Informationen zu DSVs finden Sie unter [Datenquellsichten in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md).  
  
 Jedes [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Objekt bindet auf eigene Weise an die Datenquelle. Außerdem kann die Datenbindung für diese Objekte und die Definition der Datenquelle mit der Definition des datengebundenen Objekts (beispielsweise der Dimension) inline oder out-of-line als separater Definitionssatz bereitgestellt werden.  
  
## <a name="analysis-services-data-types"></a>Analysis Services – Datentypen  
 Die Datentypen, die in Bindungen verwendet werden, müssen zu den von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]unterstützten Datentypen passen. Die folgenden Datentypen werden in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]definiert:  
  
|Analysis Services-Datentyp|Description|  
|---------------------------------|-----------------|  
|BigInt|Ein 64-Bit-Integer mit Vorzeichen Dieser Datentyp wird dem Int64-Datentyp in Microsoft [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] und dem DBTYPE_I8-Datentyp in der OLE DB zugeordnet.|  
|Bool|Ein boolescher Wert. Dieser Datentyp wird dem booleschen Datentyp in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] und dem DBTYPE_BOOL-Datentyp in der OLE DB zugeordnet.|  
|Währung|Ein Währungswert im Bereich von -263 (bzw. -922.337.203.685.477,5808) bis 263-1 (bzw. +922.337.203.685.477,5807) mit einer Genauigkeit von einem Zehntausendstel einer Währungseinheit. Dieser Datentyp wird dem Decimal-Datentyp in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] und dem DBTYPE_CY-Datentyp in der OLE DB zugeordnet.|  
|Datum|Datumsangaben, die als Gleitkommazahl mit doppelter Genauigkeit gespeichert sind. Der ganzzahlige Teil gibt die Anzahl von Tagen seit dem 30. Dezember 1899 wieder, während der Bruchteil ein Teil eines Tages ist. Dieser Datentyp wird dem DateTime-Datentyp in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] und dem DBTYPE_DATE-Datentyp in der OLE DB zugeordnet.|  
|Double|Eine Gleitkommazahl mit doppelter Genauigkeit im Bereich von -1,79E +308 bis 1,79E +308. Dieser Datentyp wird dem Double-Datentyp in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] und dem DBTYPE_R8-Datentyp in der OLE DB zugeordnet.|  
|Integer|Ein 32-Bit-Integer mit Vorzeichen Dieser Datentyp wird dem Int32-Datentyp in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] und dem DBTYPE_I4-Datentyp in der OLE DB zugeordnet.|  
|Single|Eine Gleitkommazahl mit einfacher Genauigkeit im Bereich von -3,40E +38 bis 3,40E +38. Dieser Datentyp wird dem Single-Datentyp in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] und dem DBTYPE_R4-Datentyp in der OLE DB zugeordnet.|  
|SmallInt|Eine 16-Bit-Ganzzahl mit Vorzeichen. Dieser Datentyp wird dem Int16-Datentyp in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] und dem DBTYPE_I2-Datentyp in der OLE DB zugeordnet.|  
|TinyInt|Eine 8-Bit-Ganzzahl mit Vorzeichen. Dieser Datentyp wird dem SByte-Datentyp in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] und dem DBTYPE_I1-Datentyp in OLE DB zugeordnet.<br /><br /> Hinweis: Wenn eine Datenquelle Felder enthält, die dem tinyint-Datentyp entsprechen und die Eigenschaft Automatisch inkrementieren auf TRUE festgelegt ist, werden sie in der Datenquellensicht zu ganzen Zahlen konvertiert.|  
|UnsignedBigInt|Eine 64-Bit-Ganzzahl ohne Vorzeichen. Dieser Datentyp wird dem Uint64-Datentyp in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] und dem DBTYPE_UI8-Datentyp in der OLE DB zugeordnet.|  
|UnsignedInt|Eine 32-Bit-Ganzzahl ohne Vorzeichen. Dieser Datentyp wird dem Uint32-Datentyp in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] und dem DBTYPE_UI4-Datentyp in der OLE DB zugeordnet.|  
|UnsignedSmallInt|Eine 16-Bit-Ganzzahl ohne Vorzeichen. Dieser Datentyp wird dem Uint16-Datentyp in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] und dem DBTYPE_UI2-Datentyp in der OLE DB zugeordnet.|  
|WChar|Ein mit NULL endender Datenstrom von Unicode-Zeichen. Dieser Datentyp wird dem String-Datentyp in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] und dem DBTYPE_WSTR-Datentyp in der OLE DB zugeordnet.|  
  
 Alle von der Datenquelle empfangenen Daten werden in den [!INCLUDE[ssAS](../../includes/ssas-md.md)] -Typ konvertiert, der in der Bindung (normalerweise während der Verarbeitung) angegeben wird. Ein Fehler wird ausgelöst, wenn die Konvertierung (z. B. von String in Int) nicht ausgeführt werden kann. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] legt den Datentyp in der Bindung normalerweise auf den Typ fest, der am ehesten dem Quelltyp in der Datenquelle entspricht. Beispielsweise werden die SQL-Typen Date, DateTime, SmallDateTime, DateTime2, DateTimeOffset [!INCLUDE[ssAS](../../includes/ssas-md.md)] Date zugewiesen und der SQL-Typ Time wird String zugeordnet.  
  
## <a name="bindings-for-dimensions"></a>Bindungen für Dimensionen  
 Jedes Attribut einer Dimension wird an eine Spalte in der DSV gebunden. Alle Attribute einer Dimension müssen aus einer einzigen Datenquelle kommen. Die Attribute können jedoch an Spalten in unterschiedlichen Tabellen gebunden werden. Die Beziehungen zwischen den Tabellen werden in der DSV definiert. Wenn in einer Tabelle mehrere Beziehungssätze vorhanden sind, kann es erforderlich sein, in der DSV eine benannte Abfrage einzufügen, die als Aliastabelle fungiert. Ausdrücke und Filter werden in der DSV mithilfe von benannten Berechnungen und benannten Abfragen definiert.  
  
## <a name="bindings-for-measuregroups-measures-and-partitions"></a>Bindungen für Measuregruppen, Measures und Partitionen  
 Jede Measuregruppe besitzt die folgenden Standardbindungen:  
  
-   Die Measuregruppe wird an eine Tabelle in einer DSV gebunden (z. B. **MeasureGroup.Source**).  
  
-   Jede Measuregruppe wird an eine Spalte in dieser Tabelle gebunden (z. B. **Measure.ValueColumn.Source**).  
  
-   Jede Measuregruppendimension besitzt einen Satz von *Granularitätsattributen* , die die Granularität der Measuregruppe definiert. Jedes dieser Attribute muss an die Spalte oder die Spalten in der Faktentabelle gebunden werden, die den Attributschlüssel enthalten. (Weitere Informationen über Granularitätsattribute finden Sie unter "Measuregruppen-Granularitätsattribute", weiter unten in diesem Thema.)  
  
 Diese Standardbindungen können partitionsweise selektiv überschrieben werden. Jede Partition kann eine andere Datenquelle, eine andere Tabelle, einen anderen Abfragenamen oder einen anderen Filterausdruck angeben. Das üblichste Partitionskonzept ist, die Tabelle partitionsweise mithilfe der gleichen Datenquelle zu überschreiben. Alternativ kann beispielsweise auch für jede Partition ein anderer Filter verwendet oder die Datenquelle geändert werden.  
  
 Die Standarddatenquelle muss in der DSV definiert werden, dabei werden die Schemainformationen einschließlich der Details der Beziehungen angegeben. Alle zusätzlich auf Partitionsebene angegebenen Tabellen oder Abfragen müssen nicht in der DSV aufgeführt werden, sie müssen jedoch das gleiche Schema besitzen wie die für die Measuregruppe definierte Tabelle. Zumindest müssen sie alle Spalten enthalten, die von Measures oder Granularitätsattributen verwendet werden. Die einzelnen Bindungen pro Measure und Granularitätsattribut können nicht auf Partitionsebene überschrieben werden, und es wird angenommen, dass diese Bindungen zu den gleichen Spalten bestehen, die auch für die Measuregruppe definiert sind. Wenn daher die Partition eine Datenquelle verwendet, die tatsächlich ein anderes Schema besitzt, muss die für die Partition definierte **TableDefinition** -Abfrage das gleiche Schema ergeben wie das von der Measuregruppe verwendete Schema.  
  
### <a name="measuregroup-granularity-attributes"></a>Measuregruppen-Granularitätsattribute  
 Wenn die Granularität einer Measuregruppe mit der bekannten Granularität in der Datenbank übereinstimmt und eine direkte Beziehung von der Faktentabelle zu der Dimensionstabelle besteht, muss nur das Granularitätsattribut an die entsprechende Fremdschlüsselspalte, bzw. die Spalten, in der Faktentabelle gebunden werden. Betrachten Sie z. B. die folgenden Fakten- und Dimensionstabellen:  
  
 `Sales(RequestedDate, OrderedProductID, ReplacementProductID, Qty)`  
  
 `Product(ProductID, ProductName,Category)`  
  
 ``  
  
 `Relation: Sales.OrderedProductID -> Product.ProductID`  
  
 `Relation: Sales.ReplacementProductID -> Product.ProductID`  
  
 ``  
  
 Wenn Sie eine Analyse nach bestellten Produkten ausführen, wäre das Produktgranularitätsattribut für "Bestelltes Produkt" in der Dimensionsrolle "Verkauf" an Sales.OrderedProductID gebunden.  
  
 Es kann aber auch vorkommen, dass die **GranularityAttributes** nicht als Spalten in der Faktentabelle vorhanden sind. Beispielsweise könnten die **GranularityAttributes** unter den folgenden Umständen nicht als Spalten vorhanden sein:  
  
-   Die OLAP-Granularität ist gröber als die Granularität in der Quelle.  
  
-   Eine Zwischentabelle vermittelt zwischen der Faktentabelle und der Dimensionstabelle.  
  
-   Der Dimensionsschlüssel ist nicht der gleiche wie der Primärschlüssel in der Dimensionstabelle.  
  
 In allen diesen Fällen muss die DSV so definiert werden, dass die Granularitätsattribute in der Faktentabelle vorhanden sind. Beispielsweise kann eine benannte Abfrage oder berechnete Spalte eingeführt werden.  
  
 Wenn die Granularität in der gleichen Beispieltabelle wie oben auf "Kategorie" bezogen würde, könnte eine Sicht der "Verkauf" eingefügt werden.  
  
 `SalesWithCategory(RequestedDate, OrderedProductID, ReplacementProductID, Qty, OrderedProductCategory)`  
  
 `SELECT Sales.*, Product.Category AS OrderedProductCategory`  
  
 `FROM Sales INNER JOIN Product`  
  
 `ON Sales.OrderedProductID = Product.ProductID`  
  
 ``  
  
 In diesem Fall wird die GranularityAttribute-Kategorie an SalesWithCategory.OrderedProductCategory gebunden.  
  
### <a name="migrating-from-decision-support-objects"></a>Migrieren von Decision Support Objects  
 Decision Support Objects (DSO) 8.0 ermöglicht die erneute Bindung von **PartitionMeasures** . Deshalb ist die Migrationsstrategie in diesen Fällen, die entsprechende Abfrage zu erstellen.  
  
 Außerdem ist es nicht möglich, die Dimensionsattribute innerhalb einer Partition neu zu binden, auch wenn DSO 8.0 diese erneute Bindung ermöglicht. Daher ist die Migrationsstrategie in diesen Fällen, die erforderlichen benannten Abfragen in der DSV zu definieren, sodass in der DSV für die Partition die gleichen Tabellen und Spalten vorhanden sind wie diejenigen, die für die Dimension verwendet werden. In diesen Fällen muss möglicherweise die einfache Migration verwendet werden, in der die From/Join/Filter-Klausel einer einzigen benannten Abfrage zugeordnet wird, anstatt einem strukturierten Satz verknüpfter Tabellen. Da es DSO 8.0 ermöglicht, Partitionsdimensionen erneut zu binden, selbst wenn die Partition die gleiche Datenquelle verwendet, sind bei der Migration möglicherweise auch mehrere DSVs für die gleiche Datenquelle erforderlich.  
  
 In DSO 8.0 können die entsprechenden Bindungen auf zwei unterschiedliche Arten ausgedrückt werden, je nachdem, ob optimierte Schemas verwendet werden oder nicht, indem entweder eine Bindung an den Primärschlüssel in der Dimensionstabelle erfolgt oder an den Fremdschlüssel der Faktentabelle. In ASSL werden die beiden unterschiedlichen Arten nicht unterschieden.  
  
 Das gleiche Bindungsprinzip gilt auch für Partitionen, die eine Datenquelle verwenden, die die Dimensionstabellen nicht enthalten, da die Bindung an die Fremdschlüsselspalte in der Faktentabelle erfolgt, nicht an die Primärschlüsselspalte in der Dimensionstabelle.  
  
## <a name="bindings-for-mining-models"></a>Bindungen für Miningmodelle  
 Ein Miningmodell ist entweder relational oder OLAP. Die Datenbindungen für ein relationales Miningmodell unterscheiden sich grundsätzlich von den Bindungen für ein OLAP-Miningmodell.  
  
### <a name="bindings-for-a-relational-mining-model"></a>Bindungen für ein relationales Miningmodell  
 Ein relationales Miningmodell verwendet die in der DSV definierten Beziehungen, um alle Mehrdeutigkeiten in Bezug auf die Bindung von bestimmten Spalten zu bestimmten Datenquellen aufzulösen. In einem relationalen Miningmodell folgen die Datenbindungen diesen Regeln:  
  
-   Jede nicht verschachtelte Tabellenspalte ist entweder an eine Spalte in der Falltabelle oder an eine mit der Falltabelle verknüpfte Tabelle gebunden (entweder als n:1-Beziehung oder als 1:1 Beziehung). Die Beziehungen zwischen den Tabellen werden in der DSV definiert.  
  
-   Jede verschachtelte Tabellenspalte wird an eine Quelltabelle gebunden. Die Spalten der verschachtelten Tabellenspalte werden anschließend an Spalten in dieser Quelltabelle gebunden oder an eine mit dieser Quelltabelle verknüpfte Tabelle. (Wieder folgt die Bindung einer n:1 oder 1:1 Beziehung.) Die Miningmodellbindungen stellen nicht den Joinpfad zur verschachtelten Tabelle bereit. Diese werden stattdessen von den in der DSV definierten Beziehungen bereitgestellt.  
  
### <a name="bindings-for-an-olap-mining-model"></a>Bindungen für ein OLAP-Miningmodell  
 OLAP-Miningmodelle besitzen kein Äquivalent zu einer DSV. Deshalb müssen die Datenbindungen die Eindeutigkeiten zwischen Spalten und Datenquellen bereitstellen. Ein Miningmodell kann beispielsweise auf dem Cube "Verkauf" basieren, und Spalten können auf "Menge", "Betrag" und "Produktname" basieren. Alternativ kann ein Miningmodell auf dem Cube "Produkt" basieren, und Spalten können auf "Produktname", "Produktfarbe" und einer mit "Verkaufsmenge" verschachtelten Tabelle basieren.  
  
 In einem OLAP-Miningmodell folgen die Datenbindungen diesen Regeln:  
  
-   Jede nicht verschachtelte Tabelle ist an ein Measure in einem Cube gebunden, an ein Attribut in einer Dimension dieses Cubes (das die **CubeDimension** angibt, um im Fall von Dimensionsrollen Eindeutigkeit herzustellen) oder an ein Attribut in einer Dimension.  
  
-   Jede verschachtelte Tabellenspalte wird an eine **CubeDimension**gebunden. Das bedeutet, es wird definiert, wie die Navigation von einer Dimension zu einem verknüpften Cube erfolgt oder (in dem seltenen Fall von geschachtelten Tabellen) von einem Cube zu einer seiner Dimensionen.  
  
## <a name="out-of-line-bindings"></a>Out-of-Line-Bindungen  
 Mithilfe von Out-of-Line-Bindungen können vorhandene Datenbindungen während der Dauer einer Befehlsausführung vorübergehend geändert werden. Out-of-Line-Bindungen bezeichnen Bindungen, die in einen Befehl eingeschlossen werden und nicht dauerhaft sind. Out-of-Line-Bindungen sind nur vorhanden, während dieser spezielle Befehl ausgeführt wird. Im Unterschied dazu sind Inline-Bindungen in der ASSL-Objektdefinition enthalten und bleiben mit der Objektdefinition innerhalb der Servermetadaten erhalten.  
  
 ASSL ermöglicht die Festlegung von Out-of-Line-Bindungen entweder in einem **Process** -Befehl, wenn dieser nicht in einem Batch enthalten ist, oder in einem **Batch** -Befehl. Wenn Out-of-Line Bindungen in einem **Batch** -Befehl festgelegt werden, erstellen alle in dem **Batch** -Befehl festgelegten Bindungen einen neuen Bindungskontext, in dem alle **Process** -Befehle des Batchs ausgeführt werden. Dieser neue Bindungskontext schließt Objekte ein, die aufgrund des **Process** -Befehls indirekt verarbeitet werden.  
  
 Wenn in einem Befehl Out-of-Line-Bindungen festgelegt werden, überschreiben diese die Inline-Bindungen im permanenten DDL-Code für die angegebenen Objekte. Diese verarbeiteten Objekte können das Objekt entweder direkt benannt im **Process** -Befehl enthalten, oder sie können andere Objekte enthalten, deren Verarbeitung automatisch als Teil der Verarbeitung initiiert wird.  
  
 Out-of-Line-Bindungen werden durch Einfügung des optionalen **Bindings** -Auflistungsobjekts mit dem Verarbeitungsbefehl festgelegt. Die optionale **Bindings** -Auflistung enthält die folgenden Elemente.  
  
|Eigenschaft|Kardinalität|Typ|Description|  
|--------------|-----------------|----------|-----------------|  
|**Bindung**|0-n|**Bindung**|Stellt eine Auflistung neuer Bindungen bereit.|  
|**DataSource**|0-1|**DataSource**|Ersetzt **DataSource** vom Server, der verwendet worden wäre.|  
|**DataSourceView**|0-1|**DataSourceView**|Ersetzt die **DataSourceView** vom<br /><br /> Server, der verwendet worden wäre.|  
  
 Alle Elemente, die sich auf Out-of-Line-Bindungen beziehen, sind optional. Für alle nicht angegebenen Elemente verwendet ASSL die im DDL-Code des permanenten Objekts enthaltene Festlegung. Die Angabe von **DataSource** oder **DataSourceView** im **Prozess** -Befehl ist optional. Wenn **DataSource** oder **DataSourceView** angegeben wird, werden diese nicht instanziiert und bleiben nicht erhalten, nachdem der **Process** -Befehl ausgeführt wurde.  
  
### <a name="definition-of-the-out-of-line-binding-type"></a>Definition des Out-of-Line-Bindungstyps  
 Innerhalb der Out-of-Line- **Bindings** -Auflistung ermöglicht ASSL eine Auflistung von Bindungen für mehrere Objekte, von denen jedes eine **Bindung**ist. Jede **Bindung** besitzt einen erweiterten Objektverweis, der dem Objektverweis entspricht, der jedoch auch auf untergeordnete Objekte verweisen kann (beispielsweise Dimensionsattribute und Measuregruppenattribute). Dieses Objekt übernimmt die flatform normalerweise von der **Objekt** Element im **Prozess** Befehlen, mit dem Unterschied, die die \< *Objekt* > \< */Object*>-Tags nicht vorhanden sind.  
  
 Jedes Objekt, das für die die Bindung wird angegeben, wird durch ein XML-Element des Formulars identifiziert \< *Objekt*> ID (z. B. **DimensionID**). Nachdem Sie, das Objekt identifiziert haben so genau wie möglich mit dem Formular \< *Objekt*>-ID, wird das Element für die Bindung angegeben wird, die in der Regel ist **Quelle**. Häufig ist die **Source** eine Eigenschaft für das **DataItem**. Dies ist der Fall bei Spaltenbindungen in einem Attribut. In diesem Fall geben Sie nicht das **DataItem** -Tag an, sondern lediglich die **Source** -Eigenschaft, als befände sich diese direkt in der zu bindenden Spalte.  
  
 **KeyColumns** werden durch ihre Sortierung innerhalb der **KeyColumns** -Auflistung identifiziert. Es ist nicht möglich, beispielsweise nur die erste und die dritte Spalte eines Attributs anzugeben, da keine Möglichkeit besteht, festzulegen, dass die zweite Schlüsselspalte übersprungen werden soll. Alle Schlüsselspalten müssen in der Out-of-Line-Bindung für ein Dimensionsattribut vorhanden sein.  
  
 **Übersetzungen**werden, obwohl sie keine ID haben, semantisch anhand ihrer Sprache identifiziert. Daher muss bei **Übersetzungen** innerhalb einer **Bindung** der Sprachbezeichner hinzugefügt werden.  
  
 Ein weiteres innerhalb einer **Bindung** zulässiges Element, das nicht direkt im DDL-Code vorhanden ist, ist **ParentColumnID**, das in geschachtelten Tabellen für Data Mining verwendet wird. In diesem Fall ist es erforderlich, die übergeordnete Spalte in der verschachtelten Tabelle anzugeben, für die die Bindung bereitgestellt wird.  
  
  
