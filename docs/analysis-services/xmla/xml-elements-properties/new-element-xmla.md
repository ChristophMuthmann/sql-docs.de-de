---
title: New-Element (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- New Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#New
- microsoft.xml.analysis.new
- urn:schemas-microsoft-com:xml-analysis#New
helpviewer_keywords:
- New element
ms.assetid: 1321adcb-67f7-40f0-8f20-b17c1d3e3f17
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: cfb645f7e64ddc004da4a4b42203d48d484dcf69
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="new-element-xmla"></a>New-Element (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Enthält den neuen von einem [Folder](../../../analysis-services/xmla/xml-elements-properties/folder-element-xmla.md) -Element verwendeten Speicherort des Dateisystems.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Folder>  
   ...  
   <New>...</New>  
   ...  
</Folder>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|String|  
|Standardwert|Keine|  
|Kardinalität|1-1: Erforderliches Element, das nur einmal auftritt.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Ordner](../../../analysis-services/xmla/xml-elements-properties/folder-element-xmla.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Das **New** -Element enthält einen UNC-Pfad, der während eines **Original** - oder **Folder** -Befehls den Wert des **Restore** -Elements ersetzt, das im übergeordneten **Synchronize** -Element für alle wiederhergestellten oder synchronisierten Objekte enthalten ist. Der Wert des **Original** -Elements wird mit dem Wert des **StorageLocation** -Elements für die einzelnen Cubes, Measuregruppen oder Partitionen verglichen. Wenn eine Übereinstimmung festgestellt wird, wird der Wert dieses Elements für das Update der **StorageLocation** des Objekts während der Wiederherstellung oder Synchronisierung verwendet.  
  
 Weitere Informationen zum Sichern und Wiederherstellen von Objekten finden Sie unter [Sichern und Wiederherstellen von Objekten (XMLA)](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Original-Element & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/original-element-xmla.md)   
 [Restore-Element & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)   
 [StorageLocation-Element & #40; ASSL & #41;](../../../analysis-services/scripting/properties/storagelocation-element-assl.md)   
 [Synchronisieren Sie-Element & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)   
 [Datenbankeigenschaften & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
