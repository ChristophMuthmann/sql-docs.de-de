---
title: InheritTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- InheritTypeEnum
helpviewer_keywords:
- InheritTypeEnum enumeration [ADOX]
ms.assetid: c2f6ce79-c4b3-4d40-ac95-21025208f991
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d4d822bd48d399b767c6676e014abe3d733aa5bc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="inherittypeenum"></a>InheritTypeEnum
Gibt an, wie Objekte mit festgelegten Berechtigungen erben [SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md).  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adInheritBoth**|3|Objekte und andere Container, die das primäre Objekt enthalten sind, erben den Eintrag.|  
|**adInheritContainers**|2|Andere Container, die vom primären Objekt enthalten sind, erben den Eintrag.|  
|**adInheritNone**|0|Standard. Es tritt keine Vererbung auf.|  
|**adInheritNoPropagate**|4|Die **AdInheritObjects** und **AdInheritContainers** Flags werden nicht an einen geerbten Eintrag weitergegeben.|  
|**adInheritObjects**|1|Nicht-Container-Objekte im Container erben die Berechtigungen.|  
  
## <a name="applies-to"></a>Gilt für  
 [SetPermissions-Methode (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)
