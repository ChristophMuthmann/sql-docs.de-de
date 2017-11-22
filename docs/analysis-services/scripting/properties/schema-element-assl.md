---
title: Schema-Element (ASSL) | Microsoft Docs
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
apiname: Schema Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Schema
helpviewer_keywords: Schema element
ms.assetid: 4b6375fb-7ad8-4d5f-88b1-abd3da2654db
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a39f50d6c91a8f4a321c62943e8894777c376faf
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="schema-element-assl"></a>Schema-Element (ASSL)
  Enthält das Schema der Datenquellensicht.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<DataSourceView>  
   ...  
   <Schema>...</Schema>  
   ...  
</DataSourceView>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Schema|  
|Standardwert|Keine|  
|Kardinalität|1-1: Erforderliches Element, das nur einmal auftritt.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[DataSourceView-Objekt](../../../analysis-services/scripting/objects/datasourceview-element-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Die **Schema** wird dargestellt, mit dem XML-Schemadefinition (XSD) Sprachformat des DataSets in der [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework, wobei einige Erweiterungen für DataSets und andere spezifisch für die Verwendung in der Definition Datendefinitionssprache (DDL). DataSets definieren eine flexible Zuordnung von XSD zu einem relationalen Schema, aber geben XSD in einer kanonischeren Form zurück. Nur diese kanonische Form ist innerhalb der Datenquellen gültig.  
  
 Das Element, das das übergeordnete Element des entspricht **Schema** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.DataSourceView>.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
