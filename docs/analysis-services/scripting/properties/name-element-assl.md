---
title: Name-Element (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Name Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Name
helpviewer_keywords: Name element
ms.assetid: caf2af86-5f9c-4e14-8168-f3a79248b4fe
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ec0f34bbcfa45f2ca704506374886c8ba591eca9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="name-element-assl"></a>Name-Element (ASSL)
  Enthält den Namen des übergeordneten Elements.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Action> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Name>...</Name>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge (bis zu 100 Zeichen)|  
|Standardwert|Unterschiedlich|  
|Kardinalität|1-1: Erforderliches Element, das nur einmal auftritt|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Aktion](../../../analysis-services/scripting/objects/action-element-assl.md), [Aggregation](../../../analysis-services/scripting/objects/aggregation-element-assl.md), [AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md), [AlgorithmParameter](../../../analysis-services/scripting/objects/algorithmparameter-element-assl.md), [Anmerkung](../../../analysis-services/scripting/objects/annotation-element-assl.md), [ Assembly](../../../analysis-services/scripting/objects/assembly-element-assl.md), [ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md), [Cube](../../../analysis-services/scripting/objects/cube-element-assl.md), [CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md), [CubeHierarchy](../../../analysis-services/scripting/data-type/cubehierarchy-data-type-assl.md), [Datenbank](../../../analysis-services/scripting/objects/database-element-assl.md), [DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md), [DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md), [Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md), [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md), [Gruppe](../../../analysis-services/scripting/objects/group-element-assl.md), [Hierarchie](../../../analysis-services/scripting/objects/hierarchy-element-assl.md), [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md), [Ebene](../../../analysis-services/scripting/objects/level-element-assl.md), [MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md), [ Measure](../../../analysis-services/scripting/objects/measure-element-assl.md), [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md), [MemberProperty](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md), [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md), [MiningModelColumn](../../../analysis-services/scripting/data-type/miningmodelcolumn-data-type-assl.md), [ MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md), [MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md), [Partition](../../../analysis-services/scripting/objects/partition-element-assl.md), [Berechtigung](../../../analysis-services/scripting/data-type/permission-data-type-assl.md), [ Perspektive](../../../analysis-services/scripting/objects/perspective-element-assl.md), [PerspectiveCalculation](../../../analysis-services/scripting/data-type/perspectivecalculation-data-type-assl.md), [ReportFormatParameter](../../../analysis-services/scripting/objects/reportformatparameter-element-asl.md), [ReportParameter](../../../analysis-services/scripting/objects/reportparameter-element-assl.md), [ Rolle](../../../analysis-services/scripting/objects/role-element-assl.md), [Server](../../../analysis-services/scripting/objects/server-element-assl.md), [ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md), [Trace](../../../analysis-services/scripting/objects/trace-element-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Jedes Element, das verwendet wird, definieren Sie ein Objekt (eine Instanz von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], einer Hierarchie, ein Attribut usw.) verfügt über eine **Namen** -Element als Eigenschaft. Der Wert eines **Name** -Elements hat die folgenden Einschränkungen:  
  
-   Der Wert darf keine führenden oder nachgestellten Leerzeichen enthalten. Wenn im Wert des führende oder nachgestellte Leerzeichen enthalten sind eine **Namen** Element, diese Leerzeichen implizit durch entfernt [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
-   Der Wert sollte keine Steuerzeichen enthalten. Es wird dringend von Steuerzeichen in einem Namen abgeraten, da dies in einigen Fällen zu XML-Überprüfungsfehlern führen kann.  
  
     Für Objekte erstellt, mit der **GetNewName** Methode in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], AMO sucht und entfernt diese anschließend alle Steuerzeichen sowie führende oder nachfolgende Leerzeichen im Namen. Aus diesem Grund wird empfohlen, **GetNewName** zum Festlegen von Objektnamen zu verwenden.  
  
     Beim direkten Festlegen der **Name** -Eigenschaft werden jedoch nicht die gleichen Überprüfungen ausgeführt, was zu XML-Überprüfungsfehlern führen kann. Ob ein Fehler tatsächlich auftritt, hängt davon ab, welches Steuerzeichen im Namen vorkommt.  
  
     Obwohl in Objektnamen grundsätzlich auf Steuerzeichen verzichtet werden sollte, wird deren Verwendung von Analysis Services nicht ausdrücklich untersagt. Von früheren Analysis Services-Versionen wurden manchmal Steuerzeichen in Objektnamen akzeptiert. Für diesen Grund, SQL Server 2016 Analysis Services und später Steuerzeichen in Objektnamen, um zu vermeiden, dass ältere Lösungen ignoriert.  
  
-   Die folgenden reservierten Werte können nicht verwendet werden:  
  
    -   AUX  
  
    -   CLOCK$  
  
    -   COM1 bis COM9 (COM1, COM2, COM3 usw.)  
  
    -   CON  
  
    -   LPT1 bis LPT9 (LPT1, LPT2, LPT3 usw.)  
  
    -   NUL  
  
    -   PRN  
  
 Die folgende Tabelle führt zusätzliche Zeichen auf, die abhängig vom übergeordneten Element nicht im Wert eines **Name** -Elements verwendet werden können.  
  
|Übergeordnetes Element|Ungültige Zeichen|  
|--------------------|------------------------|  
|[Server](../../../analysis-services/scripting/objects/server-element-assl.md)|Der Name muss den Regeln für [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows-Computernamen. IP-Adressen sind nicht gültig.|  
|[Datenquelle](../../../analysis-services/scripting/objects/datasource-element-assl.md)|:/\\*&#124;?"()[]{}<>|  
|[Ebene](../../../analysis-services/scripting/objects/level-element-assl.md), [-Attribut-Element](../../../analysis-services/scripting/objects/attribute-element-assl.md)|.,;'`:/\\*&#124;?"&%$!+=[]{}<>|  
|Alle anderen übergeordneten Elemente|.,;'`:/\\*&#124;?"&%$!+=()[]{}<>|  
  
## <a name="see-also"></a>Siehe auch  
 [ID-Element &#40; ASSL &#41;](../../../analysis-services/scripting/properties/id-element-assl.md)   
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
