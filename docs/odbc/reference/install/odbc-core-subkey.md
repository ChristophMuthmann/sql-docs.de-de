---
title: ODBC Core Unterschlüssel | Microsoft Docs
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
- subkeys [ODBC], core subkey
- registry entries for components [ODBC], core subkey
- core subkey [ODBC]
ms.assetid: 055b31fc-f96c-450b-a596-d4570079fbf2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f05e36c59d674104dead92ecd7da63f5fb58588a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="odbc-core-subkey"></a>ODBC Core Unterschlüssel
Der Wert unter dem Unterschlüssel ODBC Core bietet der Verwendungszähler für die Kernkomponenten (Treiber-Manager, Cursorbibliothek, Installer DLL usw.). Das Format dieses Werts wird in der folgenden Tabelle dargestellt.  
  
|Name|Datentyp|data|  
|----------|---------------|----------|  
|UsageCount|REG_DWORD-WERT|*count*|  
  
 Nehmen Sie beispielsweise an, dass durch die Setupprogramme für drei verschiedenen Anwendungen und zwei verschiedenen Treiber die ODBC-Kernkomponenten installiert wurden. Der Wert unter dem Unterschlüssel ODBC Core würde folgendermaßen lauten:  
  
```  
UsageCount : REG_DWORD : 0x5  
```
