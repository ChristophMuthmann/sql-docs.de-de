---
title: Accounts-Element (ASSL) | Microsoft Docs
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
apiname: Accounts Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Accounts
helpviewer_keywords: Accounts element
ms.assetid: 3ec62f58-c19b-4b15-b040-8941521a389b
caps.latest.revision: "44"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 00d2c1edfe91f2c0223df776ff90b4c9a33bb34b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="accounts-element-assl"></a>Accounts-Element (ASSL)
  Enthält die Auflistung der Kontotypen, die in definierten ein [Datenbank](../../../analysis-services/scripting/objects/database-element-assl.md) Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Database>  
   ...  
   <Accounts>  
      <Account>...</Account>  
   </Accounts>  
   ...  
</Database>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Keine (Auflistung)|  
|Standardwert|Keine (Auflistung)|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Datenbank](../../../analysis-services/scripting/objects/database-element-assl.md)|  
|Untergeordnete Elemente|[Konto](../../../analysis-services/scripting/objects/account-element-assl.md)|  
  
## <a name="remarks"></a>Hinweise  
 Dimensionen, deren [Typ](../../../analysis-services/scripting/properties/type-element-dimension-assl.md) -Elementgruppe ist *Konten*, haben Sie ein Attribut, das den Kontotyp, wie "Income", "Expense gibt an, und so weiter von Elementen in der Dimension dargestellt. Der Kontotyp wird dann von verwendet [Measure](../../../analysis-services/scripting/objects/measure-element-assl.md) Elemente, deren [AggregationFunction](../../../analysis-services/scripting/properties/aggregatefunction-element-assl.md) -Elementgruppe ist *ByAccount*, um zu bestimmen, die Aggregatfunktion verwendet wird, wenn aggregieren Sie die Elemente dieser Dimension. Das **Accounts** -Element enthält eine Auflistung von **Account** -Elementen, die Kontotypen und die zu verwendende Aggregatfunktion für die einzelnen Kontotypen darstellen.  
  
 Ein Kontotyp muss aufgelistet sein, wenn die Aggregatfunktion verwendeten vom Standard abweicht [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] für jeden Kontotyp.  
  
 Der Satz gültiger Kontotypen kann nicht geändert werden.  
  
 Das entsprechende Element im Objektmodell von Analysis Management Objects (AMO) ist <xref:Microsoft.AnalysisServices.AccountCollection>.  
  
## <a name="see-also"></a>Siehe auch  
 [AccountType-Element &#40; ASSL &#41;](../../../analysis-services/scripting/properties/accounttype-element-assl.md)   
 [Schemaauflistungen &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
