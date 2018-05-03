---
title: Zusammenführen von Partitionen (XMLA) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a1dffc9450174b44f2e1f935451622a0ef0029ad
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="merging-partitions-xmla"></a>Zusammenführen von Partitionen (XMLA)
  Wenn Partitionen denselben Aggregationsentwurf und die Struktur vorhanden sind, können Sie die Partition zusammenführen, mithilfe der [MergePartitions](../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md) -Befehl in XML for Analysis (XMLA). Das Zusammenführen von Partitionen ist ein wichtiger Vorgang, wenn Sie Partitionen verwalten, insbesondere wenn es sich hierbei um Partitionen mit Vergangenheitsdaten handelt, die nach Datum partitioniert sind.  
  
 Beispielsweise verwendet ein finanzieller Cube möglicherweise zwei Partitionen:  
  
-   Eine Partition stellt die finanziellen Daten für das aktuelle Jahr dar und verwendet relationale OLAP-(ROLAP-)Speichereinstellungen in Echtzeit für die Leistung.  
  
-   Eine andere Partition enthält finanzielle Daten für vergangene Jahre und verwendet mehrdimensionale OLAP-(MOLAP-)Speichereinstellungen für die Speicherung.  
  
 Beide Partitionen verwenden andere Speichereinstellungen, jedoch den gleichen Aggregationsentwurf. Sie können stattdessen verwenden, anstatt die Verarbeitung des Cubes zahlreicher Jahre Verlaufsdaten am Ende des Jahres an, die **MergePartitions** Befehl aus, um die Partition für das laufende Jahr in die Partition für die vergangenen Jahre zusammenzuführen. Dadurch werden die Aggregationsdaten beibehalten, ohne dass eine möglicherweise zeitaufwendige vollständige Verarbeitung des Cubes erforderlich ist.  
  
## <a name="specifying-partitions-to-merge"></a>Angeben von Partitionen für die Zusammenführung  
 Wenn die **MergePartitions** Befehl ausgeführt wurde, die Aggregationsdaten in die Quellpartitionen in angegebenen gespeicherten der [Quelle](../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md) Eigenschaft ist im angegebenen Zielpartition hinzugefügt der [Ziel ](../../analysis-services/xmla/xml-elements-properties/target-element-xmla.md) Eigenschaft.  
  
> [!NOTE]  
>  Die **Quelle** Eigenschaft kann mehrere partitionsobjektverweise enthalten. Allerdings die **Ziel** Eigenschaft kann nicht.  
  
 Damit die Zusammenführung erfolgreich, die in beiden angegebenen Partitionen der **Quelle** und **Ziel** müssen derselben Measuregruppe enthalten sein und den gleichen Aggregationsentwurf verwenden. Andernfalls tritt ein Fehler auf.  
  
 Die im angegebenen Partitionen der **Quelle** werden gelöscht, nachdem die **MergePartitions** Befehl erfolgreich ausgeführt wurde.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="description"></a>Description  
 Im folgenden Beispiel werden alle Partitionen in der **Customer Counts** Measuregruppe von der **Adventure Works** Cubes in der **Adventure Works DW** Beispiel [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Datenbank in der **Customers_2004** Partition.  
  
### <a name="code"></a>Code  
  
```  
<MergePartitions xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
  <Sources>  
    <Source>  
      <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2001</PartitionID>  
    </Source>  
    <Source>  
      <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2002</PartitionID>  
    </Source>  
    <Source>  
      <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2003</PartitionID>  
    </Source>  
  </Sources>  
  <Target>  
    <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
    <CubeID>Adventure Works DW</CubeID>  
    <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
    <PartitionID>Internet_Sales_2004</PartitionID>  
  </Target>  
</MergePartitions>  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Entwickeln mit XMLA in Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
