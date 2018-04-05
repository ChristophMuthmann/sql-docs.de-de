---
title: Subscribe-Element (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Subscribe Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Subscribe
- microsoft.xml.analysis.subscribe
- http://schemas.microsoft.com/analysisservices/2003/engine#Subscribe
helpviewer_keywords:
- Subscribe command
ms.assetid: aad50dd7-44d4-4d83-a973-187f9aed35ec
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 47425fd75c42d70ad98172eee2070bdcb9b2db45
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="subscribe-element-xmla"></a>Subscribe-Element (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Abonniert eine Ablaufverfolgung und gibt ein Rowset, das die Ablaufverfolgungsereignisse einer [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Instanz.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Command>  
   <Subscribe>  
      <Object>...</Object>  
   </Subscribe>  
</Command>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Description|  
|--------------------|-----------------|  
|Datentyp und -länge|InclusionThresholdSetting|  
|Standardwert|InclusionThresholdSetting|  
|Cardinality|0-n: Optionales Element, das mehr als einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Befehl](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|Untergeordnete Elemente|[Objekt](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 Die **abonnieren** Befehl abonniert und Streams Sichern eines Rowsets aus einer angegebenen Ablaufverfolgung für eine [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Instanz. Wenn ein anderes Objekt als die Ablaufverfolgung im **Object** -Element angegeben wird, tritt ein Fehler auf.  
  
 Wenn die **Objekt** Element nicht angegeben wird, eine sitzungsablaufverfolgung definiert und auf abonniert die [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Instanz. Die Sitzungsablaufverfolgung gibt einen festen Satz von Ablaufverfolgungsereignissen der aktuellen Sitzung zurück.  
  
 Der Rowset-Datenstrom zurückgegeben, die mit diesem Befehl wird beendet, wenn die Clientanwendung die Verbindung geschlossen wird die [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Instanz, oder, wenn die Sitzung auf dem die **abonnieren** Befehl wird ausgeführt, wird beendet.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Befehle &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
