---
title: InheritTypeEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: InheritTypeEnum
helpviewer_keywords: InheritTypeEnum enumeration [ADOX]
ms.assetid: c2f6ce79-c4b3-4d40-ac95-21025208f991
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 33635119675c7ebe69f7c8a6d17f5c687d8785bb
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="inherittypeenum"></a>InheritTypeEnum
Gibt an, wie Objekte mit festgelegten Berechtigungen erben [SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md).  
  
|Konstante|value|Description|  
|--------------|-----------|-----------------|  
|**adInheritBoth**|3|Objekte und andere Container, die das primäre Objekt enthalten sind, erben den Eintrag.|  
|**adInheritContainers**|2|Andere Container, die vom primären Objekt enthalten sind, erben den Eintrag.|  
|**adInheritNone**|0|Standard. Es tritt keine Vererbung auf.|  
|**adInheritNoPropagate**|4|Die **AdInheritObjects** und **AdInheritContainers** Flags werden nicht an einen geerbten Eintrag weitergegeben.|  
|**adInheritObjects**|1|Nicht-Container-Objekte im Container erben die Berechtigungen.|  
  
## <a name="applies-to"></a>Gilt für  
 [SetPermissions-Methode (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)
