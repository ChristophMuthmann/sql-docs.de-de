---
title: Folder-Element (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Folder Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.folder
- http://schemas.microsoft.com/analysisservices/2003/engine#Folder
- urn:schemas-microsoft-com:xml-analysis#Folder
helpviewer_keywords:
- Folder element
ms.assetid: 87b305b0-57e3-4ec3-9d80-f1bcf3ce7540
caps.latest.revision: 12
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a4e3a685de817e213923c6eba8f4cb251fe574a5
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="folder-element-xmla"></a>Folder-Element (XMLA)
  Enthält einen Speicherort im Dateisystem aktualisiert werden muss eine [Speicherort](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md) -Element während einer [wiederherstellen](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md) oder [Synchronize](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md) Befehl.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Folders>  
   ...  
   <Folder>  
      <Original>...</Original>  
      <New>...</New>  
   </Folder>  
   ...  
</Folders>  
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
|Übergeordnete Elemente|[Ordner](../../../analysis-services/xmla/xml-elements-properties/folders-element-xmla.md)|  
|Untergeordnete Elemente|[Neue](../../../analysis-services/xmla/xml-elements-properties/new-element-xmla.md), [ursprünglichen](../../../analysis-services/xmla/xml-elements-properties/original-element-xmla.md)|  
  
## <a name="remarks"></a>Hinweise  
 Das **Folder** -Element ändert, wenn es angegeben ist, die Speicherorte der Objekte, die entweder in der Sicherungsdatei ( **Restore** -Befehle) oder der Datenbank auf der Quellinstanz ( **Synchronize** -Befehle) enthalten sind und die den Wert des **Original** -Elements mit dem Wert des **New** -Elements abgleichen.  
  
 Weitere Informationen zum Sichern und Wiederherstellen von Objekten finden Sie unter [sichern, wiederherstellen, und Synchronisieren von Datenbanken &#40; XMLA &#41; ](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>Siehe auch  
 [StorageLocation-Element &#40; ASSL &#41;](../../../analysis-services/scripting/properties/storagelocation-element-assl.md)   
 [Datenbankeigenschaften &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

