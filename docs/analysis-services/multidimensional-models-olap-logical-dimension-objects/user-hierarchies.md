---
title: Benutzerhierarchien | Microsoft Docs
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
- members [Analysis Services], hierarchies
- dimensions [Analysis Services], hierarchies
- user hierarchies [Analysis Services]
- hierarchies [Analysis Services], multilevel
- hierarchies [Analysis Services], attribute
- attributes [Analysis Services], hierarchies
- parent-child hierarchies [Analysis Services]
- hierarchies [Analysis Services], user
- ragged hierarchies [Analysis Services]
- balanced hierarchies [Analysis Services]
- hierarchies [Analysis Services]
- OLAP objects [Analysis Services], hierarchies
- multilevel hierarchies [Analysis Services]
- unbalanced hierarchies [Analysis Services]
ms.assetid: 9394e9a3-2242-4f0e-85e0-25d499d2d3b6
caps.latest.revision: "40"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 069f68e31f516a7f90a07cd462b70e0b455ab800
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="user-hierarchies"></a>Benutzerhierarchien
  Benutzerdefinierte Hierarchien werden von benutzerdefinierten Hierarchien von Attributen, die verwendet werden [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] die Elemente einer Dimension in Form von hierarchischen Strukturen zu organisieren und Navigationspfade in einem Cube bereitzustellen. In der folgenden Tabelle ist beispielsweise eine Dimensionstabelle für eine Zeitdimension definiert. Die Dimensionstabelle unterstützt die drei Attribute "Year", "Quarter" und "Month".  
  
|Year|Quarter|Month|  
|----------|-------------|-----------|  
|1999|Quartal 1|Jan|  
|1999|Quartal 1|Feb|  
|1999|Quartal 1|Mar|  
|1999|Quartal 2|Apr|  
|1999|Quartal 2|May|  
|1999|Quartal 2|Jun|  
|1999|Quarter 3|Jul|  
|1999|Quarter 3|Aug|  
|1999|Quarter 3|Sep|  
|1999|Quarter 4|Oct|  
|1999|Quarter 4|Nov|  
|1999|Quarter 4|Dec|  
  
 Die Attribute "Year", "Quarter" und "Month" werden verwendet, um in der Zeitdimension die benutzerdefinierte Hierarchie namens "Calendar" zu erstellen. Das Verhältnis zwischen den Ebenen und Elementen der Calendar-Dimension (eine reguläre Dimension) wird im folgenden Diagramm veranschaulicht.  
  
 ![Ebenen- und Elementhierarchie für eine Zeitdimension](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/media/as-levelconcepts.gif "Ebenen- und Elementhierarchie für eine Zeitdimension")  
  
> [!NOTE]  
>  Eine andere Hierarchie als die standardmäßige Attributhierarchie mit zwei Ebenen wird als benutzerdefinierte Hierarchie bezeichnet. Weitere Informationen zu Attributhierarchien, finden Sie unter [Attribute und Attributhierarchien](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md).  
  
## <a name="member-structures"></a>Elementstrukturen  
 Mit Ausnahme von Über-/Unterordnungshierarchien sind die Positionen der Elemente innerhalb der Hierarchie durch die Reihenfolge der Attribute in der Definition der Hierarchie festgelegt. Jedes Attribut in der Hierarchiedefinition bildet eine Ebene in der Hierarchie. Die Position eines Elements innerhalb einer Ebene wird durch die Anordnung der Attribute bestimmt, die zum Erstellen der Ebene verwendet werden. Die Elementstrukturen von benutzerdefinierten Hierarchien können je nachdem, welche Beziehungen zwischen den Elementen bestehen, eine von vier Formen annehmen.  
  
### <a name="balanced-hierarchies"></a>Ausgeglichene Hierarchien  
 In einer ausgeglichenen Hierarchie verzweigen alle Zweige der Hierarchie auf dieselbe Ebene, und das logisch übergeordnete Objekt jedes Elements befindet sich auf der Ebene unmittelbar über dem betreffenden Element. Die Product Categories-Hierarchie der Product-Dimension in der [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)]-Beispieldatenbank [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ist ein gutes Beispiel für eine ausgeglichene Hierarchie. Für jedes Element in der Product Name-Ebene gibt es ein übergeordnetes Element in der Subcategory-Ebene, für die es ein übergeordnetes Element in der Category-Ebene gibt. Auch hat jeder Zweig in der Hierarchie ein Blattelement in der Product Name-Ebene.  
  
### <a name="unbalanced-hierarchies"></a>Unausgeglichene Hierarchien  
 In einer unausgeglichenen Hierarchie verzweigen die Zweige der Hierarchie auf unterschiedliche Ebenen. Über-/Unterordnungshierarchien sind unausgeglichene Hierarchien. Die Organization-Dimension in der [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)]-Beispieldatenbank [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] enthält beispielsweise ein Element für jeden Mitarbeiter. Der CEO ist das oberste Element in der Hierarchie, und die Bereichsleiter und der Direktionssekretär befinden sich in der Hierarchie unmittelbar unterhalb des CEO. Den Bereichsleitern sind weitere Elemente untergeordnet, dem Direktionssekretär jedoch nicht.  
  
 Endbenutzer sind nicht immer in der Lage, zwischen unausgeglichenen und unregelmäßigen Hierarchien zu unterscheiden. Für die Unterstützung dieser beiden Arten von Hierarchien setzen Sie in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] jedoch unterschiedliche Techniken und Eigenschaften ein. Weitere Informationen finden Sie unter [unregelmäßige Hierarchien](../../analysis-services/multidimensional-models/user-defined-hierarchies-ragged-hierarchies.md), und [Attribute in über-/ Unterordnungshierarchien](../../analysis-services/multidimensional-models/parent-child-dimension-attributes.md).  
  
### <a name="ragged-hierarchies"></a>Unregelmäßige Hierarchien  
 In einer unregelmäßigen Hierarchie befindet sich das logisch übergeordnete Objekt mindestens eines Elements nicht auf der Ebene unmittelbar über dem betreffenden Element. Dies kann dazu führen, dass Zweige der Hierarchie auf unterschiedliche Ebenen verzweigen. In einer Geography-Dimension, für die die Ebenen Continent, CountryRegion und City in dieser Reihenfolge definiert wurden, wird das Europe-Element auf der obersten Ebene der Hierarchie, das France-Element auf der mittleren Ebene und das Paris-Element auf der untersten Ebene angezeigt. France ist genauer als Europe, und Paris ist genauer als France. An dieser regulären Hierarchie werden die folgenden Änderungen vorgenommen:  
  
-   Das Vatican City-Element wird der CountryRegion-Ebene hinzugefügt.  
  
-   Elemente werden der City-Ebene hinzugefügt und dem Vatican City-Element in der CountryRegion-Ebene zugeordnet.  
  
-   Die Ebene Province wird zwischen den Ebenen CountryRegion und City hinzugefügt.  
  
 Die Province-Ebene wird mit Elementen aufgefüllt, die anderen Elementen in der CountryRegion-Ebene zugeordnet sind, und Elemente in der City-Ebene sind den entsprechenden Elementen in der Province-Ebene zugeordnet. Da es jedoch für das Vatican City-Element in der CountryRegion-Ebene in der Province-Ebene keine zugeordneten Elemente gibt, müssen Elemente aus der City-Ebene dem Vatican City-Element in der CountryRegion-Ebene direkt zugeordnet werden. Aufgrund der Änderungen ist die Hierarchie der Dimensionen jetzt unregelmäßig. Das übergeordnete Element der Stadt Vatican City ist das Land bzw. die Region Vatican City, das bzw. die sich nicht in der Ebene direkt über dem Vatican City-Element in der City-Ebene befindet. Weitere Informationen finden Sie unter [Unregelmäßige Hierarchien](../../analysis-services/multidimensional-models/user-defined-hierarchies-ragged-hierarchies.md).  
  
### <a name="parent-child-hierarchies"></a>Über-/Unterordnungshierarchien  
 Über-/Unterordnungshierarchien für Dimensionen werden mithilfe eines speziellen Attributs, des so genannten übergeordneten Attributs, definiert, um zu bestimmen, welche Beziehungen es zwischen Elementen gibt. Ein übergeordnetes Attribut beschreibt eine *auf sich selbst verweisende Beziehung*oder einen *Selbstjoin*innerhalb einer Dimensionstabelle. Über-/Unterordnungshierarchien werden von einem einzelnen übergeordneten Attribut erstellt. Nur eine Ebene ist einer Über-/Unterordnungshierarchie zugewiesen, da die in der Hierarchie vorhandenen Ebenen aus den Über-/Unterordnungsbeziehungen zwischen Elementen, die mit dem übergeordneten Attribut verknüpft sind, abgerufen werden. Das Dimensionsschema einer Über-/Unterordnungshierarchie hängt von einer auf sich selbst verweisenden Beziehung in der Dimensionshaupttabelle ab. Das folgende Diagramm veranschaulicht beispielsweise die **DimOrganization** -dimensionshaupttabelle in der [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Beispieldatenbank.  
  
 ![Sich selbst verweisende Join in der DimOrganization-Tabelle](../../analysis-services/multidimensional-models/media/dimorganization.gif "sich selbst verweisende Join in der DimOrganization-Tabelle")  
  
 In dieser Dimensionshaupttabelle verfügt die Spalte **ParentOrganizationKey** über eine Fremdschlüsselbeziehung mit der Primärschlüsselspalte **OrganizationKey** . Mit anderen Worten: Jeder Datensatz in dieser Tabelle kann durch eine Über-/Unterordnungsbeziehung mit einem anderen Datensatz in der Tabelle verknüpft werden. Diese Art von Selbstjoin wird im Allgemeinen zum Darstellen von Organisationsentitätsdaten verwendet, z. B. für die Verwaltungsstruktur von Mitarbeitern in einer Abteilung.  
  
 Wenn Sie eine Über-/Unterordnungshierarchie erstellen, müssen die durch die beiden Attribute dargestellten Spalten denselben Datentyp aufweisen. Beide Attribute müssen sich zudem in derselben Tabelle befinden. Standardmäßig wird jedes Element, für das der Schlüssel des übergeordneten Elements dem eigenen Elementschlüssel, NULL, 0 (Null) oder einem Wert entspricht, der nicht in der Spalte der Elementschlüssel enthalten ist, als ein Element der obersten Ebene (ohne Alle-Ebene) erachtet.  
  
 Bei Über-/Unterordnungshierarchien können die Zweige der Hierarchie unterschiedlich tief verzweigt sein. Das bedeutet, dass eine Über-/Unterordnungshierarchie eine unausgeglichene Hierarchie darstellt.  
  
 Im Gegensatz zu benutzerdefinierten Hierarchien, bei denen die Anzahl der Ebenen in der Hierarchie die Anzahl der für die Endbenutzer sichtbaren Ebenen bestimmt, wird eine Über-/Unterordnungshierarchie mit einer einzelnen Ebene einer Attributhierarchie definiert. Die Werte in dieser einen Ebene erzeugen die für die Benutzer sichtbaren mehreren Ebenen. Die Anzahl der angezeigten Ebenen hängt vom Inhalt der Dimensionstabellenspalten ab, in denen die Elementschlüssel und die Schlüssel der übergeordneten Elemente gespeichert sind. Die Anzahl der Ebenen kann sich ändern, wenn die Daten in den Dimensionstabellen geändert werden. Weitere Informationen finden Sie unter [über-und untergeordneten Dimensionen](../../analysis-services/multidimensional-models/parent-child-dimension.md), und [Attribute in über-/ Unterordnungshierarchien](../../analysis-services/multidimensional-models/parent-child-dimension-attributes.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen von benutzerdefinierten Hierarchien](../../analysis-services/multidimensional-models/user-defined-hierarchies-create.md)   
 [Eigenschaften der Benutzerhierarchie](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)   
 [Dimensionsattributeigenschaften-Verweis](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
