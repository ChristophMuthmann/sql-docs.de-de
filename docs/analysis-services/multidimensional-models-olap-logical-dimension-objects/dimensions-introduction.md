---
title: "Einführung in Dimensionen (Analysis Services – mehrdimensionale Daten) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
- dimensions [Analysis Services], about dimensions
- storage [Analysis Services], dimensions
- dimensions [Analysis Services], examples
- storing data [Analysis Services], dimensions
- storage [Analysis Services]
ms.assetid: ab170fdd-4144-42db-9497-690b9189fc25
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9320eebfc25964e5e751e2d93ffc8cb7503861e5
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="dimensions---introduction"></a>Dimensionen – Einführung
  Alle Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Dimensionen sind Gruppen von Attributen basierend auf Spalten aus Tabellen oder Sichten in einer Datenquellensicht. Dimensionen sind unabhängig von einem Cube vorhanden, können sowohl in mehreren Cubes als auch mehrfach in einem einzelnen Cube verwendet und zwischen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Instanzen verknüpft werden. Eine unabhängig von einem Cube vorhandene Dimension wird als Datenbankdimension bezeichnet und eine innerhalb eines Cubes verwendete Instanz einer Datenbankdimension als Cubedimension.  
  
## <a name="dimension-based-on-a-star-schema-design"></a>Dimension auf Basis eines Sternschemaentwurfs  
 Die Struktur einer Dimension hängt größtenteils von der Struktur der zugrunde liegenden Dimensionstabellen ab. Die einfachste Struktur ist das Sternschema, bei dem jede Dimension auf einer einzelnen Dimensionstabelle basiert, die über einen Primärschlüssel direkt mit der Faktentabelle verknüpft ist - Fremdschlüsselbeziehung.  
  
 Das folgende Diagramm zeigt einen Teil der [!INCLUDE[ssSampleDBDWobject](../../includes/sssampledbdwobject-md.md)] Beispieldatenbank, in dem die **FactResellerSales** -Faktentabelle zu zwei Dimensionstabellen, **DimReseller** und **DimPromotion**. Die **ResellerKey** Spalte in der **FactResellerSales** -Faktentabelle definiert eine fremdschlüsselbeziehung mit der **ResellerKey** Primärschlüsselspalte in der  **DimReseller** Dimensionstabelle. Auf ähnliche Weise die **PromotionKey** Spalte in der **FactResellerSales** -Faktentabelle definiert eine fremdschlüsselbeziehung mit der **PromotionKey** Primärschlüsselspalte in der  **DimPromotion** Dimensionstabelle.  
  
 ![Logisches Schema für faktendimensionsbeziehung](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/media/dimfactrelationship.gif "logisches Schema für faktendimensionsbeziehung")  
  
## <a name="dimension-based-on-a-snowflake-schema-design"></a>Dimension auf Basis eines Schneeflocken-Schemaentwurfs  
 In vielen Fällen ist eine komplexere Struktur erforderlich, da zum Definieren der Dimension Informationen aus mehreren Tabellen erforderlich sind. In dieser Struktur, die als Schneeflockenschema bezeichnet wird, basieren die einzelnen Dimensionen auf Attributen aus Spalten mehrerer Tabellen, die über Primärschlüssel-Fremdschlüssel-Beziehungen miteinander und letztendlich mit der Faktentabelle verknüpft sind. Das folgende Diagramm veranschaulicht beispielsweise die Tabellen erforderlich, um die Product-Dimension im vollständig beschreiben die **AdventureWorksDW** Beispielprojekt:  
  
 ![Tabellen für AdventureWorksAS Product-Dimension](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/media/dimproduct.gif "Tabellen für AdventureWorksAS Product-Dimension")  
  
 Um ein Produkt vollständig beschreiben zu können, müssen Kategorie und Unterkategorie des Produkts in der Product-Dimension enthalten sein. Allerdings diese Informationen befindet sich nicht direkt in der Haupttabelle für die **DimProduct** Dimension. Eine fremdschlüsselbeziehung zwischen **DimProduct** auf **DimProductSubcategory**, dem hat wiederum einer fremdschlüsselbeziehung mit der **DimProductCategory** table, vereinfacht möglich, die Informationen für Produktkategorien und Unterkategorien in der Product-Dimension enthalten.  
  
## <a name="snowflake-schema-versus-reference-relationship"></a>Schneeflockenschema im Vergleich zur Bezugsdimensionsbeziehung  
 Manchmal haben Sie die Wahl, ob Sie Attribute in einer Dimension mithilfe eines Schneeflockenschemas aus mehreren Tabellen erstellen oder ob Sie zwei separate Dimensionen definieren und eine auf dem Konzept der Bezugsdimension basierende Beziehung zwischen ihnen festlegen. Das folgende Diagramm veranschaulicht dieses Szenario.  
  
 ![Logisches Schema für referenzierte Beispieldimension](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/media/dimindirect.gif "logisches Schema für referenzierte Beispieldimension")  
  
 In der vorherigen Abbildung die **FactResellerSales** Faktentabelle verfügt nicht über eine fremdschlüsselbeziehung mit der **DimGeography** Dimensionstabelle. Allerdings die **FactResellerSales** Faktentabelle verfügt über eine fremdschlüsselbeziehung mit der **DimReseller** Dimensionstabelle, die wiederum verfügt über eine fremdschlüsselbeziehung mit der  **DimGeography** Dimensionstabelle. Um einer Reseller-Dimension zu definieren, die geografische Informationen zu jedem Wiederverkäufer enthält, müssten Sie abgerufen werden diese Attribute aus der **DimGeography** und **DimReseller** Dimensionstabellen. In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] erzielen Sie dasselbe Ergebnis, wenn Sie zwei separate Dimensionen erstellen und diese innerhalb einer Measuregruppe verknüpfen, indem Sie eine auf dem Konzept der Bezugsdimension basierende Beziehung zwischen beiden Dimensionen definieren. Weitere Informationen zu bezugsdimensionsbeziehungen, finden Sie unter [Dimensionsbeziehungen](../../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md).  
  
 Ein Vorteil der Verwendung von Bezugsdimensionsbeziehungen in diesem Szenario liegt darin, dass Sie eine einzelne Geography-Dimension und anschließend mehrere darauf basierende Cubedimensionen erstellen können, ohne zusätzlichen Speicherplatz zu benötigen. Sie können z.&nbsp;B. eine der Geography-Cubedimensionen mit einer Reseller-Dimension verknüpfen und eine andere mit einer Customer-Dimension. **Verwandte Themen:**[Dimensionsbeziehungen](../../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md), [Definieren einer referenzierten Beziehung und deren Eigenschaften auf die verwiesen wird](../../analysis-services/multidimensional-models/define-a-referenced-relationship-and-referenced-relationship-properties.md)  
  
## <a name="processing-a-dimension"></a>Verarbeiten einer Dimension  
 Wenn Sie eine Dimension erstellt haben, müssen Sie diese verarbeiten, bevor Sie die Elemente der Attribute und Hierarchien in der Dimension anzeigen können. Wenn sich die Struktur einer Dimension geändert hat oder die Informationen in den zugrunde liegenden Tabellen aktualisiert wurden, müssen Sie die Dimension erneut verarbeiten, bevor Sie die Änderungen anzeigen können. Beim Verarbeiten einer Dimension nach einer strukturellen Änderung müssen sämtliche Cubes, die die Dimension enthalten, ebenfalls verarbeitet werden. Andernfalls kann der Cube nicht angezeigt werden.  
  
## <a name="security"></a>Sicherheit  
 Alle untergeordneten Objekte einer Dimension, einschließlich Hierarchien, Ebenen und Elementen, werden mithilfe von Rollen in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] gesichert. Die Dimensionssicherheit kann für alle Cubes in der Datenbank angewendet werden, die die Dimension verwenden, oder nur für einen bestimmten Cube. Weitere Informationen zur dimensionssicherheit finden Sie unter [Erteilen von Berechtigungen für eine Dimension &#40; Analysis Services &#41; ](../../analysis-services/multidimensional-models/grant-permissions-on-a-dimension-analysis-services.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Speichern von Dimensionen](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-storage.md)   
 [Dimensionsübersetzungen](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimension-translations.md)   
 [Dimensionen mit aktiviertem Schreibzugriff](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)  
  
  

