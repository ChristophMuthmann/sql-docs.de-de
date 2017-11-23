---
title: StorageLocation-Element (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
apiname: StorageLocation Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: StorageLocation
helpviewer_keywords: StorageLocation element
ms.assetid: ecf8852f-56a1-4fcf-b0d8-d7eebb75e4ed
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f29d736c11dd7297d024bc9e6f72c93a521e84ff
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="storagelocation-element-assl"></a>StorageLocation-Element (ASSL)
  Enthält den Speicherort des Dateisystems für den Inhalt des übergeordneten Elements.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Cube><!-- or MeasureGroup, Partition -->  
      ...  
   <StorageLocation>...</StorageLocation>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|String|  
|Standardwert|Finden Sie in der folgenden Tabelle aus.|  
|Cardinality|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
|Vorgänger oder übergeordnetes Element|Standardwert|  
|------------------------|-------------------|  
|[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)|Keine|  
|[MeasureGroup-Objekt](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|Der Wert des **StorageLocation** vom übergeordneten **Cube** -Element.|  
|[Partition](../../../analysis-services/scripting/objects/partition-element-assl.md)|Der Wert des **StorageLocation** vom übergeordneten **MeasureGroup** -Element.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md), [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md), [Partition](../../../analysis-services/scripting/objects/partition-element-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Die Elemente, die den übergeordneten Elementen von entsprechen **StorageLocation** im Objektmodell von Analysis Management Objects (AMO) sind <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.MeasureGroup>, und <xref:Microsoft.AnalysisServices.Partition>.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
