---
title: Element (XMLA) führt | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- results Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.results
- urn:schemas-microsoft-com:xml-analysis#results
- http://schemas.microsoft.com/analysisservices/2003/engine#results
helpviewer_keywords:
- results element
ms.assetid: 3249a17a-7bfa-4753-b605-8f611ba7ae2b
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 850357c79f7ebda3c8744d72eb5fbcb1a6efd8ff
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="results-element-xmla"></a>results-Element (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Enthält eine Auflistung von [root](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) -Elementen, die von der [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) -Methode mit dem Befehl [Batch](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md) zurückgegeben werden.  
  
 **Namespace** `http://schemas.microsoft.com/analysisservices/2003/xmla-multipleresults`  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<return>  
   <results>  
      <root>...</root>  
   </results>  
</return>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Keine|  
|Standardwert|Keine|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Rückgabewert](../../../analysis-services/xmla/xml-elements-properties/return-element-xmla.md)|  
|Untergeordnete Elemente|[Stamm](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)|  
  
## <a name="remarks"></a>Hinweise  
 Wenn ein **Batch** -Befehl von der **Execute** -Methode ausgeführt wird, enthält das **return** -Element statt eines einzelnen **results** -Elements ein einzelnes **root** -Element. Der Inhalt des **results** -Elements hängt von den Einstellungen ab, die verwendet werden, um den Befehl **Batch** auszuführen.  
  
 Für nicht transaktionale **Batch** -Befehle enthält das **results** -Element ein **root** -Element für jeden Befehl, der vom **Batch** -Befehl ausgeführt wird, und zwar unabhängig davon, ob der Befehl erfolgreich abgeschlossen werden kann oder nicht. Für transaktionale **Batch** -Befehle enthält das **results** -Element nur ein **root** -Element, das die Fehlerinformationen für den Befehl enthält, der innerhalb des **Batch** -Befehls fehlgeschlagen ist.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
