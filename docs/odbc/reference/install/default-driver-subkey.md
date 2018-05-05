---
title: Standard-Treiber-Unterschlüssel | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- default subkey [ODBC]
- registry entries for components [ODBC], default subkey
- subkeys [ODBC], default subkey
- drivers subkey [ODBC]
ms.assetid: 9e58b24f-ebfc-4286-a272-0843b4d6f2d5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6563627087ce8516f74f478b35f0f6a896aa025b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="default-driver-subkey"></a>Standard-Treiber Unterschlüssel
Der Standard-Unterschlüssel enthält einen einzelnen Wert, der den Treiber, die von der Standarddatenquelle verwendete beschreibt. Das Format dieses Werts wird in der folgenden Tabelle dargestellt.  
  
|Name|Datentyp|data|  
|----------|---------------|----------|  
|**Treiber**|REG_SZ|*Standard-Treiber-Beschreibung*|  
  
 Die *Treiber standardbeschreibung* Name ist identisch mit den Namen des Werts unter der ODBC-Treiber-Unterschlüssel, die den Treiber beschreibt.  
  
 Wenn die Datenquelle standardmäßig den SQL Server-Treiber verwendet, kann z. B. der Wert unter dem Unterschlüssel Standard sein:  
  
```  
Driver : REG_SZ : SQL Server  
```  
  
> [!NOTE]  
>  Der in der Standardeinstellung Unterschlüssel enthaltenen Treiber kann auf einem Standardbenutzer-DSN oder ein Standardsystem-DSN verweisen. Wenn ein Standardbenutzer-DSN und einem Standardsystem DSN erstellt wurden, der Standardtreiber richtet sich nach der DSN, der zuletzt erstellt wurde, sodass er ein gültiger Eintrag für den DSN möglicherweise nicht, die erstmalig erstellt wurde.
