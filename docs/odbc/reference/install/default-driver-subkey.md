---
title: "Standard-Treiber-Unterschlüssel | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- default subkey [ODBC]
- registry entries for components [ODBC], default subkey
- subkeys [ODBC], default subkey
- drivers subkey [ODBC]
ms.assetid: 9e58b24f-ebfc-4286-a272-0843b4d6f2d5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5c269705f5e4c0c855b5b7f929b1a76ee9523bd7
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

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
