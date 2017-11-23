---
title: Password-Element (XMLA) | Microsoft Docs
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
apiname: Password Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Password
- urn:schemas-microsoft-com:xml-analysis#Password
- microsoft.xml.analysis.password
helpviewer_keywords: Password element
ms.assetid: 8a0603bd-f6a1-4b86-84f1-c83d0b03951b
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0e7d330f5cb2b92223ca897034130a908007afdc
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="password-element-xmla"></a>Password-Element (XMLA)
  Bestimmt das Kennwort, das vom übergeordneten Element verwendet werden [Backup](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md) oder [wiederherstellen](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md) -Befehl zum Verschlüsseln oder Entschlüsseln einer Sicherungsdatei.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Backup> <!-- or Restore -->  
   ...  
   <Password>...</Password>  
   ...  
</Backup>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|String|  
|Standardwert|Keine|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Sicherung](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md), [wiederherstellen](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Wenn ein **Backup** -Befehl kein **Password** -Element oder eine leere Zeichenfolge enthält, wird die Sicherungsdatei nicht verschlüsselt.  
  
 Wenn ein **Restore** -Befehl beim Versuch, eine verschlüsselte Sicherungsdatei wiederherzustellen, kein **Password** -Element oder eine leere Zeichenfolge enthält, tritt ein Fehler auf.  
  
 Wenn entweder ein **Location** oder ein **Backup** -Befehl **Restore** -Elemente enthält, wird genau dieses **Password** -Element für die Sicherungs- und Remotesicherungsdateien verwendet. Weitere Informationen zu remotesicherungsdateien finden Sie unter [sichern, wiederherstellen, und Synchronisieren von Datenbanken &#40; XMLA &#41; ](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Location-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md)   
 [Datenbankeigenschaften &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
