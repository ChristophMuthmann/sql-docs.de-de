---
title: IsDefaultImage-Element (XML) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: e29cd137-af82-4753-a681-0d3e705513f3
caps.latest.revision: 6
author: jeannt
ms.author: jeannt
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ed09bbccf5bb5aa399fbab0c9e6a58c7f58c7ecd
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="isdefaultimage-element-xml"></a>IsDefaultImage-Element (XML)
  Gibt an, dass die Möglichkeit besteht, das Standardimage für diese Entität durch Navigieren von dieser Beziehung zur anderen Tabelle und durch Abrufen des Members mit dem Attribut "IsDefaultImage" abzurufen.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<RelationshipEndVisualizationProperties>  
   ...  
   <IsDefaultImage>...</IsDefaultImage>  
   ...  
</RelationshipEndVisualizationProperties>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Boolean|  
|Standardwert|false|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftritt.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[RelationshipEndVisualizationProperties](../../../analysis-services/scripting/data-type/relationshipendvisualizationproperties-data-type-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Für **RelationshipEndVisualizationProperties** -Elemente gibt das **IsDefaultImage** -Element an, dass das Standardimage für diese Entität durch Navigieren zum anderen Ende dieser Beziehung abgerufen werden kann. Der Standardwert **false** gibt an, dass kein abzurufendes Standardimage vorhanden ist.  
  
  
