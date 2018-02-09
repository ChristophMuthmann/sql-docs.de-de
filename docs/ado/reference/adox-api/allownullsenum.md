---
title: AllowNullsEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- AllowNullsEnum
helpviewer_keywords:
- AllowNullsEnum enumeration [ADOX]
ms.assetid: 6acf3689-1a7f-4379-9d7f-df452ccbac27
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 75bb6aa82ec26e74675a2ccf6ff803abd9d24f6c
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
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
