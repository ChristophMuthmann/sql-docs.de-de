---
title: Standard-Treiber-Unterschlüssel | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
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
ms.openlocfilehash: c527f50ad8e71879a91b9b8f13262c5dce1a893f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
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
