---
title: Attribute und Attributhierarchien | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: olap
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 009b5857470b106cb5c68301537dceb438ec4406
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="attributes-and-attribute-hierarchies"></a>Attribute und Attributhierarchien
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Dimensionen sind Auflistungen von Attributen, die an eine oder mehrere Spalten in einer Tabelle oder Sicht in der Datenquellensicht gebunden sind.  
  
## <a name="key-attribute"></a>Schlüsselattribut  
 Jede Dimension enthält ein Schlüsselattribut. Jedes Attribut ist an mindestens eine Spalte in einer Dimensionstabelle gebunden. Das Schlüsselattribut ist das Attribut in einer Dimension, das die Spalten in der Dimensionshaupttabelle identifiziert, die in Fremdschlüsselbeziehungen zur Faktentabelle verwendet werden. Das Schlüsselattribut entspricht normalerweise den Primärschlüsselspalten in der Dimensionstabelle. Sie können einen logischen Primärschlüssel für eine Tabelle in einer Datenquellensicht definieren, die über keinen physischen Primärschlüssel in der zugrunde liegenden Datenquelle verfügt. **Weitere Informationen**, finden Sie unter [definieren logischer Primärschlüssel in einer Datenquellensicht &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/define-logical-primary-keys-in-a-data-source-view-analysis-services.md). Beim Definieren von Schlüsselattributen versuchen der Cube-Assistent und der Dimensions-Assistent, die Primärschlüsselspalten der Dimensionstabelle in der Datenquellensicht zu verwenden. Wurde für die Dimensionstabelle weder ein logischer noch ein physischer Primärschlüssel definiert, sind die Assistenten möglicherweise nicht in der Lage, die Schlüsselattribute für die Dimension richtig zu definieren.  
  
## <a name="binding-an-attribute-to-columns-in-data-source-view-tables-or-views"></a>Binden eines Attributs an Spalten in Tabellen oder Sichten einer Datenquellensicht  
 Ein Attribut ist an Spalten in mindestens einer Tabelle oder Sicht einer Datenquellensicht gebunden. Ein Attribut ist immer an mindestens eine Schlüsselspalte gebunden, wodurch die in dem Attribut enthaltenen Elemente bestimmt werden. Standardmäßig ist dies die einzige Spalte, an die ein Attribut gebunden ist. Ein Attribut kann für bestimmte Zwecke auch an eine oder mehrere zusätzliche Spalten gebunden werden. Angenommen, ein Attribut des **NameColumn** Eigenschaft bestimmt den Namen, die dem Benutzer für die einzelnen Attributelemente angezeigt wird - diese Eigenschaft des Attributs an eine bestimmte Dimensionsspalte über einer Datenquellensicht gebunden werden kann oder sein kann Um eine berechnete Spalte in der Datenquellensicht gebunden. Weitere Informationen finden Sie unter [Dimensionsattributeigenschaftenverweis](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md).  
  
## <a name="attribute-hierarchies"></a>Attributhierarchien  
 Standardmäßig sind die Elemente eines Attributs in zwei Ebenenhierarchien gruppiert, eine Blattebene und eine Alle-Ebene. Die Alle-Ebene enthält den aggregierten Wert der Attributelemente in den Measures jeder Measuregruppe, der die Dimension, mit der das Attribut verknüpft ist, als Element angehört. Jedoch, wenn die **IsAggregatable** Eigenschaft auf "false" festgelegt ist, die alle-Ebene wird nicht erstellt. Weitere Informationen finden Sie unter [Dimensionsattributeigenschaftenverweis](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md).  
  
 Attribute werden normalerweise in benutzerdefinierten Hierarchien angeordnet, die Drilldownpfade bereitstellen, über die Benutzer die Daten in den Measuregruppen durchsuchen können, mit denen das Attribut verknüpft ist. In Clientanwendungen können Attribute zur Bereitstellung von Gruppierungs- und Einschränkungsinformationen verwendet werden. Wenn Attribute in benutzerdefinierten Hierarchien angeordnet sind, definieren Sie Beziehungen zwischen Hierarchieebenen, wenn Ebenen in einer n: 1-verknüpft sind oder eine 1: 1-Beziehung (bezeichnet eine *natürlichen* Beziehung). So sollte z. B. in einer Calendar Time-Hierarchie eine Day-Ebene mit der Month-Ebene, die Month-Ebene mit der Quarter-Ebene usw. verknüpft sein. Durch das Definieren von Beziehungen zwischen Ebenen in einer benutzerdefinierten Hierarchie ist es Analysis Services möglich, zweckmäßigere Aggregationen zu definieren, um die Abfrageleistung zu erhöhen. Es kann darüber hinaus dazu beitragen, bei der Verarbeitung Arbeitsspeicher zu sparen, was bei größeren oder komplexeren Cubes wichtig sein kann. Weitere Informationen finden Sie unter [Benutzerhierarchien](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md), [Situationen Hierarchien](../../analysis-services/multidimensional-models/user-defined-hierarchies-create.md), und [definieren Attributbeziehungen](../../analysis-services/multidimensional-models/attribute-relationships-define.md).  
  
## <a name="attribute-relationships-star-schemas-and-snowflake-schemas"></a>Attributbeziehungen, Sternschemas und Schneeflockenschemas  
 Standardmäßig werden in einem Sternschema alle Attribute direkt mit dem Schlüsselattribut verknüpft. Hierdurch können Benutzer die Fakten im Cube auf Basis einer beliebigen Attributhierarchie in der Dimension durchsuchen. In einem Schneeflockenschema ist ein Attribut entweder direkt mit dem Schlüsselattribut verknüpft, falls die zugrunde liegende Tabelle direkt mit der Faktentabelle verknüpft ist, oder es ist indirekt verknüpft, und zwar durch das Attribut, das an den Schlüssel in der zugrunde liegenden Tabelle gebunden ist, die wiederum die per Schneeflockenschema verknüpfte Tabelle mit der direkt verknüpften Tabelle verbindet.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen von benutzerdefinierten Hierarchien](../../analysis-services/multidimensional-models/user-defined-hierarchies-create.md)   
 [Definieren von Attributbeziehungen](../../analysis-services/multidimensional-models/attribute-relationships-define.md)   
 [Dimensionsattributeigenschaftenverweis](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
