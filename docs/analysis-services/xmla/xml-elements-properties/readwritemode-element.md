---
title: ReadWriteMode-Element | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords: ReadWriteMode command
ms.assetid: 379bcaca-bb7e-4934-a9e7-21f8ede2fdc7
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d55928ce65b1b40710b662c6d3f5b55b798368a9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="readwritemode-element"></a>ReadWriteMode-Element
  Die **ReadWriteMode** -Datenbankeigenschaft gibt an, ob sich die Datenbank im **ReadWrite** -Modus oder im **ReadOnly** -Modus befindet. Hierbei handelt es sich um die beiden einzigen möglichen Werte der Eigenschaft.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Database>  
...  
   <ddlns_100_0:ReadWriteMode>...</ddlns_100_0:ReadWriteMode>  
...  
</Database>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge (Enumeration)|  
|Standardwert|ReadWrite|  
|Kardinalität|0-1: Optionales Element, das mehr als einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Datenbank](../../../analysis-services/xmla/xml-elements-properties/database-element-xmla.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Datenbanken können nur im **ReadWrite** -Modus erstellt werden. Datenbanken können nicht im **ReadOnly** -Modus erstellt werden.  
  
 Der Wert des **ReadWriteMode** -Elements ist auf eine der in der folgenden Tabelle aufgelisteten Zeichenfolgen beschränkt.  
  
|Wert|Description|  
|-----------|-----------------|  
|*ReadOnly*|Es können keine Änderungen oder Updates auf die Datenbank angewendet werden.|  
|*ReadWrite*|Es können Änderungen oder Updates auf die Datenbank angewendet werden.|  
  
## <a name="see-also"></a>Siehe auch  
 [Attach-Element](../../../analysis-services/xmla/xml-elements-commands/attach-element.md)   
 [Anfügen und Trennen von Analysis Services-Datenbanken](../../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [Verschieben einer Analysis Services-Datenbank](../../../analysis-services/multidimensional-models/move-an-analysis-services-database.md)   
 [Datenbank-ReadWriteModes](../../../analysis-services/multidimensional-models/database-readwritemodes.md)   
 [Umschalten Sie in einer Analysis Services-Datenbank zwischen Schreib-und Lesemodus](../../../analysis-services/multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)  
  
  
