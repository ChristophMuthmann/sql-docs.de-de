---
title: ActionEnum | Microsoft Docs
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
- ActionEnum
helpviewer_keywords:
- ActionEnum enumeration [ADOX]
ms.assetid: f948febd-c885-4621-823b-421e116fec4e
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7a38f635c03567d224559382979717c9098ddc9c
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="actionenum"></a>ActionEnum
Gibt den Typ der Aktion, die beim [SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md) aufgerufen wird.  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adAccessDeny**|3|Der Gruppen- oder Benutzernamen wird die angegebenen Berechtigungen verweigert werden.|  
|**adAccessGrant**|1|Der Gruppen- oder Benutzernamen müssen mindestens die angeforderten Berechtigungen.|  
|**adAccessRevoke**|4|Keine explizite Zugriffsrechte der Gruppe bzw. des Benutzers werden aufgehoben.|  
|**adAccessSet**|2|Der Gruppen- oder Benutzernamen müssen genau die angeforderten Berechtigungen.|
