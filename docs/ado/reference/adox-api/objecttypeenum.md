---
title: ObjectTypeEnum | Microsoft Docs
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
f1_keywords: ObjectTypeEnum
helpviewer_keywords: ObjectTypeEnum enumeration [ADOX]
ms.assetid: 3fdecfca-aa91-4596-ad98-610f1b7f840b
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b4907a7ea076a38c4f0832cf5e33b1cbcae57f15
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="objecttypeenum"></a>ObjectTypeEnum
Gibt den Typ des Datenbankobjekts für das Berechtigungen oder Besitzer festgelegt.  
  
|Konstante|value|Description|  
|--------------|-----------|-----------------|  
|**adPermObjColumn**|2|Das Objekt ist eine Spalte an.|  
|**adPermObjDatabase**|3|Das Objekt ist eine Datenbank.|  
|**adPermObjProcedure**|4|Das Objekt ist eine Prozedur.|  
|**adPermObjProviderSpecific**|-1|Das Objekt ist ein Typ, der vom Anbieter definiert. Es wird eine Fehlermeldung angezeigt, wenn die *ObjectType* Parameter ist **AdPermObjProviderSpecific** und ein *ObjectTypeId* nicht angegeben wird.|  
|**adPermObjTable**|1|Das Objekt ist eine Tabelle.|  
|**adPermObjView**|5|Das Objekt ist eine Sicht.|  
  
## <a name="applies-to"></a>Gilt für  
  
|||  
|-|-|  
|[GetObjectOwner-Methode (ADOX)](../../../ado/reference/adox-api/getobjectowner-method-adox.md)|[GetPermissions-Methode (ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)|  
|[SetObjectOwner-Methode](../../../ado/reference/adox-api/setobjectowner-method.md)|[SetPermissions-Methode (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)|
