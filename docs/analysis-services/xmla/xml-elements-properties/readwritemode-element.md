---
title: ReadWriteMode-Element | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
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
ms.openlocfilehash: 8ed345b4e0562fd61b7995d91bd2db12cad4cd57
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="readwritemode-element"></a>ReadWriteMode-Element
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Die **ReadWriteMode** -Datenbankeigenschaft gibt an, ob die Datenbank im **ReadWrite** Modus oder im **ReadOnly** Modus. Hierbei handelt es sich um die beiden einzigen möglichen Werte der Eigenschaft.  
  
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
  
  
