---
title: Isolation-Element (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- Isolation Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Isolation element
ms.assetid: 28c98c6f-668e-4547-8d25-127cc3995a7d
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 3f86379a2494b324c7d801887cb900ac6ff53274
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="isolation-element-assl"></a>Isolation-Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Gibt die Isolationsstufe für ein Element, das von abgeleitet ist die [DataSource](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md) -Datentyp.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<DataSource>  
   ...  
   <Isolation>...</Isolation>  
   ...  
</DataSource>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge (Enumeration)|  
|Standardwert|*ReadCommitted.*|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[DataSource](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Der Wert dieses Elements ist auf eine der in der folgenden Tabelle aufgelisteten Zeichenfolgen beschränkt.  
  
|Wert|Description|  
|-----------|-----------------|  
|*ReadCommitted.*|Gibt an, dass Anweisungen Zeilen nicht lesen können, die von anderen Transaktionen geändert wurden, für die jedoch noch kein Commit ausgeführt wurde. Dadurch werden Dirty Reads verhindert. Andere Transaktionen können Daten zwischen einzelnen Anweisungen innerhalb der aktuellen Transaktion ändern. Dies führt zu nicht wiederholbaren Lesevorgängen oder Phantomdaten. Dieser Wert ist der Standardwert für das **Isolation** -Element.|  
|*Momentaufnahme*|Gibt an, dass die von einer beliebigen Anweisung in einer Transaktion gelesenen Daten der im Hinblick auf Transaktionen konsistenten Version der Daten entsprechen, die zu Beginn der Transaktion vorhanden waren. Die Transaktion kann nur Datenänderungen erkennen, für die vor dem Beginn der Transaktion ein Commit ausgeführt wurde. Datenänderungen, die nach dem Start der aktuellen Transaktion durch andere Transaktionen vorgenommen wurden, sind für die Anweisungen, die in der aktuellen Transaktion ausgeführt werden, nicht sichtbar. So entsteht der Eindruck, als ob die Anweisungen in einer Transaktion eine Momentaufnahme der Daten erhalten, für die ein Commit ausgeführt wurde, wie sie zu Beginn der Transaktion vorhanden waren.|  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
