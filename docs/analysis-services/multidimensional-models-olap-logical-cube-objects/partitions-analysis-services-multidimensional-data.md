---
title: "Partitionen (Analysis Services – mehrdimensionale Daten) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- storage [Analysis Services], partitions
- incremental updates [Analysis Services]
- data sources [Analysis Services], partitions
- data storage [Analysis Services]
- aggregations [Analysis Services], partitions
- OLAP objects [Analysis Services], partitions
- storing data [Analysis Services], partitions
- partitions [Analysis Services], about partitions
- cubes [Analysis Services], partitions
- partitions [Analysis Services]
- remote partitions [Analysis Services]
- measure groups [Analysis Services], partitions
ms.assetid: cd10ad00-468c-4d49-9f8d-873494d04b4f
caps.latest.revision: "43"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: eeeec758905021bfb1b352fb325810f096e3292d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="partitions-analysis-services---multidimensional-data"></a>Partitionen (Analysis Services – Mehrdimensionale Daten)
  Eine Partition ist ein Container für einen Teil der Measuregruppendaten. Partitionen sind in einer MDX-Abfrage nicht sichtbar, da alle Abfragen den gesamten Inhalt der Measuregruppe wiedergeben, unabhängig davon, wie viele Partitionen für die Measuregruppe defniert wurden. Der Dateninhalt einer Partition wird durch die Abfragebindungen der Partition und die Slicingausdrücke definiert.  
  
 Ein einfaches <xref:Microsoft.AnalysisServices.Partition>-Objekt besteht aus grundlegenden Informationenen, der Slicingdefinition, dem Aggregationsentwurf usw. Grundlegende Informationen beinhalten den Namen der Partition, den Speichermodus, den Verarbeitungsmodus usw. Die Slicingdefinition ist ein MDX-Ausdruck, der ein Tupel oder einen Satz angibt. Die Slicingdefinition besitzt die gleichen Einschränkungen wie die StrToSet MDX-Funktion. Zusammen mit dem CONSTRAINED-Parameter kann die Slicingdefinition Dimensionen, Hierarchien, Ebenen- und Elementnamen, Schlüssel, eindeutige Namen oder andere benannte Objekte in dem Cube verwenden, jedoch keine MDX-Funktionen. Der Aggregationsentwurf ist eine Auflistung von Aggregationsdefinitionen, die für mehrere Partitionen freigegeben sein können. Der Standard wird vom Aggregationsentwurf des übergeordneten Cubes übernommen.  
  
 Partitionen werden verwendet, indem [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] zum Verwalten und Speichern von Daten und Aggregationen für eine Measuregruppe in einem Cube. Jede Measuregruppe verfügt über mindestens eine Partition, die beim Definieren der Measuregruppe erstellt wird. Wenn Sie eine neue Partition für eine Measuregruppe erstellen, wird die neue Partition der Menge von Partitionen hinzugefügt, die bereits für die Measuregruppe vorhanden sind. Die Measuregruppe spiegelt die kombinierten Daten aller ihrer Partitionen wider. Das bedeutet, dass Sie sicherstellen müssen, dass die Daten für eine Partition einer Measuregruppe von den Daten aller anderen Partitionen der Measuregruppe ausgeschlossen sind, um sicherzustellen, dass Daten in der Measuregruppe nur einmal wiedergegeben werden. Die Originalpartition für eine Measuregruppe basiert auf einer einzelnen Faktentabelle in der Datenquellensicht des Cubes. Sind mehrere Partitionen für eine Measuregruppe vorhanden, kann jede Partition auf eine andere Tabelle entweder in der Datenquellensicht oder in der zugrunde liegenden relationalen Datenquelle für den Cube verweisen. Mehrere Partitionen in einer Measuregruppe können auf die gleiche Tabelle verweisen, wenn jede Partition auf unterschiedliche Zeilen in der Tabelle beschränkt wird.  
  
 Partitionen stellen einen leistungsstarken und flexiblen Mechanismus zum Verwalten von Cubes (insbesondere von sehr großen Cubes) dar. Ein Cube, der z.&#160;B. Umsatzinformationen enthält, kann Partitionen für die Daten aus jedem der vergangenen Jahre sowie Partitionen für jedes Quartal des aktuellen Jahres enthalten. Dabei muss nur die Partition für das aktuelle Quartal verarbeitet werden, wenn dem Cube aktuelle Informationen hinzugefügt werden. Durch die Verarbeitung einer kleineren Datenmenge wird die Verarbeitungsleistung verbessert, indem die Verarbeitungszeit verkürzt wird. Am Ende des Jahres können die Partitionen für die vier Quartale in einer einzelnen Partition für das Jahr zusammengeführt und eine neue Partition für das erste Quartal des neuen Jahres erstellt werden. Darüber hinaus kann der Prozess der Erstellung dieser neuen Partition als Teil der Data Warehouse-Ladevorgänge und Cubeverarbeitungsprozeduren automatisiert werden.  
  
 Partitionen sind für Anwender des Cubes im geschäftlichen Bereich nicht sichtbar. Partitionen können jedoch von Administratoren konfiguriert, hinzugefügt oder gelöscht werden. Jede Partition wird in einer getrennten Gruppe von Dateien gespeichert. Die Aggregatdaten jeder Partition können auf der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Instanz, auf der die Partition definiert ist, auf einer anderen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Instanz oder in derselben Datenquelle gespeichert werden, die zum Bereitstellen der Quelldaten der Partition verwendet wird. Partitionen ermöglichen es, die Quelldaten und die Aggregatdaten eines Cubes auf mehrere Festplatten und zwischen mehreren Servercomputern zu verteilen. Bei einem mittelgroßen bis großen Cube kann die Abfrageleistung, die Ladeleistung und Verwaltungsfähigkeit des Cubes durch Partitionen deutlich steigen.  
  
 Der Speichermodus der einzelnen Partitionen kann unabhängig von anderen Partitionen in der Measuregruppe konfiguriert werden. Für die Speicherung von Partitionen können beliebige Kombinationen von Optionen für Quelldatenspeicherort, Speichermodus, proaktives Zwischenspeichern und Aggregationsentwurf verwendet werden. Mithilfe der Optionen für Echtzeit-OLAP und proaktives Zwischenspeichern können Sie beim Entwerfen einer Partition die Abfragegeschwindigkeit gegen die Latenzzeit abwägen. Speicheroptionen können auch auf verwandte Dimensionen und auf Fakten in einer Measuregruppe angewendet werden. Aufgrund dieser Vielfalt an Möglichkeiten können Sie Strategien für die Speicherung von Cubes entwerfen, die Ihren Anforderungen gerecht werden. Weitere Informationen finden Sie unter [Partition Speichermodi und Verarbeitung](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md), [Aggregationen und Aggregationsentwürfe](../../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md) und [proaktives Zwischenspeichern &#40; Partitionen &#41; ](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).  
  
## <a name="partition-structure"></a>Partitionsstruktur  
 Die Struktur einer Partition muss mit der Struktur der zugehörigen Measuregruppe übereinstimmen. Das bedeutet, dass auch die Measures, die die Measuregruppe definieren, zusammen mit allen verwandten Dimensionen in der Partition definiert sein müssen. Beim Erstellen einer Partition erbt diese somit dieselben Measures und verwandten Dimensionen, die für die Measuregruppe definiert wurden.  
  
 Die einzelnen Partitionen in einer Measuregruppe können jedoch über verschiedene Faktentabellen verfügen, die aus verschiedenen Datenquellen stammen können. Verfügen die verschiedenen Partitionen einer Measuregruppe über unterschiedliche Faktentabellen, müssen die Tabellen ausreichende Übereinstimmungen aufweisen, um die Struktur der Measuregruppe aufrechtzuerhalten. Das bedeutet, dass die Verarbeitungsabfrage für alle Faktentabellen aller Partitionen dieselben Spalten und dieselben Datentypen zurückgibt.  
  
 Stammen die Faktentabellen verschiedener Partitionen aus unterschiedlichen Datenquellen, müssen auch die Quelltabellen für sämtliche verwandten Dimensionen und sämtliche Zwischenfaktentabellen in allen Datenquellen vorhanden sein und in allen Datenbanken dieselbe Struktur aufweisen. Des Weiteren müssen alle Spalten in Dimensionstabellen, die zum Definieren von Attributen für Cubedimensionen im Zusammenhang mit der Measuregruppe verwendet werden, in allen Datenquellen vorhanden sein. Es ist nicht notwendig, alle Joins zwischen der Quelltabelle einer Partition und einer Tabelle mit verwandten Dimensionen zu definieren, wenn die Partitionsquelltabelle die gleiche Struktur wie die Quelltabelle für die Measuregruppe aufweist.  
  
 Spalten, die nicht zum Definieren von Measures in der Measuregruppe verwendet werden, können in einigen Faktentabellen vorhanden sein, in anderen hingegen fehlen. Ebenso können Spalten, die nicht zum Definieren von Attributen in Tabellen mit verwandten Dimensionen verwendet werden, in einigen Datenbanken vorhanden sein, in anderen hingegen fehlen. Tabellen, die weder für Faktentabellen noch für Tabellen mit verwandten Dimensionen verwendet werden, können in einigen Datenbanken vorhanden sein, in anderen hingegen fehlen.  
  
## <a name="data-sources-and-partition-storage"></a>Datenquellen und Partitionsspeicherung  
 Eine Partition basiert entweder auf einer Tabelle oder auf einer Sicht in einer Datenquelle oder auf einer Tabelle bzw. benannten Abfrage in einer Datenquellensicht. Der Speicherort der Partitionsdaten wird durch die Datenquellenbindung definiert. In der Regel kann eine Measuregruppe horizontal oder vertikal partitioniert werden.  
  
-   In einer horizontal partitionierten Measuregruppe basiert jede Partition auf einer gesonderten Tabelle. Diese Art der Partitionierung ist dann geeignet, wenn Daten auf mehrere Tabellen verteilt werden. So weisen beispielsweise einige relationale Datenbanken gesonderte Tabellen für die Daten der verschiedenen Monate auf.  
  
-   In einer vertikal partitionierten Measuregruppe basiert die Measuregruppe auf einer einzelnen Tabelle, und jede Partition basiert auf einer Abfrage des Quellsystems, die die Daten für die Partition filtert. Enthält z. B. eine einzelne Tabelle die Daten mehrerer Monate, kann die Measuregruppe dennoch nach Monaten partitioniert werden, indem die Transact-SQL-Klausel WHERE angewendet wird, die die Daten eines separaten Monats für jede Partition zurückgibt.  
  
 Jede Partition verfügt über Speichereinstellungen, die bestimmen, ob die Daten und Aggregationen der Partition in der lokalen Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oder in einer Remotepartition auf einer anderen Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] gespeichert werden. Über die Speichereinstellungen können auch der Speichermodus und das proaktive Zwischenspeichern zur Steuerung der Latenzzeit für eine Partition angegeben werden. Weitere Informationen finden Sie unter [Partition Speichermodi und Verarbeitung](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md), [proaktives Zwischenspeichern &#40; Partitionen &#41; ](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md), und [Remotepartitionen](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-remote-partitions.md).  
  
## <a name="incremental-updates"></a>Inkrementelle Updates  
 Wenn Sie in Measuregruppen mit mehreren Partitionen Partitionen erstellen und verwalten, müssen Sie besondere Vorsichtsmaßnahmen ergreifen, um die Richtigkeit der Cubedaten sicherzustellen. Obwohl diese Vorsichtsmaßnahmen normalerweise Measuregruppen mit nur einer Partition nicht betreffen, werden sie jedoch angewendet, wenn Sie ein inkrementelles Update der Partitionen durchführen. Beim inkrementellen Update einer Partition wird eine neue temporäre Partition mit einer Struktur erstellt, die mit der der Quellpartition übereinstimmt. Die temporäre Partition wird verarbeitet und dann mit der Quellpartition zusammengeführt. Daher müssen Sie sicherstellen, dass die Verarbeitungsabfrage, die die temporäre Partition auffüllt, keine bereits vorhandenen Daten einer bestehenden Partition dupliziert.  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurieren von Measureeigenschaften](../../analysis-services/multidimensional-models/configure-measure-properties.md)   
 [Cubes in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/cubes-in-multidimensional-models.md)  
  
  
