---
title: AllowNullsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- AllowNullsEnum
helpviewer_keywords:
- AllowNullsEnum enumeration [ADOX]
ms.assetid: 6acf3689-1a7f-4379-9d7f-df452ccbac27
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3b321045efcf77e3e0a5922638b8437903a69bef
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="allownullsenum"></a>AllowNullsEnum
Gibt an, ob Datensätze mit null-Werte indiziert werden.  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adIndexNullsAllow**|0|Der Index lässt Einträge in denen die Schlüsselspalten null sind. Wenn ein null-Wert in einer Schlüsselspalte eingegeben wird, wird der Eintrag in den Index eingefügt.|  
|**adIndexNullsDisallow**|1|Standard. Der Index lässt keine Einträge in denen die Schlüsselspalten null sind. Wenn ein null-Wert in einer Schlüsselspalte eingegeben wird, tritt ein Fehler auf.|  
|**adIndexNullsIgnore**|2|Bei Einträgen, die null-Schlüssel wird der Index nicht eingefügt werden. Wenn ein null-Wert in einer Schlüsselspalte eingegeben wird, wird der Eintrag ignoriert, und kein Fehler auftritt.|  
|**adIndexNullsIgnoreAny**|4|Der Index werden keine Einträge eingefügt, in denen einige Schlüsselspalte einen null-Wert aufweist. Für einen Index mit einem mehrspaltigen Schlüssel, wenn ein null-Wert in einer Spalte eingegeben wird der Eintrag ignoriert und kein Fehler auftritt.|  
  
## <a name="applies-to"></a>Gilt für  
 [IndexNulls-Eigenschaft (ADOX)](../../../ado/reference/adox-api/indexnulls-property-adox.md)
