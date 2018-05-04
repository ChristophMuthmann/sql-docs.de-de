---
title: Konto-Element (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Account Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Account
helpviewer_keywords:
- Account element
ms.assetid: 0bb7d06c-0158-4ab2-b2b1-cb50ba24f7c0
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 54da4e03516002762f0312e50bcf1256279be58f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="account-element-assl"></a>Account-Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Enthält Details über einen Kontotyp innerhalb einer [Datenbank](../../../analysis-services/scripting/objects/database-element-assl.md) Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Accounts>  
   <Account>  
      <AccountType>...</AccountType>  
      <AggregationFunction>...</AggregationFunction>  
            <Aliases>...</Aliases>  
            <Annotations>...</Annotations>  
   </Account>  
</Accounts>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Keine|  
|Standardwert|Keine|  
|Kardinalität|0-n: Optionales Element, das mehr als einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Konten](../../../analysis-services/scripting/collections/accounts-element-assl.md)|  
|Untergeordnete Elemente|[AccountType](../../../analysis-services/scripting/properties/accounttype-element-assl.md), [AggregationFunction](../../../analysis-services/scripting/properties/aggregationfunction-element-assl.md), [Aliase](../../../analysis-services/scripting/collections/aliases-element-assl.md), [Anmerkungen](../../../analysis-services/scripting/collections/annotations-element-assl.md)|  
  
## <a name="remarks"></a>Hinweise  
 Dimensionen, deren [Typ](../../../analysis-services/scripting/properties/type-element-dimension-assl.md) -Elementgruppe ist *Konten,* können ein Attribut, das gibt des Kontotyp, wie "Income", "Expense und usw., dargestellt durch Elemente in der Dimension haben. Der Kontotyp wird dann von verwendet [Measure](../../../analysis-services/scripting/objects/measure-element-assl.md) Elemente, deren [AggregationFunction](../../../analysis-services/scripting/properties/aggregatefunction-element-assl.md) -Elementgruppe ist *ByAccount*, um zu bestimmen, die Aggregatfunktion verwendet wird, wenn aggregieren Sie die Elemente dieser Dimension. Das **Account** -Element stellt einen einzelnen Kontotyp sowie die Aggregationsfunktion dar, die von solchen Measures verwendet werden sollte.  
  
 Ein Kontotyp muss aufgelistet sein, wenn die Aggregatfunktion verwendeten vom Standard abweicht [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] für jeden Kontotyp.  
  
 Der Satz gültiger Kontotypen kann nicht geändert werden.  
  
 Das entsprechende Element im Objektmodell von Analysis Management Objects (AMO) ist <xref:Microsoft.AnalysisServices.Account>.  
  
## <a name="see-also"></a>Siehe auch  
 [Database-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/database-element-assl.md)   
 [Objekte & #40; ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
